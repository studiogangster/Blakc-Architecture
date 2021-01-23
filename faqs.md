---
description: Enlisting questions that are expected from developers
---

# FAQs

## Minio vs S3 ?

We aim to build the app that can be deployed on any cloud vendor. Since, S3 restricts us to use AWS, minio is an open-source block storage that can be hosted easily in any infra. / cloud vendor. Also, minio & s3 use same API, and can work interchangeably.

## Why Golang / NodeJS ?

For CPU & IO intensive task, we opted for Golang

For IO only related tasks, NodeJS has been opted..

## Why Angular / React ?

The project is expected to grow, and release in phases. For maintaining modular code, and have access to tons of open source libraries, that might come handy.

Also, since IM chat apps follow reactive approach, RxJS can be leveraged.

## Why not club similar functionalities in a single microservice ?

Similar functionalities are already clubbed as a single microservice. Few of them might appear similar, but they are further segregated based on expected number of requests & the dependencies they have on other microservices / services \(DB, S3, etc.\)

## What is the actual role of Controller microservice in Messaging Service component ?

The .service is intended to only send those messages to the Relay Service, whose recipient are connected via websocket. In absence of this service, each relay service would subscribe to all the messages from all the different channels, while only few were required to be. This may lead to IO & CPU bottleneck, as each message is also required to be parsed before broadcasting it to clients.

Controller microservice aims to reduce CPU & IO at the client facing microservice \(Relay Service\). 

   





