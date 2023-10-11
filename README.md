# Approov Demo Server

A very simple Nginx server running on a docker container behind Traefik to serve as the homepage for demo.approov.io, the default page used by the Traefik setup. This also re-directs any undefined subdomains of demo.approov.io to the default page.


## Production Deployment

This guide assumes that you are logged in to the EC2 server that you set up by following the instructions for [AWS EC2 Traefik Setup for demo.approov.io](https://github.com/CriticalBlue/demo-approov-io-traefik). If you followed these instructions, the docker network `traefik`, which is required, will already exist. It can be re-created using this command: `sudo docker network create traefik`.

Git clone this repo into the home folder `/home/ec2-user` and change to the newly created directory:

```console
git clone https://github.com/CriticalBlue/demo-approov-io-web.git && cd demo-approov-io-web
```

> **NOTE**: If you are running the deployment in a box that isn't `demo.approov.io` then copy `.env.example` to `.env` and customize it. The default values are set in the `docker-compose.yml` file at the services `web` and `redir`.

Pull the docker image for Nginx:

```console
sudo docker pull nginx:alpine
```

Start the web server and redirection services:

```console
sudo docker-compose up --detach web redir
```

Inspect the logs (optional):

```console
sudo docker-compose logs --follow --tail 10
```

Finally, check the web server works by visiting [https://demo.approov.io](https://demo.approov.io). Also check that the redirection to the main page works by visiting a nonexisting subdomain of `demo.approov.io`, for example [https://nonexistent.demo.approov.io](https://nonexistent.demo.approov.io).


## Localhost Deployment

First, create a docker network for Traefik:

```console
 docker network create traefik
```
> **NOTE:** In development Traefik isn't used, but the network is declared in the `docker-compose.yml` file .

Git clone this repo into the a folder on your machine:

```console
git clone https://github.com/CriticalBlue/demo-approov-io-web.git && cd demo-approov-io-web
```

Now, pull the docker image for Nginx:

```console
sudo docker pull nginx:alpine
```

Next, start the docker stack:

```console
sudo docker-compose up dev
```

Finally, check it works by visiting http://localhost, then make any changes needed to the `index.html` page and refresh the browser to see them.
