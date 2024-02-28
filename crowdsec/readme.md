# Crowdsec with Traefik Bouncer

Let's protect your homelab with Crowdsec and Traefik Bouncer

## Setup

Let's setup directories in your homefolder like so:
- ~/crowdsec
    - compose.yml
    - config
        - acquis.yaml

Basically:
```
mkdir crowdsec
```
```
cd crowdsec
```
```
touch compose.yml
```
```
mkdir config
```
```
touch acquis.yaml
```

## Run

Go to the directory with the compose.yml

Run it with ```docker compose up -d```

## How to get the bouncer API key from crowdsec AND setup Traefik-Bouncer

- After crowdsec is up and running run the following command:

```
docker exec crowdsec-example cscli bouncers add traefik-bouncer
```

- Copy the API key printed. You WON'T be able the get it again.

- Paste this API key as the value for bouncer environment variable ```CROWDSEC_BOUNCER_API_KEY``` in your compose.yaml

- Uncomment that whole section and save it.

- Recreate crowdsec with ```docker compose up -d --force-recreate