# RITlug GitLab

## About

The [RITlug GitLab](https://git.ritlug.com) is a hosted, Community Edition (CE) GitLab instance.
This GitLab instance runs on [Titan](http://runbook.ritlug.com/infrastructure/hosted-server/).


## Contents

RITlug's GitLab requires several custom files for operation. 


### gitlab-renew-cert.timer

This `systemd` timer is used to renew the https://git.ritlug.com Let's Encrypt certificate.
Currently, this cert is set to renew every Wednesday at 3AM EDT.


### gitlab-renew-cert.service

This `systemd` service file is used in conjunction with `gitlab-renew-cert.timer`.
Once the date and time of the systemd timer is reached, this service file is executed.


### gitlab-renew-cert

This script is the main culprit for renewing the GitLab web certificate.
It is located under `/usr/local/bin/` and is executed by the `systemd` service file.
Its contents temporarily shuts down the RITlug GitLab, renews the Let's Encrypt cert, and starts up GitLab.
GitLab cannot be running at the time of the cert renewal.
