# Nginx

This service runs on CCAO's Shiny server/Ubuntu VM and is responsible directing traffic from the [Data Department subdomain](https://datascience.cookcountyassessor.com) to various Data Department applications and services. It utilizes a containerized version of [NGINX](https://hub.docker.com/_/nginx) (pronounced "engine-x") to direct traffic.


## Usage

To start this service, first connect to the Shiny server [via SSH](https://support.rackspace.com/how-to/connecting-to-a-server-using-ssh-on-linux-or-mac-os/) (ask IT for login details). Next, go to the folder containing this repository (usually `~/services/service_nginx`) or clone the repo if it doesn't exist locally. Finally, start the service using [Docker Compose](https://docs.docker.com/compose/gettingstarted/) by typing `docker-compose up -d` while in the same folder as `docker-compose.yml`.

This service is configured using the [`nginx.conf`](nginx.conf) file. See [this guide](https://nginx.org/en/docs/beginners_guide.html#proxy) for general NGINX configuration.

NGINX requires SSL or TLS certificates in order to serve websites via HTTPS. These certificates must exist in a subfolder named `secrets` and must have a specific names (see below). To generate certificates see [this wiki article](https://github.com/ccao-data/wiki/blob/master/How-To/Issue-a-certificate-for-the-data-team-server.md.md). The final directory structure should be:

```
service_nginx
├── docker-compose.yml
├── nginx.conf
└── secrets
    ├── nginx-selfsigned-datascience.crt
    └── nginx-selfsigned-datascience.key
```
