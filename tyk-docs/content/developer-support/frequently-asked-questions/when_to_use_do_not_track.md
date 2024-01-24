---
title: "When To Use do_not_track Analytics"
date: 2024-01-22
tags: ["do_not_track", Analytics]
description: "Explains do_not_track Analytics and the circumstances under which it should be used"
---

Tyk provides the *do_not_track* configuration parameter to disable tracking analytics at two levels:

- **Global**: Analytics are not tracked for all endpoints of an API. This feature is configurable in [Tyk OAS APIs]() and [Tyk Classic APIs]({{< ref "tyk-apis/tyk-gateway-api/api-definition-objects/other-root-objects" >}})
- **Endpoint**: Analytics can be disabled for a specific endpoint. This is configurable at the endpoint level for [Tyk OAS APIs](), [Tyk Classic APIs]() and from within the Tyk Dashboard [endpoint designer]({{< ref "advanced-configuration/transform-traffic/endpoint-designer#do-not-track-endpoint" >}}).

## How Does This Impact Performance?

In the image below we can see two APIs were setup within Tyk Dashboard:

- **track**: Analytics are tracked for an API, i.e. *track_enabled* is false.
- **notrack**: Analytics are not tracked for an API, i.e. *track_enabled* is true.

{{< img src="img/faq/do-not-track-usage-scenario/dashboard_apis_measured.png" alt="apis measured in Tyk Dashboard" >}}

100,000 requests were sent to each API and the total number of requests per second was measured. The results are illustrated below. The results for the *tracked* API are displayed in the left pane terminal window; with the right pane shown the results for the *untracked* API.

{{< img src="img/faq/do-not-track-usage-scenario/do_not_track_performance_impact.png" alt="measuring do_not_track API performance impact" >}}

We can see that 19253.75 requests per second was recorded for the *untracked* API; with 16743.6011 requests per second reported for the *tracked* API. The number of requests per seconds decreased by 13.0372% when analytics was enabled.

## When To Use Do Not Track?

<!-- TODO -->