---
title: Tyk Gateway 5.0 Release Notes
description: Tyk Gateway v5.0 release notes
tags: ["release notes", "Tyk Gateway", "v5.0", "5.0", "5.0.0", "5.0.1", "5.0.1", "5.0.2", "5.0.3", "5.0.4", "5.0.5", "5.0.6", "5.0.7", "5.0.8", "5.0.9", "5.0.10"]
aliases:
    - /release-notes/version-5.0/
---

**Open Source** ([Mozilla Public License](https://github.com/TykTechnologies/tyk/blob/master/LICENSE.md))

**This page contains all release notes for version 5.0.X displayed in reverse chronological order**

---
## Support Lifetime
<!-- Required. replace X.Y with this release and set the correct quarter of the year -->
Please add statement explaining when 5 LTS is supported until

---

## 5.0.11 Release Notes

### Release Date N April 2024

### Breaking Changes
<!-- Required. Use the following statement if there are no breaking changes, or explain if there are -->
**Attention: Please read this section carefully**

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

#### 3rd Party Dependencies & Tools (Please verify and check for 5.0.11 LTS)
<!-- Required. Third-party dependencies encompass tools (GoLang, Helm etc.), databases (PostgreSQL, MongoDB etc.) and external software libraries. This section should be a table that presents the third-party dependencies and tools compatible with the release. Compatible is used in the sense of those versions tested with the releases. Such information assists customers considering upgrading to a specific release.

Additionally, a disclaimer statement was added below the table, for customers to check that the third-party dependency they decide to install remains in support.

An example is given below for illustrative purposes only. Tested Versions and Compatible Versions information will require discussion with relevant squads and QA. -->

| Third Party Dependency                                       | Tested Versions        | Compatible Versions    | Comments | 
| ------------------------------------------------------------ | ---------------------- | ---------------------- | -------- | 
| [Go](https://go.dev/dl/)                                     | 1.19 (GQL), 1.21 (GW)  | 1.19 (GQL), 1.21 (GW)  | [Go plugins]({{< ref "plugins/supported-languages/golang" >}}) must be built using Go 1.21 | 
| [Redis](https://redis.io/download/)  | 6.2.x, 7.x  | 6.2.x, 7.x  | Used by Tyk Gateway | 
| [OpenAPI Specification](https://spec.openapis.org/oas/v3.0.3)| v3.0.x                 | v3.0.x                 | Supported by [Tyk OAS]({{< ref "tyk-apis/tyk-gateway-api/oas/x-tyk-oas-doc" >}}) |

Given the potential time difference between your upgrade and the release of this version, we recommend users verify the ongoing support of third-party dependencies they install, as their status may have changed since the release.

### Deprecations
<!-- Required. Use the following statement if there are no deprecations, or explain if there are -->

<!-- Optional section!
Used to share and notify users about our plan to deprecate features, configs etc. 
Once you put an item in this section, we must keep this item listed in all the following releases till the deprecation happens. -->
<!-- ##### Future deprecations
-->
There are no deprecations in this release.

### Upgrade instructions
If you are upgrading to 5.0.11, please follow the detailed [upgrade instructions](#upgrading-tyk).

### Release Highlights
<!-- Required. Use similar ToV to previous release notes. For example for a patch release:
This release primarily focuses on bug fixes.
For a comprehensive list of changes, please refer to the detailed [changelog]({{< ref "#Changelog-vX.Y.0">}}) below.
-->
Please add release highlights

### Downloads
- [Docker image to pull](https://hub.docker.com/r/tykio/tyk-gateway/tags?page=&page_size=&ordering=&name=v5.0.11)
  - ```bash
    docker pull tykio/tyk-gateway:v5.0.11
    ``` 
- Helm charts
  - [tyk-charts GH Repo](https://github.com/TykTechnologies/tyk-charts/releases)
- [Source code tarball for OSS projects](https://github.com/TykTechnologies/tyk/releases)

### Changelog {#Changelog-v5.0.11}
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
</ul>

#### Changed
<!-- This should be a bullet-point list of updated features. Explain:

- Why was the update necessary?
- How does the update benefit users?
- Link to documentation of the updated feature
- For OSS - Link to the corresponding issue if possible on GitHub to allow the users to see further info.

Each change log item should be expandable. The first line summarises the changelog entry. It should be then possible to expand this to reveal further details about the changelog item. This is achieved using HTML as shown in the example below. -->
<ul>
</ul>
 
#### Fixed
<!-- This section should be a bullet point list that describes the issues fixed in the release. For each fixed issue explain:

- What problem the issue caused
- How was the issue fixed
- Link to (new) documentation created as a result of a fix. For example, a new configuration parameter may have been introduced and documented for the fix
- For OSS - Link to the corresponding issue if possible on GitHub to allow the users to see further info.

Each change log item should be expandable. The first line summarises the changelog entry. It should be then possible to expand this to reveal further details about the changelog item. This is achieved using HTML as shown in the example below. -->
<ul>
</ul>


#### Security Fixes
<!-- This section should be a bullet point list that should be included when any security fixes have been made in the release, e.g. CVEs. For CVE fixes, consideration needs to be made as follows:
1. Dependency-tracked CVEs - External-tracked CVEs should be included on the release note.
2. Internal scanned CVEs - Refer to the relevant engineering and delivery policy.

For agreed CVE security fixes, provide a link to the corresponding entry on the NIST website. For example:

- Fixed the following CVEs:
    - [CVE-2022-33082](https://nvd.nist.gov/vuln/detail/CVE-2022-33082)
-->

<ul>
</ul>

<!-- Required. use 3 hyphens --- between release notes of every patch (minors will be on a separate page) -->
---

## 5.0.10 Release Notes
Please refer to our GitHub [release notes](https://github.com/TykTechnologies/tyk/releases/tag/v5.0.10).

---

## 5.0.9 Release Notes
Please refer to our GitHub [release notes](https://github.com/TykTechnologies/tyk/releases/tag/v5.0.9).

---

## 5.0.8 Release Notes
Please refer to our GitHub [release notes](https://github.com/TykTechnologies/tyk/releases/tag/v5.0.8).

---

## 5.0.7 Release Notes
Please refer to our GitHub [release notes](https://github.com/TykTechnologies/tyk/releases/tag/v5.0.7).

---

## 5.0.6 Release Notes
Please refer to our GitHub [release notes](https://github.com/TykTechnologies/tyk/releases/tag/v5.0.6).

---

## 5.0.5 Release Notes
Please refer to our GitHub [release notes](https://github.com/TykTechnologies/tyk/releases/tag/v5.0.5).

---

## 5.0.4 Release Notes
Please refer to our GitHub [release notes](https://github.com/TykTechnologies/tyk/releases/tag/v5.0.4).

---

## 5.0.3 Release Notes
Please refer to our GitHub [release notes](https://github.com/TykTechnologies/tyk/releases/tag/v5.0.3).

---

## 5.0.2 Release Notes

##### Release Date 29 May 2023

#### Release Highlights

This release primarily focuses on bug fixes. 
For a comprehensive list of changes, please refer to the detailed [changelog]({{< ref "#Changelog-v5.0.2">}}) below.

#### Downloads

- [docker image to pull](https://hub.docker.com/layers/tykio/tyk-gateway/v5.0.2/images/sha256-5e126d64571989f9e4b746544cf7a4a53add036a68fe0df4502f1e62f29627a7?context=explore) 
- [source code](https://github.com/TykTechnologies/tyk/releases/tag/v5.0.2)

#### Changelog {#Changelog-v5.0.2}

##### Updated
- Internal refactoring to make storage related parts more stable and less affected by potential race issues

---

## 5.0.1 Release Notes

##### Release Date 25 Apr 2023

#### Release Highlights
This release primarily focuses on bug fixes. 
For a comprehensive list of changes, please refer to the detailed [changelog]({{< ref "#Changelog-v5.0.1">}}) below.

#### Downloads
- [docker image to pull](https://hub.docker.com/layers/tykio/tyk-gateway/v5.0.1/images/sha256-5fa7aa910d62a7ed2c1cfbc68c69a988b4b0e9420d7a52018f80f9a45cadb083?context=explore
- [source code](https://github.com/TykTechnologies/tyk/releases/tag/v5.0.1)

#### Changelog {#Changelog-v5.0.1}

##### Added
- Added a new `enable_distributed_tracing` option to the NewRelic config to enable support for Distributed Tracer

##### Fixed
- Fixed  panic when JWK method was used for JWT authentication and the token didn't include kid
- Fixed an issue where failure to load GoPlugin middleware didn’t prevent the API from proxying traffic to the upstream: now Gateway logs an error when the plugin fails to load (during API creation/update) and responds with HTTP 500 if the API is called; at the moment this is fixed only for file based plugins
- Fixed MutualTLS issue causing leak of allowed CAs during TLS handshake when there are multiple mTLS APIs
- Fixed a bug during hot reload of Tyk Gateway where APIs with JSVM plugins stored in filesystem were not reloaded
- Fixed a bug where the gateway would remove the trailing `/`at the end of a URL
- Fixed a bug where nested field-mappings in UDG weren't working as intended
- Fixed a bug when using Tyk OAuth 2.0 flow on Tyk Cloud where a request for an Authorization Code would fail with a 404 error
- Fixed a bug where mTLS negotiation could fail when there are a large number of certificates and CAs; added an option (`http_server_options.skip_client_ca_announcement`) to use the alternative method for certificate transfer
- Fixed CVE issue with go.uuid package
- Fixed a bug where rate limits were not correctly applied when policies are partitioned to separate access rights and rate limits into different scopes

---

## 5.0.0 Release Notes

##### Release Date 28 Mar 2023

#### Deprecations
- Tyk Gateway no longer natively supports **LetsEncrypt** integration. You still can use LetsEncrypt CLI tooling to generate certificates and use them with Tyk.

#### Release Highlights

##### Improved OpenAPI support

We have added some great features to the Tyk OAS API definition bringing it closer to parity with our Tyk Classic API and to make it easier to get on board with Tyk using your Open API workflows.

Tyk’s OSS users can now make use of extensive [custom middleware](https://tyk.io/docs/plugins/) options with your OAS APIs, to transform API requests and responses, exposing your upstream services in the way that suits your users and internal API governance rules. We’ve enhanced the Request Validation for Tyk OAS APIs to include parameter validation (path, query, headers, cookie) as well as the body validation that was introduced in Tyk 4.1.

[Versioning your Tyk OAS APIs]({{< ref "getting-started/key-concepts/oas-versioning" >}}) is easier than ever, with the Tyk OSS Gateway now looking after the maintenance of the list of versions associated with the base API for you; we’ve also added a new endpoint on the Tyk API that will return details of the versions for a given API.

We’ve improved support for [OAS Mock Responses]({{< ref "product-stack/tyk-gateway/middleware/mock-response-middleware" >}}), with the Tyk OAS API definition now allowing you to register multiple Mock Responses in a single API, providing you with increased testing flexibility.

Of course, we’ve also addressed some bugs and usability issues as part of our ongoing ambition to make Tyk OAS API the best way for you to create and manage your APIs.

Thanks to our community contributors [armujahid](https://github.com/armujahid), [JordyBottelier](https://github.com/JordyBottelier) and [ls-michal-dabrowski](https://github.com/ls-michal-dabrowski) for your PRs that further improve the quality of Tyk OSS Gateway!

#### Downloads

- [docker image to pull](https://hub.docker.com/layers/tykio/tyk-gateway/v5.0.0/images/sha256-196815adff2805ccc14c267b14032f23913321b24ea86c052b62a7b1568b6725?context=explore)
- [source code](https://github.com/TykTechnologies/tyk/releases/tag/v5.0.0)

#### Changelog {#Changelog-v5.0.0}

##### Added
- Support for request validation (including query params, headers and the rest of OAS rules) with Tyk OAS APIs
- Transform request/response middleware for Tyk OAS APIs
- Custom middleware for Tyk OAS APIs
- Added a new API endpoint to manage versions for Tyk OAS APIs
- Improved Mock API plugin for Tyk OAS APIs
- Universal Data Graph and GraphQL APIs now support using context variables in request headers, allowing passing information it to your subgraphs
- Now you can control access to introspection on policy and key level

#### Fixed
- Fixed potential race condition when using distributed rate limiter

---

## Further Information

### Upgrading Tyk
Please refer to the [upgrading Tyk]({{< ref "upgrading-tyk" >}}) page for further guidance with respect to the upgrade strategy.

### API Documentation

- [OpenAPI Document]({{<ref "tyk-dashboard-api">}})
- [Postman Collection](https://www.postman.com/tyk-technologies/workspace/tyk-public-workspace/collection/27225007-374cc3d0-f16d-4620-a435-68c53553ca40)

### FAQ
Please visit our [Developer Support]({{< ref "frequently-asked-questions/faq" >}}) page for further information relating to reporting bugs, upgrading Tyk, technical support and how to contribute.
