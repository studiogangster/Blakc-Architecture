# Blakc-Architecture

# Overview

# Features
The end product is expected to ship with below features

### Authentication
- [x] Sign Up
- [x] Login

### Team Management
- [x] Create Team
- [x] Delete Team
- [x] Modify Team Details
- [x] Add Team Member
- [x] Remove Team Member
- [x] Add admin
- [x] Remove admin
- [x] Change team owner (Transfer ownership)
- [x] Deactivate Team (Disable messaging)

### Realtime Instant Messaging
- [x] Send text message in team channel (GM: Group Message)
- [x] Send media content in team channel (GM: Group Message)
- [x] Send text-message directly to a team member (DM: Direct Message)
- [x] Send media-content directly to a team member (DM: Direct Message)
- [x] Retrieve Chat history from team' channel
- [x] Retrieve Chat history from DM
- [x] Send voice message (explicit audio based media-content)
- [x] Search functionality for Chat messages



# Technology Stack
* Database: MongoDB
* Message Broker: Kafka
* Cache: Redis
* Storage: minio for production
```Note:
The techstack is selected while keeping in mind, not to have any explicit dependency on cloud / infrastructure vendor, so that deployment or migration can be done without any hassle.  
```

# Architecture
```
`Blakc` follows layered microservices architecture. This not only makes it easier to develop resillient & scalable app, but will also allow individual controbutors to develop delegated task parallely, reducing time to ship and faster development.
Each latyer in the architecture can easily be scaled horizontally, making it easy to avoid any bottleneck.
```

# Components




