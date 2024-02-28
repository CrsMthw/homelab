# Adguard-Home

## Installation and setup

- Make a docker macvlan network first using [this documentation](https://docs.docker.com/network/drivers/macvlan/)
- I named my macvlan network ```priv_lan```, if you used some other name, change it in the compose.yml
- Run it with ```docker compose up -d```
- Access the adguard-home dashboard through the ipv4 address you specified in the compose.yml (for security reasons DO NOT expose this dashboard outside your network)
- Go through the settings and change whatever you like
- Set the ipv4 address as the DNS server 1 & 2 in your router. (If your router does not have a DNS setting, you can try to setup adguard-home as your DHCP server, but make sure you TURN OFF the DHCP server in your main router)