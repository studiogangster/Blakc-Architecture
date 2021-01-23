---
description: A microservice exposing a REST API web server to manage team & members
---

# Team Management Service

## Overview:

Management Service is a REST API server, that authenticates the user via `auth_oken` \(received via Authentication Service\), and validates if the user is authorised to perform the action. An action could be: 

* Create Team
* Get Teams
* Delete Team
* Modify Team: Change Display Picture, Team name, alias, meta-data, etc.
* Add Team Member
* Remove Team Member
* Modify User Role

## Storyboard

Once the user has logged in, `:auth_token` is used to consume Team-Management APIs. At the dashboard, user will fetch list of all the teams, and use the channel\_id to .

{% hint style="info" %}
#### Abbreviations:

**`:User`**   
 User fetched via auth token, interacting with the API   
 **`:auth_token`**   
 Auth token received after Authenticating from Authentication µService
{% endhint %}

## Tasks

This µService will be responsible for managing teams & channels. All the endpoints will require `auth_token`, received via Authentication µService.   
   
 Team Management µService exposes a set of API endpoints that provides below functionalities:  


* [x] Get Teams
  * `:User` is team creator
  * `:User` is team admin
  * `:User` is a team member
* [x] Create Team
* [x] Delete Team
* [x] Modify Team: Change DP, teamname, alias, meta-data, etc.
* [x] Add Team Member
* [x] Remove Team Member
* [x] Modify User Role



## Features:

* Get Teams: _\(**Filters**: multiple\)_
  * User is team creator
  * User is team admin
  * User is a team member
* Create Team
* Delete Team
* Modify Team: Change DP, teamname, alias, meta-data, etc.
* Add Team Member
* Remove Team Member
* Modify User Role

## Dependencies:

* **Firebase**: For sign-up & sign-in integration
* **DB \(MongoDB\)**: For storing user related data

## Data Models

### Team

A team is a group of members, wherein users can broadcast and messages to others.

#### Attributes

* Team Id: Unique id created at server \(MongoDB Object id\)
* Date Of Creation: Timestamp when the team was created
* Team Name
* Team Icon
* Active: \(true, false\)
* Meta Tags: Tags that can be used while searching
* Team Members: Array of unique user identifiers who are part of the team
* Team Admin: Array of unique user identifiers who are admin of the team
* Super Admin: Unique identifier of the user who created the team.

#### **Sample Document**

```javascript
{
    "id": "507f191e810c19729de860ea", 
    "name": "Test Team Name",
    "icon": "uri-to-icon",
    "active": true,
    "meta_tags": ["awesome-team", "team-hello-world", "test"],
    "members": [ "prakhar@black.dev", "test@black.dev" ],
    "admins": [ "prakhar@black.dev" ],
    "super_admin": "prakhar@black.dev",
    "doc": "Mon, 18 Jan 2021 01:48:42 GMT"
}
```

{% hint style="info" %}
**Note** A team can only have one creator.
{% endhint %}

### User Roles

Any logged in user can have one of the below roles for a team:

* user: `Member of the team`
* admin: `Administrator of the team`
* super\_admin: `Creator of the team`

### User's Privilege

* user:
  * Send / Receive message to Team
  * Send / Receive message privately to a Team Member
  * Leave Team
* admin:
  * Send / Receive message to Team
  * Send / Receive message privately to a Team Member
  * Add Team Member \(with user level\)
  * Remove Team Member \(with user level\)
  * Leave Team
* super\_admin:

  * Send / Receive message to Team
  * Send / Receive message privately to a Team Member
  * Add Team Member \(with user level\)
  * Remove Team Member \(with user level\)
  * Elect any other user as an admin
  * Remove any other user from admin list
  * Leave Team

  \*\*\*\*

## **Implementation Details:**

* Programming language: **Golang**
* Framework: **FastHTTP** for REST API Server
* Versioning: through URI \(Eg: **/{v1}/{route}**\)



## Guidelines:

* Since, this service will be used extensively, performance & optimisations should be considered from ground up while implementing functionality.
* All the parameters that vary for different env. \(staging / productions\) should be grabbed in via environment / config. file
* Every route must follow versioning pattern
* Authentication should be implemented as a middleware
* Logging mechanism 
* Use well defined JSON response structure  
* Honor HTTP Status Code \(200, 403, 404, 500\) 
* Proper error handling with logging, and custom error messages 

## Security Guidelines:

* Credentials should never be exposed in the logs
* No hardcoded tokens / credentials in the code
* No dynamic database query generation  
* Input Sanitisation  

