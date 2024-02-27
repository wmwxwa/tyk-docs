---
title: "Upgrading Go Plugins On Cloud - SaaS"
date: 2024-02-6
tags: ["Upgrade plugins", "Tyk plugins", "SaaS", "Cloud"]
description: "Explains how to upgrade Go Plugins on Cloud SaaS"
---

## Upgrading your Cloud configuration

After reviewing your upgrade pre-requesites, follow the instructions below to upgrade your Tyk components and plugins. 

## Upgrading the Control Planes
 1. Log in to Cloud Provisioning Portal.
 2. Go to Control Plane (Dashboard) settings using the Edit Control Planes  instructions and scroll down to the Version section.
 3. Select a Bundle Channel.
 4. Next, select a Bundle Version.
 5. To apply your changes, click the “Save and Re-Deploy” button. After a few seconds, you will be redirected to the overview page of the Control Plane and a “Deploying” indicator button will appear.
 6. A “Deployed” button indicates a successful upgrade. 

## Upgrading Cloud Data Planes

 1.  Go to the Cloud Data Plane settings using the Edit Cloud Data Planes instructions and scroll down to the Version setting.
 2. Select a Bundle Channel.
 3. Next, select a Bundle Version. 
 4. To apply your changes, click the “Save and Re-Deploy” button. After a few seconds, you will be redirected to the overview page of the Control Plane and a “Deploying” indicator button will appear.
 5. A “Deployed” button indicates a successful upgrade. 



## Upgrading Custom Go Plugins

 | Path | Current Version | Target Version |
 | ---- | --------------- | -------------- |
 | 1    | < 4.1.0         | < 4.1.0        |
 | 2    | < 4.1.0         | \>= 4.1.0      |
 | 3    | \>= 4.1.0       | \>=5.1.0       |

- 

### Path 1 - Upgrading Go Plugins (Before Upgrading Tyk Gateway)
 1. Open a terminal/command prompt in the directory of your plugin source file(s)  
 2. Run the following commands to initialize your plugin:
 
 ```
 go get
 github.com/TykTechnologies/tyk@6c76e802a29838d058588ff924358706a078d0c5

 //Tyk Gateway versions < 4.2 have a dependency on graphql-go-tools
 go mod edit -replace github.com/jensneuse/graphql-go-tools=github.com/TykTechnologies/graphql-go-tools@v1.6.2-0.20220426094453-0cc35471c1ca

 go mod tidy
 go mod vendor
 ```
