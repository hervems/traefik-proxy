# Traefik Proxy external docker

This is a Traefik external docker and it can manage all your
local dockers.

## Requirements

* [docker](https://docs.docker.com/install/) version 18.02.0 or more
* [docker-compose](https://docs.docker.com/compose/install/) version 1.20.0 or more

## Use Makefile

* Install : `make install`
* Start the container: `make start`
* Stop the container: `make stop`
* Clean the container: `make clean`
* Destroy the containers and images too: `make destroy`
* Console: `make console`
* All logs: `make logs`
* Just error logs : `make error-logs`

## Example of Traefik labels in a docker-compose.yml

```yaml
version: '3.5'

services:
    db:
        image: ...
        networks:
            - internal      
    node:
        image: ...
        labels:
            - "traefik.enable=true"
            - "traefik.docker.network=traefik_gateway"
            - "traefik.http.routers.service_node.rule=Host(`my.localhost`")
        networks:
            - gateway
            - internal
    nginx:
        image: ...
        labels:
            - "traefik.enable=true"
            - "traefik.docker.network=traefik_gateway"
            - "traefik.http.routers.service_nginx.rule=Host(`api.localhost`")
        networks:
            - gateway
            - internal
networks:
    internal:
    gateway:
        external: true
        name: traefik_gateway

```

## Frontend Traefik

You can access to the web frontend traefik via: [http://127.0.0.1:8080](http://127.0.0.1:8080)
