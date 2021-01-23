---
description: 'Enhanced features, performance improvement & bug fixes'
---

# Phase V: Version 3

## Phase V: Version 3

### Tasks:

* `Realtime IM Service`:
  * Integration with different message types
  * S3 / minio API integration for providing pre-signed URL
  * Implement & use Redis for frequently used data from MongoDB
  * REST API for retrieving older messages 
  * Admin management
* `Web App`: 
  * UI Enhancement with new Screen for new features
  * Chat: DM, & Group Messaging over websocket
  * Chat: Upload, download & preview media attachments

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
* [ ] Send voice message \(explicit audio based media-content\)
* [ ] Search functionality for Chat messages

### Estimated Time:

**7 days**

### Release:

Version 0.3 will be released with few enhanced features, & bug fixes for QA.

