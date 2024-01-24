---
title: "When To Use do_not_track"
date: 2024-01-22
tags: ["do_not_track"]
description: "Explains do_not_track and the circumstances under which it should be used"
---

Tyk provides the *do_not_track* configuration parameter to disable tracking analytics at two levels:
    - Global: Analytics are not tracked for all endpoints of an API. This feature is configurable in [Tyk OAS APIs]({{< ref "TO DO" >}}) and [Tyk Classic APIs]({{< ref "tyk-apis/tyk-gateway-api/api-definition-objects/other-root-objects" >}})
    - Endpoint: Analytics can be disabled for a specific endpoint. This is configurable at the endpoint level for [Tyk OAS APIs](<< ref "" >>), [Tyk Classic APIs({{< ref "" >}})] and from within the Tyk Dashboard [endpoint designer]({{< ref "advanced-configuration/transform-traffic/endpoint-designer#do-not-track-endpoint" >}}).

## When To Use Do Not Track?
