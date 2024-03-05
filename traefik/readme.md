# Traefik2 reverse proxy with automatic wildcard SSL from cloudflare 

Create a DNS entry in your cloudflare: ```traefik.YOURDOMAIN.com``` Make sure it is not proxied at first (necessary for creating SSL certificate), you can enable proxy later after everything.

Create a docker network called "proxy" using the following command:
```
docker network create proxy
```
This is the network that traefik and all other containers that need to be automatically configured in traefik should use.

Make directories in your homefolder like so:
- ~/traefik
    - compose.yml
    - data
        - acme.json # make sure to change permissions of this file with ``` chmod 600 acme.json ```
        - config.yml
        - traefik.yml

Use mkdir to make the folders and touch to create the json and yml files

Basically:

```
mkdir traefik
cd traefik
touch compose.yml
mkdir data
cd data
touch acme.json
chmod 600 acme.json
touch config.yml
touch traefik.yml
cd ..
```

The contents to put inside those files are given here. Except for acme.json, which will be automatically generated.

## How to generate a hashed password to put in the compose.yml file

- First install apache2-utils
```
sudo apt update
sudo apt install apache2-utils
```
- Next generate your hashed password with the following command
```
echo $(htpasswd -nB USER) | sed -e s/\\$/\\$\\$/g
```

    - Replace USER with your username
    - Enter a password when it prompts
    - Copy paste the generated hashed password into the compose.yml file

## Run

Go to the directory with the compose.yml

Run it with ```docker compose up -d```

If everything is done right, you will be able to access the traefik dashboard at traefik.YOURDOMAIN.com in a few moments.

## How to expose my docker containers to the internet

First make sure you have created a DNS entry in your cloudflare for the service you want to expose

Then all you have to do is add these labels to the compose.yml of all your containers that you want to expose:
```
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.CONTAINER_NAME.entrypoints=http" # You can skip this line if you do not need http access at all. HTTP access can be useful for internal networks DNS resolver.
      - "traefik.http.routers.CONTAINER_NAME.rule=Host(`SUBDOMAIN.YOURDOMAIN.COM`)" # Same thing for this line. This is only for http.
      - traefik.http.routers.CONTAINER_NAME.middlewares=https-redirect@file # Remove this line if you do not want automatic http to https redirection or if you skipped the two lines above.
      - "traefik.http.routers.CONTAINER_NAME-secure.entrypoints=https"
      - "traefik.http.routers.CONTAINER_NAME-secure.rule=Host(`SUBDOMAIN.YOURDOMAIN.COM`)"
      - "traefik.http.routers.CONTAINER_NAME-secure.tls=true"
      - "traefik.http.routers.CONTAINER_NAME-secure.service=CONTAINER_NAME@docker"
      - "traefik.http.services.CONTAINER_NAME.loadbalancer.server.port=PORT_OF_CONTAINER_WEBUI"
      - "traefik.docker.network=proxy"
```
Replace ```CONTAINER_NAME``` with the name of the docker container

Replace ```SUBDOMAIN.YOURDOMAIN.COM```  with the URL you want your container webui to be exposed at.

Replace ```PORT_OF_CONTAINER_WEBUI``` with the port of the container's webui

### Example compose.yml of Heimdall Dashboard exposed with Traefik

```
version: "3.9"
services:
  heimdall:
    image: lscr.io/linuxserver/heimdall:latest
    container_name: heimdall
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Asia/Riyadh
    volumes:
      - ./config:/config
    networks:
      - proxy
    restart: unless-stopped
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.heimdall.entrypoints=http"
      - "traefik.http.routers.heimdall.rule=Host(`heimdall.example.com`)"
      - traefik.http.routers.heimdall.middlewares=https-redirect@file
      - "traefik.http.routers.heimdall-secure.entrypoints=https"
      - "traefik.http.routers.heimdall-secure.rule=Host(`heimdall.example.com`)"
      - "traefik.http.routers.heimdall-secure.tls=true"
      - "traefik.http.routers.heimdall-secure.service=heimdall@docker"
      - "traefik.http.services.heimdall.loadbalancer.server.port=80"
      - "traefik.docker.network=proxy"
networks:
  proxy:
    external: true
```

## How to expose anything else

By anything else I mean services on other computers or containers that cannot use the proxy network, like home-assistant for example which needs host network.

For this you need to make entries in the config.yml file. An example of home-assistant is already given in the config.yml file.


## Credits

Huge thanks to Techno Tim. You can watch his video tutorial [here](https://youtu.be/liV3c9m_OX8?si=qPIQsIdypHKt2hUq)