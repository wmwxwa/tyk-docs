---
title: Using the Request Body Transform middleware with Tyk Classic APIs
date: 2024-02-02
description: "Using the Request Validation middleware with Tyk Classic APIs"
tags: ["request validation", "validate JSON", "middleware", "per-endpoint", "Tyk Classic", "Tyk Classic API"]
---

The [request body transform]({{< ref "transform-traffic/request-body" >}}) middleware provides a way to modify the payload of API requests before they are proxied to the upstream.

This middleware is configured in the Tyk Classic API Definition at the endpoint level. You can do this via the Tyk Dashboard API or in the API Designer.

If you're using the newer Tyk OAS APIs, then check out the [Tyk OAS]({{< ref "product-stack/tyk-gateway/middleware/request-body-tyk-oas" >}}) page.

## Configuring the middleware in the Tyk Classic API Definition
To enable the middleware you must add a new `transform` object to the `extended_paths` section of your API definition.

The `transform` object has the following configuration:
 - `path`: the path to match on
 - `method`: this method to match on
 - `template_data`: details of the Go template to be applied for the transformation of the request body
 - `fromDashboard`: an optional boolean flag set to `true` if XXX 
 
The Go template is described in the `template_data` object by the following fields:
 - `input_type`: the format of input data the parser should expect (either `xml` or `json`)
 - `enable_session`: set this to `true` to make session metadata available to the transform template
 - `template_mode`: informs the middleware whether to look for the template in a `file` or in a base64 encoded `blob`; the actual file location (or base64 encoded template) is provided in `template_source`
 - `template_source`: if `template_mode` is set to `file`, this will be the path to the file containing the template. If `template_mode` is set to `blob`, this will be a `base64` encoded representation of your template

For example:
```.json  {linenos=true, linenostart=1}
{
    "extended_paths": {
        "transform": [
            {
                "path": "/anything",
                "method": "POST",
                "template_data": {
                    "template_mode": "file",
                    "template_source": "./templates/transform_test.tmpl",
                    "input_type": "json",
                    "enable_session": true,
                }
            }
        ]
    }
}
```

In this example, the Request Body Transform middleware is directed to use the template located in the `file` at location `./templates/transform_test.tmpl`. The input (pre-transformation) request payload will be `json` format and session metadata will be available for use in the transformation.

{{< note success >}}

**Note**  

Tyk will load and evaluate the template when the Gateway starts up. If you modify the template, you will need to restart Tyk in order for the changes to take effect.

{{< /note >}}

## Configuring the middleware in the API Designer
You can use the API Designer in the Tyk Dashboard to configure the request body transform middleware for your Tyk Classic API by following these steps.

#### Step 1: Add an endpoint for the path and select the plugin
From the **Endpoint Designer** add an endpoint that matches the path for which you want to allow access. Select the **Body Transforms** plugin.

{{< img src="/img/2.10/body_transforms.png" alt="Endpoint designer" >}}

#### Step 2: Configure the middleware
Select your input type, and then add the template you would like to use to the **Template** input box.

### Step 3: Test the Transform

If you have sample input data, you can use the Input box to add it, and then test it using the **Test** button. You will see the effect of the template on the sample input in the Output box.

{{< img src="/img/dashboard/system-management/define_transform_2.5.png" alt="Body transform" >}}

#### Step 4: Save the API
Use the *save* or *create* buttons to save the changes and activate the Request Body Transform middleware.

Note that if you provide a sample Input and generate the sample Output per step 3, then these will be appended to the `template_data` object in the API definition, together with a boolean flag `fromDashboard`, which will be set to `true`.

## XML Data

We have a video that demonstrates how the XML to JSON transform works, using the sample Input and template below.

{{< youtube kLh_qAI3meE >}}
