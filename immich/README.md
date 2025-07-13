# Immich
## Self-hosted photo and video management solution
### Easily back up, organize, and manage your photos on your own server. Immich helps you browse, search and organize your photos and videos with ease, without sacrificing your privacy.

Check out: https://immich.app

# Pre-Requisites

- Traefik already setup
- A subdomain created with ```photos.YOURDOMAIN.com``` or whatever
- Since I use an nvidia card, this installation pretty much uses the nvidia setup. If you have an Nvidia GPU, make sure that your GPU is accessible to docker containers. If you are not using an nvidia card, make sure you change the files I provided with the appropriate drivers.
- If you have an NVIDIA card, but have not done the NVIDIA setup to make it accessible to docker containers, follow the simple guide here: https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html

# Installation

- Make an immich folder in your home directory:
```
mkdir -p ~/immich
cd immich
```

- Drop the 4 files I have provided above.
- If you are using an Nvidia card, you only have to make changes to the ```.env``` and ```compose.yml``` 
- If you are using any other GPU, then you will have to adjust all 4 files. The links with information as to how to edit the file for other GPUs are provided as comments within those files
- Run it with ```docker compose up -d```
- Access it from ```photos.YOURDOMAIN.com``` or whatever you provided, and set it up.