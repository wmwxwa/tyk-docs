---
title: "When To Use Do Not Track Analytics"
date: 2024-01-22
tags: ["do_not_track", Analytics]
description: "This FAQ explains when not to use do_not_track Analytics"
---

Tyk allows analytics to be recorded for API endpoints. This can increase the CPU load and subsequently reduce the RPS (requests per second).

Tyk provides the [do_not_track]({{<ref "advanced-configuration/transform-traffic/endpoint-designer#do-not-track-endpoint">}}) configuration parameter to disable analytics recording at two levels:

- **Per API**: Tyk Gateway will not record analytics for requests/responses of all the endpoints of this API.
- **Endpoint**: Tyk Gateway will not record analytics for requests to the selected endpoint. Other endpoints will be tracked as normal.

Enabling [do_not_track]({{<ref "advanced-configuration/transform-traffic/endpoint-designer#do-not-track-endpoint">}}) can help reduce analytics traffic for systems that are under high load, exhibiting high traffic, e.g. social media platforms, streaming services and financial services and trading platforms.

Application decisions need to be made concerning which endpoints are non critical and can thus have analytics disabled. Furthermore, benchmarking and testing will be required to evaluate the actual benefits for the application specific use case.

In the *Tyk Dashboard API* screen below, there are two APIs, *track* and *notrack*. The APIs were created to conduct a simple load test, to show the gateway's RPS (requests per second) for each API:

- **track**: Analytics are tracked for an API, i.e. *do_not_track* is false.
- **notrack**: Analytics are not tracked for an API, i.e. *do_not_track* is true.

{{< img src="img/faq/do-not-track-usage-scenario/dashboard_apis_measured.png" alt="apis measured in Tyk Dashboard" >}}

100,000 requests were sent to each API and the total number of requests per second was measured. The results for the *tracked* API are displayed in the left pane terminal window; with the right pane showing the results for the *untracked* API.

{{< img src="img/faq/do-not-track-usage-scenario/do_not_track_performance_impact.png" alt="measuring do_not_track API performance impact" >}}

We can see that **19,253.75** RPS was recorded for the *untracked* API; with **16,743.6011** RPS reported for the *tracked* API. The number of requests per second decreased by **13.0372%** when analytics was enabled. Subsequently, it is worthwhile monitoring traffic and system load and using this feature to improve performance. 
