# ConvertX File Converter


## Setup

First go to your cloudflare at https://dash.cloudflare.com and create a new CNAME record, something like ```convert.YOURDOMAIN.com```

Then let's setup directories in your homefolder like so:
- ~/convertx

Basically:
```
mkdir ~/convertx
cd ~/convertx
```

Then copy the contents from my compose.yml to your portainer > stacks > create new stack, and make the necessary changes.

## Run

Ater making the changes in the compose.yml, deploy it.
