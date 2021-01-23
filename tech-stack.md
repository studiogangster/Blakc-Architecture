---
description: >-
  Exhaustive list of all the technology components that will be used during the
  design & development of product
---

# Technology Stack

## Components

{% hint style="info" %}
The techstack was finalised, keeping in mind, not to have any explicit dependency on a particular cloud / infrastructure vendor, so as to make deployment / migration hassle free in near future.
{% endhint %}

* Database: **MongoDB**
* Message Broker: **Kafka**
* oAuth & SSO: **Firebase**
* Cache: **Redis**
* Storage: **minio / S3**
* Programming Languages:
  * Backend µServices: **NodeJS** & **GoLang**
  * Frontend Webapp: **Angular** / **React**
* Packaging & Bundling:
  * **Docker image** for Backend  µServices
  * **S3** to host Frontend App \(static files\)
* Source Code Management: **Github**

{% hint style="info" %}
**minio** & **s3** are used interchangeably. Since,  S3 restricts us to use AWS, minio is an open-source block storage that can be hosted easily in any infra. / cloud vendor. Also, minio & s3 use same API, and can work interchangeably.
{% endhint %}



{% hint style="info" %}
**Redis** will be used by almost all the microservices, and is not depicted explicitly in the architecture diagrams & document. Whenever cache is referred, it'd mean  **Redis** and not in-memory cache, until stated explicitly.  **** 
{% endhint %}

