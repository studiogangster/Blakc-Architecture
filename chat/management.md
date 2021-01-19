## Team Management *µService*:

### Abbreviations:
**`:User`**
<br>
User fetched via auth token, interacting with the API
<br>
**`:auth_token`**
<br>
Auth token recieved after Authenticating vua Authentication µService

### Purpose:
This µService will be responsible for managing teams & channels.
All the endpoints will require `auth_token`, recieved via Authentication µService.
<br>
<br>
Team Management µService exposes a set of API endpoints that provides below functionalities:<br>

* Get Teams
    * `:User` is team creator
    * `:User` is team admin
    * `:User` is a team member
* Create Team
* Delete Team
* Modify Team: Change DP, teamname, alias, meta-data, etc.
* Add Team Member
* Remove Team Member
* Modify User Role



### Features:

* Get Teams: *(Fiters: multiple)*
    * User is team creator
    * User is team admin
    * User is a team member
* Create Team
* Delete Team
* Modify Team: Change DP, teamname, alias, meta-data, etc.
* Add Team Member
* Remove Team Member
* Modify User Role

### Dependencies:
* *Firebase*: For sign-up & sign-in integration
* *DB*: For storing user related data in 

### Story:
Once the user has logged in, `:auth_token` is used to consume Team-Management APIs. 
At the dashboard, user will fetch list of all the teams. 

### Team:
A team is a group of members, wherein users can broadcast and messages to others.

#### Attributes: ####
* Team Id: Unique id created at server (MongoDB Object id)
* Date Of Creation: Timestamp when the team was created
* Team Name
* Team Icon
* Active: (true,false)
* Meta Tags: Tags that can be used while searching
* Team Members: Array of unique user identifiers who are part of the team
* Team Admin: Array of unique user identifiers who are admin of the team
* Super Admin: Unqiue identifier of the user who created the team.
<br>
<br>
#### Sampe Document: ####
<br>

```
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

```
Note
A team can only have one creator.
```
#### User Roles: ####
* user: `Member of the team`
* admin: `Administrator of the team`
* super_admin: `Creator of the team`

#### Role's Privilege: ####
* user:
    *   Send / Recieve message to Team
    *   Send / Recieve message privately to a Team Member
    *   Leave Team

* admin:
    *   Send / Recieve message to Team
    *   Send / Recieve message privately to a Team Member
    *   Add Team Member (with user level)
    *   Remove Team Member (with user level)
    *   Leave Team

* super_admin:
    *   Send / Recieve message to Team
    *   Send / Recieve message privately to a Team Member
    *   Add Team Member (with user level)
    *   Remove Team Member (with user level)
    *   Elect any other user as an admin
    *   Remove any other user from admin list
    *   Leave Team


### Implementation Details:
* Programming language: Golang
* Framework: FastHTTP for API
* Versioning: Through URI (Eg: /{v1}/{route})

### Guidelines:
* Since, this service will be used extensively, performance & optimization should be considered from ground up while implementing functionality.
* All the parameters that vary for different env. (staging / productions) should be grabbed in via environment / config. file
* Every route must follow versioning pattern
* Authentication should be implemented as a middleware
* Logging mechanism 
* Use well defined JSON response structure  
* Honor HTTP Status Code (200, 403, 404, 500) 
* Proper error handling with logging, and custom error messages 

### Security Guidelines:
* Credentials should never be exposed in the logs
* No hardcoded tokens / credentials in the code
* No dynamic database query generation  
* Input sanitization  
















