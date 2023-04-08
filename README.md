# Docker Proxy - Multiple Applications

With this method you can serve multiple applications in different docker containers for diffrent domains.


## How To Use?

### 1. Create a new docker network for proxy
We need to create a custom network first. 
```
$ docker network create nginx-proxy
```


### 2. Application Docker Config Example
Create or update your applications docker-compose.yaml file to use with this proxy.
Define your domain as environment.

```
version: "3.8"
services:
  app1:
    ...
    expose:
      - 80
    environment:
      - VIRTUAL_HOST=app1.domain.local
      - VIRTUAL_PORT=80
    networks:
      - proxy

networks:
  proxy:
    external:
      name: nginx-proxy

```
You can follow same setup for your all applications (app1, app2, app3 e.t.c)


### 3. Add your domains in /etc/hosts file
You need to define your domains in hosts.

```
127.0.0.1	app1.domain.local
127.0.0.1	app2.domain.local
127.0.0.1	app3.domain.local
```
