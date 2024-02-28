# Traefik reverse proxy with automatic wildcard SSL from cloudflare 

First create a docker network called "proxy" usig the following command:
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
```
```
cd traefik
```
```
touch compose.yml
```
```
mkdir data
```
```
cd data
```
```
touch acme.json
```
```
chmod 600 acme.json
```
```
touch config.yml
```
```
touch traefik.yml
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