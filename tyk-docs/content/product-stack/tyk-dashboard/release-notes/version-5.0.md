---
title: Tyk Dashboard v5.0
tags: ["release notes", "Tyk Dashboard", "v5.0", "5.0", "5.0.0", "5.0.1", "5.0.1", "5.0.2", "5.0.3", "5.0.4", "5.0.5", "5.0.6", "5.0.7", "5.0.8", "5.0.9", "5.0.10", "5.0.11"]
weight: 2
---

**Licensed Protected Product**

**This page contains all release notes for version 5.0.X displayed in reverse chronological order**

---
## Support Lifetime
<!-- Required. replace X.Y with this release and set the correct quarter of the year -->
Please add statement explaining when 5.0.11 is supported until

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

### Downloads
- [Docker image to pull](https://hub.docker.com/r/tykio/tyk-dashboard/tags?page=&page_size=&ordering=&name=v5.0.11)
  - ```bash
    docker pull tykio/tyk-dashboard:v5.0.11
    ``` 
- Helm charts
  - [tyk-charts GH Repo](https://github.com/TykTechnologies/tyk-charts/releases)

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
Please refer to our GitHub [release notes](https://github.com/TykTechnologies/tyk/releases/tag/v5.0.10)

---

## 5.0.9 Release Notes
Please refer to our GitHub [release notes](https://github.com/TykTechnologies/tyk/releases/tag/v5.0.9)

---

## 5.0.8 Release Notes
Please refer to our GitHub [release notes](https://github.com/TykTechnologies/tyk/releases/tag/v5.0.8)

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

##### Support for MongoDB 5 and 6
From Tyk 5.0.2, we added support for MongoDB 5.0.x and 6.0.x. To enable this, you have to set new Dashboard config option driver to *mongo-go*. 
The driver setting defines the driver type to use for MongoDB. It can be one of the following values:
- [mgo](https://github.com/go-mgo/mgo) (default): Uses the *mgo* driver. This driver supports MongoDB versions <= v4.x (lower or equal to v4.x). You can get more information about this driver in the [mgo](https://github.com/go-mgo/mgo) GH repository. To allow users more time for migration, we will update our default driver to the new driver, *mongo-go*, in next major release.
- [mongo-go](https://github.com/mongodb/mongo-go-driver): Uses the official MongoDB driver. This driver supports MongoDB versions >= v4.x (greater or equal to v4.x). You can get more information about this driver in [mongo-go-driver](https://github.com/mongodb/mongo-go-driver) GH repository.

See how to [Choose a MongoDB driver]({{< ref "planning-for-production/database-settings/mongodb#choose-a-mongodb-driver" >}})

**Note: Tyk Pump 1.8.0 and MDCB 2.2 releases have been updated to support the new driver option**

#### Downloads

[docker image to pull](https://hub.docker.com/layers/tykio/tyk-dashboard/v5.0.2/images/sha256-fe3009c14ff9096771d10995a399a494389321707e951a3c46f944afd28d18cd?context=explore)


#### Changelog {#Changelog-v5.0.2}

##### Fixed
- Fixed a bug on migration of a portal catalogue with deleted policy to SQL
- Fixed: Redirect unregistered user to new page when SSOOnlyForRegisteredUsers is set to true

---

## 5.0.1 Release Notes

##### Release Date 25 Apr 2023

#### Release Highlights
This release primarily focuses on bug fixes. 
For a comprehensive list of changes, please refer to the detailed [changelog]({{< ref "#Changelog-v5.0.1">}}) below.

#### Downloads
- [docker image to pull](https://hub.docker.com/layers/tykio/tyk-dashboard/v5.0.1/images/sha256-013d971fc826507702f7226fa3f00e1c7e9d390fc0fb268bed42e410b126e89d?context=explore)

#### Changelog {#Changelog-v5.0.1}

##### Added
- Improved security for people using the Dashboard by adding the Referrer-Policy header with the value `no-referrer`
- Added ability to select the plugin driver within the Tyk OAS API Designer

##### Changed
- When creating a new API in the Tyk OAS API Designer, caching is now disabled by default

##### Fixed
- Fixed a bug where a call to the `/hello` endpoint would unnecessarily log `http: superfluous response.WriteHeader call`
- Fixed a bug where the Dashboard was showing *Average usage over time* for all Developers, rather than just those relevant to the logged in developer
- Fixed a bug where logged in users could see Identity Management pages, even if they didn't have the rights to use these features
- Fixed a bug that prevented Tyk Dashboard users from resetting their own passwords
- Fixed issue with GraphQL proxy headers added via UI
- Fixed a bug where the Dashboard would not allow access to any screens if a logged in user didn’t have access to the APIs resource regardless of other access rights
- Fixed a bug on the key management page where searching by `key_id` did not work - you can now initiate the search by pressing enter after typing in the `key_id`
- Fixed a bug where Dashboard API could incorrectly return HTTP 400 when deleting an API
- Fixed UDG UI bug that caused duplicate data source creation on renaming
- Fixed schema validation for custom domain in Tyk OAS API definition
- Fixed a bug where the left menu did not change when Dashboard language was changed
- Fixed a bug that caused the Dashboard to report errors when decoding multiple APIs associated with a policy
- Fixed a bug where it was not possible to disable the Use Scope Claim option when using JWT authentication
- Fixed a bug in the default OPA rule that prevented users from resetting their own password
- Fixed a bug where authToken data was incorrectly stored in the JWT section of the authentication config when a new API was created

---

## v5.0.0 Release Notes

##### Release Date 28 Mar 2023

#### Release Highlights

##### Improved OpenAPI support

Tyk Dashboard has been enhanced with **all the custom middleware options** for Tyk OAS APIs, so **for the first time** you can configure your custom middleware from the Dashboard; this covers the full suite of custom middleware from pre- to post- and response plugins. We’ve got support for middleware bundles, Go plugins and Tyk Virtual Endpoints, all within the new and improved Tyk Dashboard UI.

[Versioning your Tyk OAS APIs]({{< ref "getting-started/key-concepts/oas-versioning" >}}) is easier than ever, with the Tyk OSS Gateway now looking after the maintenance of the list of versions associated with the base API for you; we’ve also added a new endpoint on the Tyk API that will return details of the versions for a given API.

Tyk Dashboard hasn’t been left out, we’ve implemented a brand new version management UI for Tyk OAS APIs, to make it as easy as possible for you to manage those API versions as you develop and extend your API products with Tyk.

We’ve improved support for [OAS Mock Responses]({{< ref "product-stack/tyk-gateway/middleware/mock-response-middleware" >}}), with the Tyk OAS API definition now allowing you to register multiple Mock Responses in a single API, providing you with increased testing flexibility.

Another new feature in the Tyk OAS API Designer is that you can now update (PATCH) your existing Tyk OAS APIs through the Dashboard API without having to resort to curl. That should make life just that little bit easier.
Of course, we’ve also addressed some bugs and usability issues as part of our ongoing ambition to make Tyk OAS API the best way for you to create and manage your APIs.

##### GraphQL and Universal Data Graph improvements

This release is all about making things easier for our users with GraphQL and Universal Data Graph.

In order to get our users up and running with a working Universal Data Graph quickly, we’ve created a repository of examples that anyone can import into their Dashboard or Gateway and see what Universal Data Graph is capable of. Import can be done in two ways:
- manually, by simply copying a Tyk API definition from GitHub - [TykTechnologies/tyk-examples](https://TykTechnologies/tyk-examples): A repository containing example API definitions and policies for Tyk products. 
- via command line [using tyk-sync]({{< ref "universal-data-graph/udg-examples" >}})

To make it easier for our users to find their way to Universal Data Graph, we’ve also given it its own space in the Dashboard. From now on you can find UDG under Data Graphs section of the menu.

It also got a lot easier to turn a Kafka topic into a GraphQL subscription. Using our new Dashboard API endpoint, users will be able to transform their AsyncAPI documentation into Universal Data Graph definition with a single click. Support for OAS coming soon as well!

With this release we are also giving our users [improved headers for GQL APIs]({{< ref "graphql/gql-headers" >}}). It is now possible to use context variables in request headers and persist headers needed for introspection separately for improved security.

Additionally we’ve added Dashboard support for introspection control on policy and key level. It is now possible to allow or block certain consumers from being able to introspect any graph while creating a policy or key via Dashboard.

#### Downloads

[docker image to pull](https://hub.docker.com/layers/tykio/tyk-dashboard/v5.0/images/sha256-3d736b06b023e23f406b1591f4915b3cb15a417fcb953d380eb8b4d71829f20f?tab=vulnerabilities)

#### Changelog {#Changelog-v5.0.0}

##### Added
- Numerous UX improvements
- New UI for custom middleware for Tyk OAS APIs
- Significantly improved Tyk OAS API versioning user experience
- It now possible to use PATCH method to modify Tyk OAS APIs via the Dashboard API
- Now you can turn a Kafka topic into a GraphQL subscription by simply [importing your AsyncAPI definition]({{< ref "tyk-apis/tyk-dashboard-api/data-graphs-api" >}})
- Way to control access to introspection on policy and key level

##### Changed
- Universal Data Graph moved to a separate dashboard section

---

## Further Information

### Upgrading Tyk
Please refer to the [upgrading Tyk]({{< ref "upgrading-tyk" >}}) page for further guidance with respect to the upgrade strategy.

### API Documentation

- [OpenAPI Document]({{<ref "tyk-dashboard-api">}})
- [Postman Collection](https://www.postman.com/tyk-technologies/workspace/tyk-public-workspace/collection/27225007-374cc3d0-f16d-4620-a435-68c53553ca40)

### FAQ
Please visit our [Developer Support]({{< ref "frequently-asked-questions/faq" >}}) page for further information relating to reporting bugs, upgrading Tyk, technical support and how to contribute.
