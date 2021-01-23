# Deployment Plan

## Plan of action

* Web app will be hosted on the parent domain @ blakc.xyz
* Public facing services will be hosted in delegated subdomains 
  * auth.blakc.xyz
  * chat.blaks.xyz
  * manage.blakc.xyz
  * storage.blakc.xyz
  * api.blakk.xyz
* For test & QC environment, all the above services will be prefixed with slug and an hyphen
  * stage
  * qc
  * test

    **Example:**

    * stage-auth.blakc.xyz
    * stage-chat.blaks.xyz
    * stage-manage.blakc.xyz
    * stage-storage.blakc.xyz
    * stage-api.blakk.xyz
    * stage.blakc.xyz

## Configuration

* Configure CORS Policy at LoadBalancer / Firewall  to allow inter-service communication
* DNS Record Entries \(for domains, subdomains, s3 buckets, etc.\)
* Enforce HTTPS via HSTS Policy
* Google/Firebase API Keys 







