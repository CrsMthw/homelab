# Headscale with Headscale Admin UI

## What is it?
Headscale is an admin management server for tailscale services.
Headscale-Admin is the UI interface for Headscale.

This Docker compose sets up the above two things for you.

## Pre-requisites
Create a DNS entry on your cloudflare (or whatever DNS you use). 
For example ```https://tailscale.YOURDOMAIN.com```

## Setup
- Copy the compose.yml into portainer or dockge or whatever compose manager you use, and run.
- Enter the following command to make an API key within headscale: ```docker exec headscale headscale apikeys create --expiration 90d``` You can change the expiration limit if you want. Copy the resulting API key.
- Now go to ```https://tailscale.YOURDOMAIN.com/admin``` This will open the UI page of Headscale Admin.
- Leave the API URL blank, and fill in the API KEY you copied earlier and proceed.
- Refresh the page or go to ```https://tailscale.YOURDOMAIN.com/admin``` again to see all the settings now.
- Create your first user in the Users page.
- You can now add nodes and stuff.

## Node Setup
- Go to https://tailscale.com and download and install the client for your device.
- Then follow the instructions provided in this link to connect the client node to your custom headscale server: https://tailscale.com/kb/1507/custom-control-server
- You can use the UI at ```https://tailscale.YOURDOMAIN.com/admin``` to create a node, in the Nodes page where you can add the device key directly, to authorize your client device.
- If you want to be able to use the network of a certain node like a VPN, make sure you setup that client as an exit node. Then any other nodes can connect to the network of this node. More info here: https://tailscale.com/kb/1103/exit-nodes