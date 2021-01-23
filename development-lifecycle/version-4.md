---
description: 'Major change: Record & send voice messages with performance impr. & bug fixes'
---

# Phase VI: Version 4

## Phase VI: Version 4

### Tasks:

* `Realtime IM Service`:
  * Chat caching engine: Archive chat from MongoDB to s3 bucket
  * REST API: Retrieve chat from s3 & fallback to MongoDB
  * Purge duplicate chat history from DB
* `Web App`: 
  * Implement: record & send voice messages
  * Preview / Play recieved recorded messages
  * Integrate UI designs & screens

### Released Features:

#### Authentication

* [x] Sign Up
* [x] Login

#### Team Management

* [x] Create Team
* [x] Delete Team
* [x] Modify Team Details
* [x] Add Team Member
* [x] Remove Team Member
* [x] Add admin
* [x] Remove admin
* [x] Change team owner \(Transfer ownership\)
* [x] Deactivate Team \(Disable messaging\)

#### Realtime Instant Messaging

* [x] Send text message in team channel \(GM: Group Message\)
* [x] Send media content in team channel \(GM: Group Message\)
* [x] Send text-message directly to a team member \(DM: Direct Message\)
* [x] Send media-content directly to a team member \(DM: Direct Message\)
* [x] Retrieve Chat history from team channel
* [x] Retrieve Chat history from DM
* [x] Send voice message \(explicit audio based media-content\)
* [x] Search functionality for Chat messages

### Estimated Time:

**7 days**

### Release:

Version 0.4 will be released with few enhanced features, & bug fixes for QA.

