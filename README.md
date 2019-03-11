burdastyletech/reverse-proxy
------------------------
This image contains a reverse proxy, based on [Traefik](https://docs.traefik.io) to automatically make containers 
available in the browser without any extra configuration.
## Features

## How use it

- Create a docker network where container could be automatically added:
```
docker network create reverse-proxy
```
**Every container must be configured to belong to this network, as the container (Traefik) of this image**

- Spin up traefik with:
```
docker run -d \
    -p 80:80 \
    -p 443:443 \
    -p 8080:8080 \
    -v /var/run/docker.sock:/var/run/docker.sock \
    --name traefik \
    --network reverse-proxy \
    burdastyletech/reverse-proxy:1.0.0
```
or to have a custom configuration under *conf/traefik.toml*:
```
docker run -d \
    -p 80:80 \
    -p 443:443 \
    -p 8080:8080 \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v ${PWD}/conf/traefik.toml:/etc/traefik/traefik.toml \
    --name traefik \
    --network reverse-proxy \
    burdastyletech/reverse-proxy:1.0.0
    
```
## Build a new image
If you prefer to build a new image just run:
```
docker image build -t {your/image/name}:{your/tag} .
```