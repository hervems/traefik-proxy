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
            - "traefik.docker.network=traefik_gateway"
            - "traefik.frontend.rule=Host:my.localhost"
            - "traefik.backend=node"
        networks:
            - gateway
            - internal
    nginx:
        image: ...
        labels:
            - "traefik.docker.network=traefik_gateway"
            - "traefik.1.frontend.rule=Host:admin.localhost; PathPrefix: /api"
            - "traefik.2.frontend.rule=Host:myapi.localhost"
            - "traefik.backend=nginx"
        networks:
            - gateway
            - internal
networks:
    internal:
    gateway:
        external: true
        name: traefik_gateway

```
