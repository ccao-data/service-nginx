# Nginx

This service runs on CCAO's Shiny server/Ubuntu VM and is responsible directing traffic from the Data Science subdomain ([datascience.cookcountyassessor.com](datascience.cookcountyassessor.com)) to various Data Science Department applications and services. It utilizes a containerized version of [Nginx](https://hub.docker.com/_/nginx) ((pronounced "engine-x") to direct traffic.


## Usage

To start this service, first connect to the Shiny server [via SSH](https://support.rackspace.com/how-to/connecting-to-a-server-using-ssh-on-linux-or-mac-os/) (ask IT for login details). Next, go to the folder containing this repository (usually `~/services/service_nginx`) or clone the repo if it doesn't exist locally. Finally, start the service using [Docker Compose](https://docs.docker.com/compose/gettingstarted/) by typing `docker-compose up -d` while in the same folder as `docker-compose.yml`. 

This service is configured using the [`nginx.conf`](nginx.conf) file. See [this guide](https://nginx.org/en/docs/beginners_guide.html#proxy) for general Nginx configuration and the [ShinyProxy docs](https://www.shinyproxy.io/security/) for Nginx configuration specific to ShinyProxy.

Nginx requires SSL or TLS certificates in order to serve websites via HTTPS. These certificates must exist in a subfolder named `secrets` and must have a specific names (see below). To generate certificates (self-sign) see [here](https://stackoverflow.com/questions/10175812/how-to-create-a-self-signed-certificate-with-openssl). The final directory structure should be:

```
service_nginx
├── docker-compose.yml
├── nginx.conf
└── secrets
    ├── nginx-selfsigned-datascience.crt
    └── nginx-selfsigned-datascience.key
```