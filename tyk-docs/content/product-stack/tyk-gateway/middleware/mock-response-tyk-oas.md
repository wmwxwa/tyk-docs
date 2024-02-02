---
title: Using the Mock Response middleware with Tyk OAS APIs
date: 2024-01-31
description: "Using the Mock Response middleware with Tyk OAS APIs"
tags: ["mock response", "middleware", "per-endpoint", "Tyk OAS", "Tyk OAS API"]
---

The [Mock Response]({{< ref "product-stack/tyk-gateway/middleware/mock-response-middleware" >}}) middleware allows you to configure Tyk to return a response for an API endpoint without requiring an upstream service. This can be useful when creating a new API or making a development API available to an external team.

When working with Tyk OAS APIs, this middleware is executed at the end of the request processing chain immediately prior to the upstream proxy stage. Thus, any other request processing middleware - including authentication - will be run before the request reaches the mock response.

The middleware is configured in the [Tyk OAS API Definition]({{< ref "tyk-apis/tyk-gateway-api/oas/x-tyk-oas-doc#operation" >}}). You can do this via the Tyk Dashboard API or in the API Designer.

Tyk can automatically populate the Mock Response middleware with [example values](#example-responses-in-openapi-specification) taken from the OpenAPI Document, or you can configure the response [manually](#manually-configuring-the-middleware-in-the-tyk-oas-api-definition). 

If you're using the legacy Tyk Classic APIs, then check out the [Tyk Classic]({{< ref "product-stack/tyk-gateway/middleware/mock-response-tyk-classic" >}}) page.

## Example responses in OpenAPI Specification
The [OpenAPI Specification](https://learn.openapis.org/specification/docs.html#adding-examples) includes metadata that can be used by automatic documentation generators to produce comprehensive reference guides for APIs. Most objects in the specification include a `description` field that can provide additional human-readable information that is fed into such documentation. Alongside the descriptions, some OpenAPI objects can have `example` values listed in the OpenAPI Document that further enhance the generated documentation by giving representative content that the upstream service might provide in responses.

The specification provides two different ways for an API developer to provide sample responses for an endpoint:
 - `example`: a sample value that could be returned in a specific field in a response
 - `examples`: a list of key-value pairs comprising of `"exampleName":"value"`

Note that `example` and `examples` are mutually exclusive within the OpenAPI Document for a field in the `responses` object: the developer cannot provide both for the same object. The content-type (e.g. `application/json`, `text/plain`) must be declared for each `example` or `examples` in the API description.

The `exampleName` defined with `examples` can be used to [invoke the desired response](#working-with-multiple-mock-responses-for-an-endpoint) from a mocked endpoint.

Tyk can also automatically create a mock response if a `schema` is defined that describes the format of the response.

### `example`
```.json {hl_lines=["9-10"],linenos=true, linenostart=1}
{
  "paths": {
    "/get": {
      "get": {
        "operationId": "getget",
        "responses": {
          "200": {
            "content": {
                "text/plain": {
                    "example": "Furkan"
                }
            },
            "description": ""
          }
        }
      }
    }
  }
}
```
In this extract from an OpenAPI Document, a single `example` has been declared for a request to `GET /get` - the API developer indicates that such a call could return `HTTP 200` and the body value `Furkan` in plain text format.

### `examples`
```.json {hl_lines=["9-18"],linenos=true, linenostart=1}
{  
  "paths": {
    "/get": {
      "get": {
        "operationId": "getget",
        "responses": {
          "200": {
            "content": {
              "text/plain": {
                "examples": {
                    "first-example": {
                        "value": "Jeff"
                    },
                    "second-example": {
                        "value": "Laurentiu"
                    }
                }
              }
            },
            "description": ""
          }
        }
      }
    }
  }
}
```
In this extract, the API developer also indicates that a call to a`GET /get` could return `HTTP 200` but here provides two example body values `Jeff` and `Laurentiu`, again in plain text format. The `exampleNames` for these two values have been configured as `first-example` and `second-example`.

### `schema`
If there is no `example` or `examples` defined for an endpoint, Tyk will try to find a `schema` for the response. If there is a schema, it will be used to generate a mock response. Tyk can extract values from a referenced or nested schema objects when creating the mock response.

Response headers do not have standalone `example` or `examples` attributes, however they can have a `schema` - the Mock Response middleware will include these in the mock response if provided in the OpenAPI description.

The schema properties may have an `example` field, in which case they will be used to build a mock response, however if there is no `example` value in the schema then default values are used to build a response as follows:
- `string` > `string`
- `integer` > `0`
- `boolean` > `true`

For example:
```.json {hl_lines=["10-13", "18-33"],linenos=true, linenostart=1}
{
    "paths": {
        "/get": {
            "get": {
                "operationId": "getget",
                "responses": {
                    "200": {
                        "headers": {
                            "X-Status": {
                                "schema": {
                                    "type": "string",
                                    "example": "Foobar"
                                }
                            }
                        },
                        "content": {
                            "application/json": {
                                "schema": {
                                    "type": "object",
                                    "properties": {
                                        "lastName": {
                                            "example": "Bar",
                                            "type": "string"
                                        },
                                        "name": {
                                            "example": "Foo",
                                            "type": "string"
                                        },
                                        "id": {
                                            "type": "integer"
                                        }
                                    }
                                }
                            }
                        },
                        "description": ""
                    }
                }
            }
        }
    }
    "x-tyk-api-gateway": {
        "middleware": {
            "operations": {
                "getget": {
                    "mockResponse": {
                        "enabled": true,
                        "fromOASExamples": {
                            "enabled": true
                        }
                    }
                }
            }
        }
    }
}
```

This partial Tyk OAS API Definition would generate a mock response for calls to the `GET /get` endpoint from the schema defined in the OpenAPI description.

A call to this endpoint would return the following:

```
HTTP/1.1 200 OK
X-Status: Foobar
Content-Type: application/json
 
{
  "name": "Foo",
  "lastName": "Bar",
  "id": 0
}
```

## Manually configuring the middleware in the Tyk OAS API Definition
The design of the Tyk OAS API Definition takes advantage of the `operationID` defined in the OpenAPI Document that declares both the path and method for which the middleware should be added.

The mock response middleware (`mockResponse`) can be added to the `operations` section of the Tyk OAS Extension (`x-tyk-api-gateway`) in your Tyk OAS API Definition for the appropriate `operationId` (as configured in the `paths` section of your OpenAPI Document).

The `mockResponse` object has the following configuration:
 - `enabled`: enable the middleware for the endpoint
 - `code`: the HTTP status code to be provided with the response (this defaults to `200` if not set)
 - `body`: the payload to be returned as the body of the response
 - `headers`: the headers to inject with the response

For example:
```.json {hl_lines=["39-49"],linenos=true, linenostart=1}
{
    "components": {},
    "info": {
        "title": "example-mock-response",
        "version": "1.0.0"
    },
    "openapi": "3.0.3",
    "paths": {
        "/anything": {
            "get": {
                "operationId": "anythingget",
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
            "name": "example-mock-response",
            "state": {
                "active": true
            }
        },
        "upstream": {
            "url": "http://httpbin.org/"
        },
        "server": {
            "listenPath": {
                "value": "/example-mock-response/",
                "strip": true
            }
        },
        "middleware": {
            "operations": {
                "anythingget": {
                    "mockResponse": {
                        "enabled": true,
                        "code": 200,
                        "body": "This is the mock response body",
                        "headers": [
                            {
                                "name": "X-Example-Header",
                                "value": "foobar"
                            }
                        ]
                    }
                }
            }
        }
    }
}
```

In this example the mock response middleware has been configured for HTTP `GET` requests to the `/anything` endpoint.

A call to `GET /anything` would return:

```
HTTP/1.1 200 OK
X-Example-Header: foobar
Content-Type: text/plain; charset=utf-8
 
This is the mock response body
```

The configuration above is a complete and valid Tyk OAS API Definition that you can import into Tyk to try out the mock response middleware.

## Automatically configuring the middleware from the OpenAPI Document
You can direct Tyk to configure the Mock Response middleware automatically from the examples and schema [defined](#example-responses-in-openapi-specification) in the OpenAPI description by enabling the middleware for an endpoint and configuring the `fromOASExamples` object wiithin that.

The middleware (`mockResponse`) can be added to the `operations` section of the Tyk OAS Extension (`x-tyk-api-gateway`) in your Tyk OAS API Definition for the appropriate `operationId` (as configured in the `paths` section of your OpenAPI Document).

The `fromOASExamples` object has the following configuration:
 - `enabled`: enable the automatic configuration of mock response
 - `code`: [optional] identifies which HTTP status code to be provided with the response (defaults to `200` if not set)
 - `contentType`: [optional] identifies which response body type (defaults to `application/json` if not set)
 - `exampleName`: [optional] the sample response to be returned from an `examples` list

The three optional fields (`code`, `contentType`, `exampleName`) are used to identify which sample response should be returned by the mock if multiple sample responses are declared in the OpenAPI Document.

For example:
```.json {hl_lines=["15-24", "29-33", "59-67"],linenos=true, linenostart=1}
{  
    "components": {},
    "info": {
        "title": "example-mock-response",
        "version": "1.0.0"
    },
    "openapi": "3.0.3",
    "paths": {
        "/anything": {
            "get": {
                "operationId": "anythingget",
                "responses": {
                    "200": {
                        "content": {
                            "text/plain": {
                                "examples": {
                                    "first-example": {
                                        "value": "Petric"
                                    },
                                    "second-example": {
                                        "value": "Andrei"
                                    }
                                }
                            }
                        },
                        "description": ""
                    },
                    "300": {
                        "content": {
                            "text/plain": {
                                "example": "Maciej"
                            }
                        },
                        "description": ""
                    }
                }
            }
        }
    },
    "x-tyk-api-gateway": {
        "info": {
            "name": "example-mock-response",
            "state": {
                "active": true
            }
        },
        "upstream": {
            "url": "http://httpbin.org/"
        },
        "server": {
            "listenPath": {
                "value": "/example-mock-response/",
                "strip": true
            }
        },
        "middleware": {
            "operations": {
                "anythingget": {
                    "mockResponse": {
                        "enabled": true,
                        "fromOASExamples": {
                            "enabled": true,
                            "code": 200,
                            "contentType": "text/plain",
                            "exampleName": "second-example"
                        }
                    }
                }
            }
        }
    }
}
```

In this example, the OpenAPI document declares three possible responses: two for HTTP 200 and one for HTTP 300. We have configured the Mock Response middleware to return the value defined for HTTP 200 (code) with `exampleName` set to "second-example".

If you make a call to `GET /anything` the response will be:
```
HTTP/1.1 200 OK
Content-Type: text/plain
X-Ratelimit-Limit: 0
X-Ratelimit-Remaining: 0
X-Ratelimit-Reset: 0
Date: Thu, 01 Feb 2024 12:31:50 GMT
Content-Length: 8
 
"Andrei"
```

If you add `"code":300` in the `fromOASExamples` object, a call to `GET /anything` will instead respond as follows:
```
HTTP/1.1 300 Multiple Choices
Content-Type: text/plain
X-Ratelimit-Limit: 0
X-Ratelimit-Remaining: 0
X-Ratelimit-Reset: 0
Date: Thu, 01 Feb 2024 12:35:45 GMT
Content-Length: 8
 
"Maciej"
```

{{< note success >}}
**Note**  

If multiple `examples` are defined in the OpenAPI description but no default `exampleName` is set in the middleware configuration `fromOASExamples` Tyk will select randomly from the multiple `examples`. Yes, that means the response may change with every request. You can [control which response](#working-with-multiple-mock-responses-for-an-endpoint) will be returned using special headers in the request.
{{< /note >}}

The configuration above is a complete and valid Tyk OAS API Definition that you can import into Tyk to try out the mock response middleware.

## Configuring the middleware in the API Designer
Adding a Mock Response to your API endpoints is easy when using the API Designer in the Tyk Dashboard, simply follow the steps taken in these short videos:

 < placeholder for "classic style" video >
 < placeholder for "openapi style" video >

## Working with multiple mock responses for an endpoint
The Mock Response middleware is enabled and configured in the Tyk OAS API definition to provide a default response to requests to an endpoint. Where the middleware is configured to return responses from the OpenAPI description within the API definition, you can configure the request to invoke a specific response, overriding the defaults configured in the middleware.

To invoke a non-default response from a mocked endpoint, you must add one or more special headers to the request:
- `Accept`: This standard HTTP header will override the response content type (e.g. `application/json`, `text/plain`)
- `X-Tyk-Accept-Example-Code`: This will select the HTTP response code for which to return the example response (e.g. `400`)
- `X-Tyk-Accept-Example-Name`: This identifies which example to select from an `examples` list

If an example response can’t be found for the configured `code`, `contentType` or `exampleName`, an HTTP 404 error will be returned to inform the client that there is no declared example for that configuration.

For example:
```.json {hl_lines=["15-19", "22-39", "45-50", "53-55", "82-89"],linenos=true, linenostart=1}
{  
    "components": {},
    "info": {
        "title": "example-mock-response",
        "version": "1.0.0"
    },
    "openapi": "3.0.3",
    "paths": {
        "/anything": {
            "get": {
                "operationId": "anythingget",
                "responses": {
                    "200": {
                        "headers": {
                            "X-Status": {
                                "schema": {
                                    "type": "boolean"
                                }
                            }
                        },
                        "content": {
                            "application/json": {
                                "schema": {
                                    "type": "object",
                                    "properties": {
                                        "lastName": {
                                            "example": "Bar",
                                            "type": "string"
                                        },
                                        "name": {
                                            "example": "Foo",
                                            "type": "string"
                                        },
                                        "id": {
                                            "type": "integer"
                                        }
                                    }
                                }
                            }
                        },
                        "description": ""
                    },
                    "300": {
                        "headers": {
                            "X-Status": {
                                "schema": {
                                    "type": "boolean",
                                    "example": false
                                }
                            }
                        },
                        "content": {
                            "text/plain": {
                                "example": "Warlock"
                            }
                    },
                    "description": ""
                    } 
               }
            }
        }
    },
    "x-tyk-api-gateway": {
        "info": {
            "name": "example-mock-response",
            "state": {
                "active": true
            }
        },
        "upstream": {
            "url": "http://httpbin.org/"
        },
        "server": {
            "listenPath": {
                "value": "/example-mock-response/",
                "strip": true
            }
        },
        "middleware": {
            "operations": {
                "anythingget": {
                    "mockResponse": {
                        "enabled": true,
                        "fromOASExamples": {
                            "enabled": true,
                            "code": 200,
                            "contentType": "application/json"
                        }
                    }
                }
            }
        }
    }
}
```

In this example, the OpenAPI document declares two possible responses: one for HTTP 200 and one for HTTP 300. We have configured the Mock Response middleware to return the value defined for HTTP 200 for which the body (content) is in JSON format and a custom header `X-Status` which will take the default value of `true`.

You can trigger the mock response for HTTP 300 by adding the following headers to your request:
 - `X-Tyk-Accept-Example-Code`: 300
 - `Accept`: text/plain

This would return a plain text body and the `X-Status` header set to `false`.

The configuration above is a complete and valid Tyk OAS API Definition that you can import into Tyk to try out the mock response middleware.