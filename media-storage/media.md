## Media Storage *µService*:

### Overview:
Minio storage exposes S3 compatible API that will be used to store media content:
* Images 
* Videos
* Document
* Audio Clip
* File Attachment
<br>
<br>

### Details:

Whenever a client wants to send media content, the client issues an API request with meta-data (content-type, size, name, meta-data, etc.) of the attachment, and a pre-signed URL of S3 Object is requested from the server. Later, the client uploads the content on the recieved pre-signed URL, and sends the attachment-id over channel to as a part of message.

### Dependencies:
* *S3/Minio*: Block storage

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
* For upload request, pre-signed URL will be used and no direct access to S3 bucket should be exposed to client
* When downloading media-content, pre-signed URL will be issues only after verifying that the content is meant to be accessible by the requestee. (If the user is a member of the team / channel, where the mediacontent was posted).
* Configurable TTL / Expiry time of the URL
* No hard coded credentials (s3 keys & tokens)
















