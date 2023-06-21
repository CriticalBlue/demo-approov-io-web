# Approov Demo Server

A very simple Nginx server running on a docker container behind Traefik to serve as the homepage for demo.approov.io, the default page used by the Traefik setup.

## Production Deployment

This guide assumes that you are in the EC2 server that you setup by following the [AWS EC2 Traefik](https://github.com/approov/aws-ec2-traefik-setup) setup guide.

First, create a docker network for Traefik:

```console
 docker network create traefik
```

Now, git clone this repo into the home folder `/home/ec2-user`:

```console
git@github.com:approov/aws-ec2-traefik-setup.git
```

> **NOTE**: If you are running the deployment in a box that isn't demo.approov.io then copy `.env.example` to `.env` and customize it.

Next, get inside the repo:

```console
cd core-demo-approov-io
```

Now, pull the docker image for Nginx:

```console
sudo docker pull nginx:alpine
```

Next, start the docker stack:

```console
sudo docker-compose up web --detach
```

Now, to tail the logs (optional):

```console
sudo docker-compose logs --follow --tail 10
```

Finally, check it works by visiting https://demo.approov.io.

Traefik will handle creation and renewal of LetsEncrypt certificates for you.


## Localhost Deployment

First, create a docker network for Traefik:

```console
 docker network create traefik
```
> **NOTE:** In development Traefik isn't used, but the network is declared in the `docker-compose.yml` file .

Now, git clone this repo into the a folder on your machine:

```console
git clone https://github.com/approov/core-demo-approov-io
```

Next, get inside the repo:

```console
cd core-demo-approov-io
```

Now, pull the docker image for Nginx:

```console
sudo docker pull nginx:alpine
```

Next, start the docker stack:

```console
sudo docker-compose up dev
```

Finally, check it works by visiting http://localhost and then make any changes needed to the `index.html` page a refresh the browser to see them.
