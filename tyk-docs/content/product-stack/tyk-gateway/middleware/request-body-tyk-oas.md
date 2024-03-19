---
title: Using the Request Body Transform middleware with Tyk OAS APIs
date: 2024-02-07
description: "Using the Request Body Transform middleware with Tyk OAS APIs"
tags: ["request transform", "body transform", "transform", "middleware", "per-endpoint", "Tyk OAS", "Tyk OAS API"]
---

The [request body transform]({{< ref "transform-traffic/request-body" >}}) middleware provides a way to modify the payload of API requests before they are proxied to the upstream.

The middleware is configured in the [Tyk OAS API Definition]({{< ref "tyk-apis/tyk-gateway-api/oas/x-tyk-oas-doc#operation" >}}). You can do this via the Tyk Dashboard API or in the API Designer.

If you're using the legacy Tyk Classic APIs, then check out the [Tyk Classic]({{< ref "product-stack/tyk-gateway/middleware/request-body-tyk-classic" >}}) page.

## Configuring the middleware in the Tyk OAS API Definition
The design of the Tyk OAS API Definition takes advantage of the `operationID` defined in the OpenAPI Document that declares both the path and method for which the middleware should be added.

The request body transformation middleware (`transformRequestBody`) can be added to the `operations` section of the Tyk OAS Extension (`x-tyk-api-gateway`) in your Tyk OAS API Definition for the appropriate `operationId` (as configured in the `paths` section of your OpenAPI Document).

The `transformRequestBody` object has the following configuration:
 - `enabled`: enable the middleware for the endpoint
 - `format`: the format of input data the parser should expect (either `xml` or `json`)
 - `body`: [see note] this is a `base64` encoded representation of your template
 - `path`: [see note] this is the path to the text file containing the template

{{< note success >}}
**Note**  

You should configure only one of `body` or `path` to indicate whether you are embedding the template within the middleware or storing it in a text file. The middleware will automatically select the correct source based on which of these fields you complete. If both are provided, then `body` will take precedence and `path` will be ignored.
{{< /note >}}

For example:
```.json {hl_lines=["39-43"],linenos=true, linenostart=1}
{
    "components": {},
    "info": {
        "title": "example-request-body-transform",
        "version": "1.0.0"
    },
    "openapi": "3.0.3",
    "paths": {
        "/anything": {
            "put": {
                "operationId": "anythingput",
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
            "name": "example-request-body-transform",
            "state": {
                "active": true
            }
        },
        "upstream": {
            "url": "http://httpbin.org/"
        },
        "server": {
            "listenPath": {
                "value": "/example-request-body-transform/",
                "strip": true
            }
        },
        "middleware": {
            "operations": {
                "anythingput": {
                    "transformRequestBody": {
                        "enabled": true,
                        "format": "json",
                        "body": "ewogICJ2YWx1ZTEiOiAie3sudmFsdWUyfX0iLAogICJ2YWx1ZTIiOiAie3sudmFsdWUxfX0iLAogICJyZXEtaGVhZGVyIjogInt7Ll90eWtfY29udGV4dC5oZWFkZXJzX1hfSGVhZGVyfX0iLAogICJyZXEtcGFyYW0iOiAie3suX3R5a19jb250ZXh0LnJlcXVlc3RfZGF0YS5wYXJhbX19Igp9"
                    }
                }
            }
        }
    }
}
```

In this example the request body transform middleware has been configured for HTTP `PUT` requests to the `/anything` endpoint. The `body` contains a base64 encoded Go template (which you can check by pasting the value into a service such as [base64decode.org](https://www.base64decode.org)).

Decoded, this template is:
```go
{
  "value1": "{{.value2}}",
  "value2": "{{.value1}}",
  "req-header": "{{._tyk_context.headers_X_Header}}",
  "req-param": "{{._tyk_context.request_data.param}}"
}
```

So if you make a request to `PUT /anything?param=foo`, configuring a header `X-Header`:`bar` and providing this request body:
```json
{
    "value1": "world",
    "value2": "hello"
}
```

You will receive a response from the upstream with this payload: 
```json
{
    "req-header": "bar",
    "req-param": "[foo]",
    "value1": "hello",
    "value2": "world"
},
```

The `/anything` endpoint returns the details of the request that was received by httpbin.org. You can see that Tyk has swapped `value1` and `value2` and embedded the `X-Header` header and `param` query values into the body of the request.

The configuration above is a complete and valid Tyk OAS API Definition that you can import into Tyk to try out the mock response middleware.

{{< note success >}}

**Note**  

If using a template in a file (i.e. you configure `path` in the `transformRequestBody` object), remember that Tyk will load and evaluate the template when the Gateway starts up. If you modify the template, you will need to restart Tyk in order for the changes to take effect.

{{< /note >}}

## Configuring the middleware in the API Designer
Adding Request Body Transformation to your API endpoints is easy when using the API Designer in the Tyk Dashboard, simply follow the steps taken in this short video:

 < placeholder for video >

