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

- Recreate crowdsec with ```docker compose up -d --force-recreate```

## Integrate with Traefik (Final Step)

Go to the directory where traefik is setup. 

If you have used my files, uncomment the parts in both traefik.yml and config.yml that is related to crowdsec and restart traefik using ```docker restart traefik```

If you haven't used my files, refer to my [traefik data folder](https://git.crsmthw.com/crsmthw/homelab/src/branch/main/traefik/data) and add those parts from my config.yml and traefik.yml.

## Credits

Huge thanks to Techno Tim! You can watch his video tutorial [here](https://youtu.be/-GxUP6bNxF0?si=7dpWFtDHyq8JWBZi)