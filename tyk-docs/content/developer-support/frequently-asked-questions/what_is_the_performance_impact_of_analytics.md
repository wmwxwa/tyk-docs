---
title: "What Is The Performance Impact Of Analytics?"
date: 2024-01-22
tags: ["do_not_track", "Analytics", "RPS", "Requests Per Second", "CPU", "high load", "high traffic"]
description: "This FAQ explains how analytics impacts system performance and how to disable using do_not_track"
---

This FAQ explains how analytics may impact performance relating to high CPU load and reduced Requests Per Second (RPS). Subsequently, it describes how to configure Tyk to reduce this performance impact for platforms that exhibit high volumes of traffic.

## What Are Analytics?
Tyk Gateway allows analytics to be recorded and stored in backend storage (MongoDB/SQL) for all APIs by default, via [Tyk Pump]({{< ref "tyk-stack/tyk-pump/tyk-analytics-record-fields" >}}).

Tyk Gateway generates transaction records for each API request and response, containing [analytics data]({{< ref "tyk-stack/tyk-pump/tyk-analytics-record-fields" >}}) relating to: the originating host (where the request is coming from), which Tyk API version was used, the HTTP method requested and request path etc.

The transaction records are transmitted to Redis and subsequently transferred to a [data sink]({{< ref "tyk-stack/tyk-pump/other-data-stores" >}}) of your choice via Tyk Pump. Furthermore, Tyk Pump can also be configured to [aggregate]({{< ref "tyk-dashboard-analytics#aggregated-analytics" >}}) this data (using different data keys - API ID, access key, endpoint, response status code, location) and write to persistent storage. Tyk Dashboard uses this data for:
- Displaying [analytics]({{< ref "tyk-dashboard-analytics" >}}) based on the aggregated data.
- Browsing logs for the [raw transaction records]({{< ref "tyk-stack/tyk-manager/analytics/log-browser" >}}).

## How Do Analytics Impact Performance?

Analytics may introduce the problem of increased CPU load and a decrease in the number of requests per second (RPS).

In the *Tyk Dashboard API* screen below, there are two APIs, *track* and *notrack*. The APIs were created to conduct a simple load test, to show the gateway's RPS (requests per second) for each API:

- **track**: Analytics are tracked for an API, i.e. *do_not_track* is false.
- **notrack**: Analytics are not tracked for an API, i.e. *do_not_track* is true.

{{< img src="img/faq/do-not-track-usage-scenario/dashboard_apis_measured.png" alt="apis measured in Tyk Dashboard" width="864">}}

100,000 requests were sent to each API and the total number of requests per second was measured. The results for the *tracked* API are displayed in the left pane terminal window; with the right pane showing the results for the *untracked* API.

{{< img src="img/faq/do-not-track-usage-scenario/do_not_track_performance_impact.png" alt="measuring do_not_track API performance impact" >}}

We can see that **19,253.75** RPS was recorded for the *untracked* API; with **16,743.6011** RPS reported for the *tracked* API. The number of requests per second decreased by **13.0372%** when analytics was enabled.

## What Can Be Done To Address This Performance Impact?

Tyk is configurable, allowing fine grained control over which information should be recorded and which can be skipped, thus reducing CPU cycles, traffic and storage.

Users can selectively disable analytics using the [do_not_track]({{<ref "advanced-configuration/transform-traffic/endpoint-designer#do-not-track-endpoint">}}) configuration parameter. This can configured:

- **Per API**: Tyk Gateway will not create records for requests/responses for any endpoints of an API.
- **Per Endpoint**: Tyk Gateway will not record analytics for requests for a specific endpoint. Other endpoints will be tracked as normal.

When set, this prevents Tyk Gateway from generating the transaction records. Without transaction records, Tyk Pump will not transfer analytics to the chosen data sink. It's worth noting that the "track" middleware exclusively influences the generation of *endpoint popularity* aggregated data by *Tyk Pump*.

## Conclusion

[Disabling]({{<ref "product-stack/tyk-gateway/middleware/do-not-track-middleware">}})  the creation of analytics (either per API or for specific endpoints) helps to reduce CPU cycles and network requests for systems that exhibit high load and traffic, e.g. social media platforms, streaming, financial services and trading platforms.

Application decisions need to be made concerning which endpoints are non critical and can thus have analytics disabled. Furthermore, benchmarking and testing will be required to evaluate the actual benefits for the application specific use case.

Subsequently, it is worthwhile monitoring traffic and system load and using this feature to improve performance. 
