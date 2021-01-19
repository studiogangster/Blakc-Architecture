## Chat *µService*:
After the user has recieved auth_token via Auth Service, he can comunicate with the Chat Service. Ideally, the user uses auth_token to initiate a handshake with WebSocket Server. 
Once connected, client can send & recieve messages.
```
Note: 
Websocket server will only broadcast new messages ingested after the client's commection was established & old messages are fetched via Management REST API Server. 
```  

### Components:
* Relay Service (Websocket Server)
* Management Service (REST API)
* Controller Service (gRPC Server)

### Tech stack
* Minio / s3 
* Message Broker (Kafka)
* Load Balancer (nginx)
<br>

### Chat Service Architecture:
<img src="./chat.svg">
<br>
<br>
## Relay Service (Websocket Server)
```
Programming Language:
NodeJS with microWebSockets (µWS)
```
```
A dumb client facing microservice, that maintains websocket connections with the client. The service will simply push recieved message to the Kafka (MQ).
It also maintains a pubsub based GRPC connection with `Controller Service`, and broadcasts messages recieved via it.
```
<br>
<br>

## Controller Service (gRPC Server)
<br>

```
Programming Language:
Golang + gRPC
```
```
Main task of controller service are:
1. Persist messages in DB
2. **Push only required message to the subscribed WebSocket server for broadcast
```
```
gRPC Server will act as a pub-sub, where WebSocket server can subscribe for new channel_ids (when a new client with a new channel_id connects). Controller will only publish the messages that belong to the subscribed channel_id, sabing ingress data, I/O, and CPU. 
```

## Message:
A message recieved from client goes through a series of parsing & transformation. A message when recieved from the client is validated with usual sanity checks (structure, expected fields, etc.). Later, authorization is validated (if sender is authorised to send message to the channel_id). Once validated, new server-side fields are embedded in it and is pushed to Message Broker.
<br>

### via Client
```
Sample Message recieved from client
{
    "channel_id": "", // team_id
    "to": "", // '*' -> All ,  'member_id' -> DM to a specific member 
    "type":"", // text, video, image, audio, file 
    "data": "", // message / media_attachment_id
}
```

* `channel_id`: A message can be sent to a team or personally to a team member (DM). channel_id is the team_id, as a team can only have one channel.  

* `to`: If the message is intended for group message, `*` is used, else `user_id` of the reciepient from the team (DM: Direct message) .

* `type`: Type of message:<br> `video` , `image`, `audio`, `file` , `text`

* `data`: <br>
`text` -> `data` contains text message (UTF-8 Encoded)
<br>
`video` , `image`, `audio`, `file` -> `data` will have attachment ID of the object stored in S3 / minio 


### Transformation
WebSocket server will transform the recieved message by adding few more required fields: 

1. from: Sender's user_id
2. ts: serverside Timestamp

```


{
    "channel_id": "", // team_id
    "to": "", // '*' -> All ,  'member_id' -> DM to a specific member 
    "type":"", // text, video, image, audio, file 
    "data": "", // message / media_attachment_id
    "ts": "", // timestamp
    "from": "" //Sender's userId of the client connected via websocket
}
```


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
















