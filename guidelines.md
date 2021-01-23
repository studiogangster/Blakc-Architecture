---
description: >-
  Below are the strict guidelines that must be followed by each developer while
  implementing services.
---

# Implementation Guidelines

## API Guidelines

While developing any REST API Service, following guidelines must be followed:

#### URI path should follow prefixed URI versioning pattern

**Example:**

`/v1/{route}/{to}/{an}/{endpoint}`

#### Authentication token `auth_token` must be passed in request's header.y

```text
POST /v1/hello-world HTTP/1.1
Host: api.blakc.xyz
Connection: keep-alive
sec-ch-ua: "Google Chrome";v="87", " Not;A Brand";v="99", "Chromium";v="87"
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 11_1_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.141 Safari/537.36
auth_token: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

#### The REST service and client app must honour common HTTP Status code, while responding

* 500: Unhandled Exception
* 403: Unauthorised \(Invalid .auth\_token \)
* 404: Unknown API endpoint
* 200: Successful completion of requested action

#### The REST service must follow the below JSON structure 

```javascript
{
status: true,
messsage: "Hi from the other side", // Error message to show, in case  'status' == false`
data: 
        {
                 // Requested Response
        }
}
```



## Websocket Service

Websocket service must follow below guidelines

#### Websocket reconnection strategy

Web-socket server can pile up stale sockets due to network congestion at server / client. If the connection stays ideal for a while \(no ping-pong messages\), the connection should forcefully be dropped, and client must reinitiate a new connection

#### Secured handshake.

On initial connection, the client must pass auth\_token in request header, and server must validate the token before establishing the connection. After successful handshake and authorisation, in-memory hash-map must store the userid till the connection lasts. For all the further transactions, the same user\_id  must be used for security purpose.

#### Message Broadcast

The messages broadcasted over websocket channel will only transfer new messages. A well choreographed use of REST Api & Websocket are used together, and bulk data \(like chat history\) is sent over HTTP request, and realtime messages & notifications are transferred over websocket.

**Multiplexing**

Single websocket connection is used for transferring messages \(from different teams, users, etc.\), notifications, etc. The message structure'd have provision to incorporate new message types, going forward.

 



## Frontend __ App

* Honour HTTP status code, and gracefully handle all possible edge cases.
* Frequent websocket connection can be expected, and such situations must be handled gracefully, with a robust retry mechanism

## Implementation Guidelines 

* Initial focus will be on close integration with the webservices, and provide a functional app with a dummy / wireframe design. 
* Since, each team can only have one channel for communication, a unique channel_id / team_ id should be used to as the unique identifier to send / receive messages
*  The client should use this channel\_id to subscribe to messages over websocket.
* The client will establish only one websocket connection with the server at a time, and multiplexing paradigm will be followed to receive messages from different team
* If the client creates/joins a new team, it should refresh the websocket connection and inform the relay server, to regather associated teams with the user from the database. Else, the user won't receive messages for the newly created/joined team.
* A team member should also be able to send DM to another team member. For such messages, same channel\_id along with an extra parameter should be used. Extra parameter can be random or derived from the both the clients participating in the DM chat.
* When the user get connected over websocket, only new messages are received viia websocket, while previously sent messages are synced in paginated manner via REST API.
* Websocket channel can also be used to inform about the new updates \(newly added team member, newly joined team, etc.\) using custom message type. Types of message may increase in future, so do ensure to make it easily extensible.  

 

#### 

