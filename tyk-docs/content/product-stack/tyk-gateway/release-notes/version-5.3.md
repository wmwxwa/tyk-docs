---
title: Tyk Gateway 5.3 Release Notes
date: 2023-09-27T15:49:11Z
description: "Release notes documenting updates enhancements, and changes for Tyk Gateway versions within the 5.3.X series."
tags: ["Tyk Gateway", "Release notes", "v5.3", "5.3.0", "5.3", "changelog"]
---

<!-- Required. oss or licensed. Choose one of the following:
    **Licensed Protected Product**
    Or
    ****Open Source** ([Mozilla Public License](https://github.com/TykTechnologies/tyk/blob/master/LICENSE.md))**
-->

**Open Source** ([Mozilla Public License](https://github.com/TykTechnologies/tyk/blob/master/LICENSE.md))

**This page contains all release notes for version 5.3.X displayed in a reverse chronological order**

## Support Lifetime
<!-- Required. replace X.Y with this release and set the correct quarter of the year -->
Our minor releases are supported until our next minor comes out. This would be <vX.Y+1> scheduled in Q<1-4> if this goes ahead as planned. If not, X.Y will remain in support until our next LTS version comes out in March 2024.

---

## 5.3.0 Release Notes

### Release Date DD Mon YYYY <<update>>

### Breaking Changes
<!-- Required. Use the following statement if there are no breaking changes, or explain if there are -->
**Attention: Please read this section carefully.**

As Tyk OAS transitions out of Early Access, we cannot guarantee backward compatibility for versions pre 5.3.0. When upgrading to 5.3.0, Tyk will automatically migrate existing Tyk OAS APIs, however, post migrations, there’s a risk that downgrading to pre 5.3.0 versions may render the API definitions non-functional. We recommend retaining copies of existing TYK OAS API definitions before upgrading.

Users are strongly advised to follow the recommended upgrade instructions provided by Tyk before applying any updates.

<!-- The following "Changed error log messages" section is Optional!
Instructions: We should mention in the changelog section ALL changes in our application log messages. In case we made such changes, this section should also be added, to make sure the users don't miss this notice among other changelog lines. -->
<!-- #### Changed error log messages
Important for users who monitor Tyk components using the application logs (i.e. Tyk Gateway log, Tyk Dashboard log etc.).
We try to avoid making changes to our log messages, especially at error and critical levels. However, sometimes it's necessary. Please find the list of changes made to the application log in this release: -->

<!-- The following "|Planned Breaking Changes" section is optional!
Announce future scheduled breaking changes, e.g. Go version updates, DB driver updates etc. -->
<!-- #### Planned Breaking Changes -->

### Dependencies
<!--Required. Use this section to announce the following types of dependencies compatible with the release:

Version compatibility with other components in the Tyk stack. This takes the form of a compatibility matrix and is only required for Gateway and Portal.

3rd party dependencies and tools -->

### Compatibility Matrix For Tyk Components
<!-- Required. Version compatibility with other components in the Tyk stack. This takes the form of a compatibility matrix and is only required for Gateway and Portal.
An illustrative example is shown below. -->
| Gateway Version | Recommended Compatibility | Backwards Compatibility |
|----    |---- |---- |
| 5.3 LTS | Helm v2.2     | Helm vX - vY |
|         | MDCB v2.5     | MDCB v1.7 - v2.4 |
|         | Operator v1.8 | Operator vX - vY |
|         | Sync v2.4.1   | Sync vX - vY |
| | | EDP vX - vY |
| | | Pump vX - vY |
| | | TIB vX - vY |

### 3rd Party Dependencies & Tools
<!-- Required. Third-party dependencies encompass tools (GoLang, Helm etc.), databases (PostgreSQL, MongoDB etc.) and external software libraries. This section should be a table that presents the third-party dependencies and tools compatible with the release. Compatible is used in the sense of those versions tested with the releases. Such information assists customers considering upgrading to a specific release.

Additionally, a disclaimer statement was added below the table, for customers to check that the third-party dependency they decide to install remains in support.

An example is given below for illustrative purposes only. Tested Versions and Compatible Versions information will require discussion with relevant squads and QA. -->

| Third Party Dependency                                     | Tested Versions        | Compatible Versions    | Comments | 
| ---------------------------------------------------------- | ---------------------- | ---------------------- | -------- | 
| [GoLang](https://go.dev/dl/)                               | 1.19, 1.20, 1.21       | 1.19, 1.20, 1.21       | All our binaries| 
| [MongoDB](https://www.mongodb.com/try/download/community)  | 4.4.x, 5.0.x and 6.0.x | 4.4.x, 5.0.x and 6.0.x | Used by Tyk Dashboard | 
| [PostgreSQL](https://www.postgresql.org/download/)         | 11.x - 15.x LTS        | 11.x - 15.x            | Used by Tyk Dashboard | 
| OpenAPI JSON Schema  | v3.0.0...      | v3.0.0...          | Used by [Tyk OAS API definition](https://swagger.io/specification/)                | [3.0.3](https://spec.openapis.org/oas/v3.0.3)|

Given the time difference between your upgrade and the release of this version, we recommend customers verify the ongoing support of third-party dependencies they install, as their status may have changed since the release.

### Deprecations
<!-- Required. Use the following statement if there are no deprecations, or explain if there are -->
In 5.3.0, we have simplified the configuration of response transform middleware. We encourage users to embrace the ‘global_headers’ mechanism as the ‘response_processors.header_injector’ is now an optional setting and will be removed in a future release.

<!-- Optional section!
Used to share and notify users about our plan to deprecate features, configs etc. 
Once you put an item in this section, we must keep this item listed in all the following releases till the deprecation happens. -->
<!-- ##### Future deprecations
-->

### Upgrade instructions
<!-- Required. For patches release (Z>0) use this:
For users currently on vX.Y.Z, we strongly recommend promptly upgrading to the latest release. If you are working with an older version (lower major), it is advisable to bypass version X.Y.0 and proceed directly to this latest patch release.
<br/>
Go to the [Upgrading Tyk](#upgrading-tyk) section for detailed upgrade Instructions.
-->
If you are upgrading to 5.3.0, please follow the detailed [upgrade instructions](#upgrading-tyk).


### Release Highlights
<!-- Required. Use similar ToV to previous release notes. For example for a patch release:
This release primarily focuses on bug fixes.
For a comprehensive list of changes, please refer to the detailed [changelog]({{< ref "#Changelog-vX.Y.0">}}) below.
-->
We’re thrilled to announce the release of 5.3.0, an update packed with exciting features and significant fixes to elevate your experience with Tyk Gateway. For a comprehensive list of changes, please refer to the detailed [changelog](#Changelog-v5.3.0) below.


#### Tyk OAS Feature Maturity
Tyk OAS is now out of early access as we have reached feature maturity. We have enabled the majority of its features, which are ready for adoption in Tyk Gateway.

In Tyk 5.3.0 we support the following features when using Tyk OAS APIs with Tyk Gateway:

- API Versioning
- All Tyk-supported client-gateway authentication methods
- Automatic configuration of authentication from the OpenAPI description
- Gateway-upstream mTLS
- CORS
- Custom Plugins
- Open Telemetry tracing
- Response caching
- Detailed log recording
- Do-not-track endpoints
- API-level rate limits
- Request Validation - headers and body
- Request Transformation - method, headers and body
- Response Transformation - headers and body
- Allow and block listing of endpoints
- Circuit breakers
- Enforced timeouts
- URL rewrite and internal endpoints
- Mock Responses (automatically configurable from the OpenAPI description)


#### Implemented KV Store for API Definition Fields
In this release, we have implemented storage for all `string` type APIDefinition fields in separate KV storage, supporting environment variable, Tyk configuration file, Consul and Vault stores.


#### Gateway and Component Upgrades
We've raised the bar with significant upgrades to our Gateway and components. Leveraging the power of Go 1.21, upgrading Sarama to version 1.41.0 and enhancing the GQL engine with Go version 1.19, we ensure improved functionality and performance to support your evolving needs seamlessly.

### Downloads
- [docker image to pull](https://hub.docker.com/layers/tykio/tyk-dashboard/vX.Y.Z/images/blabla)
- <<Helm charts links>>
- [source code tarball for oss projects]()

### Changelog {#Changelog-v5.3.0}
<!-- Required. The change log should include the following ordered set of sections below that briefly summarise the features, updates and fixed issues of the release.

Here it is important to explain the benefit of each changelog item. As mentioned by James in a previous Slack message (https://tyktech.slack.com/archives/C044R3ZTN6L/p1686812207060839?thread_ts=1686762128.651249&cid=C044R3ZTN6L):
"...it is important to document the customer impact for the work delivered, so we can share it with prospects/install base. For example:
"New Chart delivers x and y benefit to a and b customer use cases. The business impact for them will be this and that" -->

#### Added
<!-- This section should be a bullet point list of new features. Explain:

- The purpose of the new feature
- How does the new feature benefit users?
- Link to documentation of the new feature
- For OSS - Link to the corresponding issue if possible on GitHub to allow the users to see further info.

Each change log item should be expandable. The first line summarises the changelog entry. It should be then possible to expand this to reveal further details about the changelog item. This is achieved using HTML as shown in the example below. -->
<ul>
<li>
<details>
<summary>Per-API Rate Limit support in Tyk OAS API Definitions</summary>

Tyk now supports API level rate limit in Tyk OAS API definition.
</details>
</li>
<li>
<details>
<summary>Custom domain certificates support in Tyk OAS API Definitions</summary>

Tyk now supports custom domain certificates in Tyk OAS API definitions.
</details>
</li>
<li>
<details>
<summary>Request method transform middleware support in OAS UI</summary>

Added support for the Request method transform middleware with Tyk OAS APIs.
</details>
</li>
<li>
<details>
<summary>URL rewrite middleware support</summary>

Added support for URL Rewrite middleware with Tyk OAS APIs.
</details>
</li>
<li>
<details>
<summary>Request size limit support</summary>

Added request size limit support for Tyk OAS APIs.
</details>
</li>
<li>
<details>
<summary>Per-endpoint response header transform middleware support</summary>

Added support for modifying the response and request header middleware per-endpoint.
</details>
</li>
<li>
<details>
<summary>Circuit Breaker Middleware support in OAS</summary>

Implemented circuit breaker middleware for Tyk OAS APIs.
</details>
</li>
<li>
<details>
<summary>OAS converter support for *allOf*/*anyOf*/*oneOf* keywords</summary>

The OAS-to-UDG converter now seamlessly handles OAS documents that utilise the *allOf*, *anyOf* and *oneOf* keywords, ensuring accurate and comprehensive conversion to a Tyk API definition. The feature expands the scope of OAS documents that the converter can handle and allows our users to import REST API data sources defined in OAS in more complex cases.
</details>
</li>
<li>
<details>
<summary>Clearer error messages for invalid variables (JSON Schema)</summary>

Some of the error messages generated by the GQL engine were unclear for users, especially relating to variable validation. The errors have been changed and are now much more clearer and helpful in cases where engine processing fails.
</details>
</li>
<li>
<details>
<summary>Upgraded GQL Engine's Go version to 1.19</summary>

Upgraded Go version for GQL engine to [1.19](https://go.dev/doc/go1.19).
</details>
</li>
<li>
<details>
<summary>Enhanced semantic conventions for GraphQL spans in Gateway</summary>

We've added OpenTelemetry semantic conventions for GraphQL spans. Spans will now incorporate `<operation.type>`, `<operation.name>` and `<document>` tags.
</details>
</li>
<li>
<details>
<summary>Added support for *detailed_tracing* in API Definitions for GQL APIs</summary>

GraphQL APIs can now use the `detailed_tracing` setting in an API definition. With that property set to `true` any call to a GraphQL API will create a span for each middleware involved in request processing. While it is set to `false`, only two spans encapsulating the entire request lifecycle will be generated. This setting helps to reduce the size of traces, which can get large for GraphQL APIs. Furthermore, this gives users an option to customise the level of tracing detail to suit their monitoring needs.
</details>
</li>
<li>
<details>
<summary>Enhanced trace generation for UDG with mixed data sources</summary>

This release introduces an enhanced trace generation system for Universal Data Graph (UDG). It consolidates all spans from both Tyk-managed and external data source executions into a single trace when used together. Furthermore, when UDG solely utilises Tyk-managed data sources, trace management is simplified and operational visibility is improved.
</details>
</li>
<li>
<details>
<summary>Disabled *normalise* and *validate* in GraphQL Engine</summary>

For GraphQL requests normalisation and validation has been disabled in the GraphQL engine. Both of those actions were performed in the Tyk Gateway and were unnecessary to be done again in the engine. This enhances performance slightly and makes detailed OTel traces concise and easier to read.
</details>
</li>
<li>
<details>
<summary>Added *introspection_config* to API Definition</summary>

Added a new set of settings in the API definition called *introspection_config*. This enables users to have more control over introspection on a single GQL API level.
</details>
</li>
<li>
<details>
<summary>Enhanced handling of arrays of objects in OpenAPI Documents</summary>

The Tyk Dashboard API endpoint */api/data-graphs/data-sources/import* now handles OAS schemas with arrays of objects. This addition means users can now import more complex OAS documents and transform them into UDG configurations.
</details>
</li>
<li>
<details>
<summary>Improved handling of unnamed object definitions in OpenAPI Documents</summary>

OAS converter can now create GraphQL types even if an object definition doesn’t have an explicit name.
</details>
</li>
<li>
<details>
<summary>Refined handling of arrays of objects in endpoint responses by OAS-to-UDG Converter</summary>

The OAS-to-UDG converter was unable to handle a document properly if an object within the OpenAPI Specification (OAS) had no properties defined. This limitation resulted in unexpected behaviour and errors during the conversion process. The tool will now handle such cases seamlessly, ensuring a smoother and more predictable conversion process.
</details>
</li>
<li>
<details>
<summary>OAS converter does not handle enums</summary>

Previously OAS-to-UDG converter had limitations in handling enums from OAS documents, leading to discrepancies and incomplete conversions. With the inclusion of enum support, the OAS converter now seamlessly processes enums defined in your OpenAPI Specifications, ensuring accurate and complete conversion to GraphQL schemas.
</details>
</li>
<li>
<details>
<summary>Implement KV store for API Definition fields</summary>

Implemented storage for all `string` type APIDefinition fields in separate KV storage, supporting environment variable, Tyk configuration file, Consul and Vault stores.
</details>
</li>
<li>
<details>
<summary>Expanded handling of HTTP Status Code ranges by OAS-to-GQL converter</summary>

OAS-to-UDG converter can now handle HTTP status code ranges that are defined by the OAS specification. This means that code ranges defined as 1XX, 2XX, etc will be correctly converted by the tool.
</details>
</li>
<li>
<details>
<summary>Support Redis v7.0.x</summary>

Tyk 5.3 refactors Redis connection logic by using [storage v1.2.2](https://github.com/TykTechnologies/storage/releases/tag/v1.2.2), which integrates with [go-redis](https://github.com/redis/go-redis) v9. Subsequently, Tyk 5.3 supports Redis v7.0.x.
</details>
</li>
</ul>

#### Changed
<!-- This should be a bullet-point list of updated features. Explain:

- Why was the update necessary?
- How does the update benefit users?
- Link to documentation of the updated feature
- For OSS - Link to the corresponding issue if possible on GitHub to allow the users to see further info.

Each change log item should be expandable. The first line summarises the changelog entry. It should be then possible to expand this to reveal further details about the changelog item. This is achieved using HTML as shown in the example below. -->
<ul>
<li>
<details>
<summary>Remove `slug` from the Tyk OAS API Definition</summary>

Removed the unnecessary ‘slug’ field from the OAS API Definition and OAS API Designer
</details>
</li>


<li>
<details>
<summary>Set default MongoDB driver to mongo-go</summary>

Tyk uses `mongo-go` as the default MongoDB driver from v5.3. This provides support for MongoDB 4.4.x, 5.0.x, 6.0.x and 7.0.x. If you are using older MongoDB versions e.g. 3.x, please set MongoDB driver to `mgo`. [MongoDB supported versions]({{<ref "planning-for-production/database-settings/mongodb#supported-versions">}}) page provides details on how to configure MongoDB drivers in Tyk.
</details>
</li>


<li>
<details>
<summary>Prefetch session expiry information from MDCB to reduce API call duration in case Gateway is temporarily disconnected from MDCB</summary>

Previously, when operating in a slave configuration, the Tyk Gateway fetched session expiry information from the master layer the first time an API was accessed for a given organisation. This approach led to a significant issue: if the MDCB connection was lost, the next API consumption attempt would incur a long response time. This delay, typically around 30 seconds, was caused by the Gateway waiting for the session fetching operation to time out, as it tried to communicate with the now-inaccessible master layer.

<br>To mitigate this issue, the PR introduces a proactive fetching strategy. Now, the gateway fetches the session expiry information beforehand, while there is an active connection to MDCB. By doing so, it ensures that this data is already available locally in the event of an MDCB disconnection.

<br>This change significantly improves the API response time under MDCB disconnection scenarios. It eliminates the need for the Gateway to wait for a timeout when attempting to fetch session information from the master layer, thus avoiding the previous 30-second delay. This optimisation enhances the resilience and efficiency of Tyk Gateway in distributed environments.
</details>
</li>

</ul>
 
#### Fixed
<!-- This section should be a bullet point list that describes the issues fixed in the release. For each fixed issue explain:

- What problem the issue caused
- How was the issue fixed
- Link to (new) documentation created as a result of a fix. For example, a new configuration parameter may have been introduced and documented for the fix
- For OSS - Link to the corresponding issue if possible on GitHub to allow the users to see further info.

Each change log item should be expandable. The first line summarises the changelog entry. It should be then possible to expand this to reveal further details about the changelog item. This is achieved using HTML as shown in the example below. -->
<ul>
<li>
<details>
<summary>Enhanced Redis token management and Gateway efficiency</summary>

In this release, we fixed automated token trimming in Redis, ensuring efficient management of OAuth tokens by implementing a new hourly job within the Gateway and providing a manual trigger endpoint. 
</details>
</li>
<li>
<details>
<summary>Tyk Gateway validates RFC3339 Date-Time Formats</summary>

Tyk Gateway now validates RFC3330 date-time formats with Tyk OAS validate request middleware.
</details>
</li>
<li>
<details>
<summary>Inaccurate Distributed Rate Limiting (DRL) behavior on Gateway startup</summary>

Fixed an issue when using the Distributed Rate Limiter (DRL) where the Gateway did not apply any rate limit until a DRL notification was received. Now the rate of requests will be limited at 100% of the configured rate limit until the DRL notification is received, after which the limit will be reduced to an even share of the total (i.e. 100% divided by the number of Gateways) per the rate limit algorithm design.
</details>
</li>
<li>
<details>
<summary>Duplicate fields added by OAS-to-GQL translator</summary>

Fixed an issue where the OAS-to-UDG converter was sometimes adding the 5.same field to an object type many times. This caused issues with the resulting GQL schema and made it non-compliant with GQL specification.
</details>
</li>
<li>
<details>
<summary>Gateway issue processing queries with GQL Engine</summary>

Fixed an issue where the Gateway attempted to execute a query with GQL engine version 1 (which lacks OTel support), while simultaneously trying to validate the same query with the OpenTelemetry (OTel) supported engine. It caused the API to fail with an error message "Error socket hang up". Right now with OTel enabled, the gateway will enforce GQL engine to default to version 2, so that this problem doesn't occur anymore.
</details>
</li>
<li>
<details>
<summary>Handling arrays of objects in endpoint responses by OAS/UDG converter</summary>

The OAS/UDG converter now effectively handles array of objects within POST paths. Previously, there were instances where the converter failed to accurately interpret and represent these structures in the generated UDG configuration.
</details>
</li>
<li>
<details>
<summary>Playground issues in Cloud/K8s deployments</summary>

An issue was identified where the encoding from the GQL upstream cache was causing readability problems in the response body. Specifically, the upstream GQL cache was utilizing brotli compression and not respecting the Accept-Encoding header. Consequently, larger response bodies became increasingly unreadable for the GQL engine due to compression, leading to usability issues for users accessing affected content. The issue has now been fixed by adding the brotli encoder to the GQL engine.
</details>
</li>
<li>
<details>
<summary>OAS Converter issue with "Json" Return Type</summary>

OAS-to-UDG converter was unable to correctly process OAS API definitions where "json" was used as one of enum values. This issue is now fixed and whenever "json" is used as one of enums in OAS, it will get correctly transformed into a custom scalar in GQL schema.
</details>
</li>
<li>
<details>
<summary>OAS Panic during API Edit with Virtual Endpoint middleware configured</summary>

Fixed an issue where the Gateway could panic while updating a Tyk OAS API with the Virtual Endpoint middleware configured.
</details>
</li>
<li>
<details>
<summary>Gateway panics during API Reload with JavaScript middleware bundle</summary>

Fixed an issue where reloading a bundle containing JS plugins could cause the Gateway to panic.
</details>
</li>
<li>
<details>
<summary>GraphQL introspection issue with Allow List</summary>

Fixed an issue where the *Disable introspection* setting was not working correctly in cases where field-based permissions were set (allow or block list). It was not possible to introspect the GQL schema while introspection was technically allowed but field-based permissions were enabled. Currently, Allow/Block list settings are ignored only for introspection queries and introspection is only controlled by the *Disable introspection* setting.
</details>
</li>
<li>
<details>
<summary>Handling of objects without properties in OAS-to-UDG converter</summary>

The OAS-to-UDG converter was unable to handle a document properly if an object within the OpenAPI Specification (OAS) had no properties defined. This limitation resulted in unexpected behavior and errors during the conversion process. The tool will now handle such cases seamlessly, ensuring a smoother and more predictable conversion process
</details>
</li>

</ul>


#### Security Fixes
<!-- This section should be a bullet point list that should be included when any security fixes have been made in the release, e.g. CVEs. For CVE fixes, consideration needs to be made as follows:
1. Dependency-tracked CVEs - External-tracked CVEs should be included on the release note.
2. Internal scanned CVEs - Refer to the relevant engineering and delivery policy.

For agreed CVE security fixes, provide a link to the corresponding entry on the NIST website. For example:

- Fixed the following CVEs:
    - [CVE-2022-33082](https://nvd.nist.gov/vuln/detail/CVE-2022-33082)
-->

#### Comunity Contributions
<!-- This section should thank external contributors and include a linked reference to their GitHub username with a summary of their contribution.

Example

Special thanks to the following member of the Tyk community for their contribution to this release:

<ul>
<li>
<details>
<summary>Runtime log error incorrectly produced when using Go Plugin Virtual Endpoints</summary>

Fixed a minor issue with Go Plugin virtual endpoints where a runtime log error was produced from a request, even if the response was successful. Thanks to ghub_user_tag_name for highlighting the issue and proposing a fix.
</details>
</li>
</ul>
-->

<!-- Required. use 3 hyphens --- between release notes of every patch (minors will be on a separate page) -->
---

<!--
Repeat the release notes section above for every patch here
-->


<!-- The footer of the release notes page. It contains a further information section with details of how to upgrade Tyk,
links to API documentation and FAQs. You can copy it from the previous release. -->
## Further Information

### Upgrading Tyk
Please refer to the [upgrading Tyk]({{< ref "upgrading-tyk" >}}) page for further guidance on the upgrade strategy.

### API Documentation
<!-- Required. Update the link to the Gateway "tyk-gateway-api" or dashboard "tyk-dashboard-api" and the Postman collection

If there were changes in any of Tyk’s API docs:

- Have API endpoints been documented in the release note summary and changelog?             
- Has a link to the endpoint documentation being included?
- Has the benefit of the new/updated endpoint been explained in the release highlights and changelog?
-->
- [OpenAPI Document]({{<ref "tyk-gateway-api/" >}})
- [Postman Collection](https://www.postman.com/tyk-technologies/workspace/tyk-public-workspace/overview)

### FAQ
Please visit our [Developer Support]({{< ref "frequently-asked-questions/faq" >}}) page for further information relating to reporting bugs, upgrading Tyk, technical support and how to contribute.
