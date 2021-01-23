---
description: >-
  Blakc follows layered microservices architecture. This not only makes it
  easier to develop resilient & scalable app, but will also allow individual
  contributors to develop delegated tasks in parallel
---

# Architecture

## Components

Each component may have one or more microservices. Each microservice will have pre-determined controlled & only the required access to other resources \(DB, S3, peer services, etc.\)

## Core components:

* Authentication Service
* Messaging Service
* Team Management Service
* Storage Service
* Web App \(Frontend App\)

> #### Note: 
>
> Each component's individual architecture & functionality is described in detail, in the later section.

## Component's Overview

_Bird's eye view of all the components, services and the connectivity between them_

![Component&apos;s overview and connectivity diagram](../.gitbook/assets/components.png)

![Auth. Service Architecture](../.gitbook/assets/authentication.svg)

{% hint style="info" %}
Each component is explained in details in the subsection.
{% endhint %}

![Messaging Service Architecture](../.gitbook/assets/chat.png)

{% hint style="info" %}
**Redis** will be used by almost all the microservices, and is not depicted explicitly in the architecture diagrams. Whenever cache is referred, it'd mean **Redis** and not in-memory cache, until stated explicitly.  **** 
{% endhint %}

