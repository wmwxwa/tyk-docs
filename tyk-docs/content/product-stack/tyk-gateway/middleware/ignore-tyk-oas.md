---
title: Using the Ignore Authentication middleware with Tyk OAS APIs
date: 2024-01-24
description: "Using the Ignore Authentication middleware with Tyk OAS APIs"
tags: ["ignore authentication", "ignore", "ignore auth", "authentication", "middleware", "per-endpoint", "Tyk OAS"]
---

The [Ignore Authentication]({{< ref "product-stack/tyk-gateway/middleware/ignore-middleware" >}}) middleware instructs Tyk Gateway to skip the authentication step for calls to an endpoint, even if authentication is enabled for the API.

When working with Tyk OAS APIs the middleware is configured in the [Tyk OAS API Definition]({{< ref "tyk-apis/tyk-gateway-api/oas/x-tyk-oas-doc#operation" >}}) either manually within the `.json` file or from the API Designer in the Tyk Dashboard.

If you're using the legacy Tyk Classic APIs, then check out the [Tyk Classic]({{< ref "product-stack/tyk-gateway/middleware/ignore-tyk-classic" >}}) page.

## Configuring the middleware in the Tyk Classic API Definition
The design of the Tyk OAS API Definition takes advantage of the `operationID` defined in the OpenAPI Document that declares both the path and method for which the middleware should be added.

The ignore authentication middleware (`ignoreAuthentication`) can be added to the `operations` section of the Tyk OAS Extension (`x-tyk-api-gateway`) in your Tyk OAS API Definition for the appropriate `operationId` (as configured in the `paths` section of your OpenAPI Document).

The `ignoreAuthentication` object has the following configuration:
 - `enabled`: enable the middleware for the endpoint
 - `ignoreCase`: if set to `true` then the path matching will be case insensitive

For example:
```.json {hl_lines=["47-50", "53-56"],linenos=true, linenostart=1}
{
    "components": {},
    "info": {
        "title": "example-ignore-authentication",
        "version": "1.0.0"
    },
    "openapi": "3.0.3",
    "paths": {
        "/status/200": {
            "get": {
                "operationId": "status/200get",
                "responses": {
                    "200": {
                        "description": ""
                    }
                }
            }
        }
    },
    "x-tyk-api-gateway": {
        "info": {
            "name": "example-ignore-authentication",
            "state": {
                "active": true
            }
        },
        "upstream": {
            "url": "http://httpbin.org/"
        },
        "server": {
            "listenPath": {
                "value": "/example-ignore-authentication/",
                "strip": true
            }
        },
        "middleware": {
            "operations": {
                "status/200get": {
                    "ignoreAuthentication": {
                        "enabled": true,
                        "ignoreCase": false
                    }                
                }
            }
        }
    }
}
```

In this example the ignore authentication middleware has been configured for HTTP `GET` requests to the `/status/200` endpoint. Any such calls will skip the authentication step in the Tyk Gateway's processing chain.
 - the allow list has been configured to be case sensitive, so calls to `GET /Status/200` will not skip authentication

The configuration above is a complete and valid Tyk OAS API Definition that you can import into Tyk to try out the API-level response header transform.

## Configuring the middleware in the API Designer
Adding Ignore Authentication to your API endpoints is easy when using the API Designer in the Tyk Dashboard, simply follow the steps taken in this short video:

 < placeholder for video >
