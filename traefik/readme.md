Make directories in your homefolder like so:
- ~/traefik
    - compose.yml
    - data
        - acme.json # make sure to change permissions of this file with chmod 600 acme.json
        - config.yml
        - traefik.yml

Use mkdir to make the folders and touch to create the json and yml files

Basically:
mkdir traefik
cd traefik
touch compose.yml
mkdir data
cd data
touch acme.json
chmod 600 acme.json
touch config.yml
touch traefik.yml

The contents to put inside those files are given here. Except for acme.json which will be automatically generated.