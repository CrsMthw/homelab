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
cd crowdsec
touch compose.yml
mkdir config
cd config
touch acquis.yaml
cd ..
```

Then copy the contents from my compose.yml to yours and make the necessary changes.

## Run

Go to the directory with the compose.yml

Run it with ```docker compose up -d```

## How to get the bouncer API key from crowdsec AND setup Traefik-Bouncer

- After crowdsec is up and running run the following command:

```
docker exec crowdsec cscli bouncers add traefik-bouncer
```

- Copy the API key printed. You WON'T be able the get it again.

- Paste this API key as the value for bouncer environment variable ```CROWDSEC_BOUNCER_API_KEY``` in your compose.yaml

- Uncomment that whole section and save it.

- Recreate crowdsec with ```docker compose up -d --force-recreate```

## Integrate with Traefik (Final Step)

Go to the directory where traefik is setup. 

If you have used my files, uncomment the parts in both traefik.yml and config.yml that is related to crowdsec and restart traefik using ```docker restart traefik```

If you haven't used my files, refer to my [traefik data folder](https://git.crsmthw.com/crsmthw/homelab/src/branch/main/traefik/data) and add those parts from my config.yml and traefik.yml.

## Optional Steps

### Add your own public IP to the whitelist to prevent getting banned

- Login as root
```
sudo su
```
- Go to the crowdsec docker volume
```
cd /var/lib/docker/volumes/crowdsec_crowdsec-config/_data/parsers/s02-enrich
```
- Create a file called ```mywhitelists.yaml```
```
nano mywhitelists.yaml
```
- Paste the following in it:
```
name: crowdsecurity/whitelists
description: "Whitelist events from my ip addresses"
whitelist:
  reason: "my ip ranges"
  ip:
    - "YOUR.IP.ADDRESS.HERE"
```
- Replace ```YOUR/IP.ADDRESS.HERE``` with your IP Address, save and exit.

- Restart crowdsec with ```docker restart crowdsec```

### To enable notifications like telegram, gotify or more

Follow the instructions from the official documentations [here](https://docs.crowdsec.net/docs/notification_plugins/intro)

Only difference is the directory to make changes, where in our case it will be in ```/var/lib/docker/volumes/crowdsec_crowdsec-config/_data/``` and you will need to login as root with ```sudo su``` to access this directory.

## Credits

Huge thanks to Techno Tim! You can watch his video tutorial [here](https://youtu.be/-GxUP6bNxF0?si=7dpWFtDHyq8JWBZi)