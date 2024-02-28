# Full fledge Media Server system with Plex. Jellyfin, *arr stack, Qbittorrent, and more

This is a fully automated media-server system. Once you setup everything, all you have to do is make a request for the movie/show/whatever and it will be available within moments for you to enjoy.

The components included in this system are:
- autoscan
- bazarr
- deleterr
- deluge
- jackett
- jellyfin
- lidarr
- overseerr
- plex
- prowlarr
- qbittorrent
- radarr
- readarr
- sonarr
- tautulli
- whisparr
- youtube-dl

## How my directories are setup

This will help you understand the volume bind mounts in my compose.yml and help you figure out how you want to setup your directories.

I have a NAS that is mounted to ```/lake```, this is the parent directory for everything
```
lake
|__downloads
|  |__torrents # this is where qbittorrent downloads to, sub-categories inside are made by qbittorrent's auto management
|     |__books
|     |__movies
|     |__music
|     |__other
|
|__media # this is where arr stack apps and youtube-dl organize media into, sub-categories inside are for the different apps
|  |__anime
|  |__books
|  |__movies
|  |__music
|  |__shows
|  |__xx
|  |__xxx
|  |__youtube
|  |__youtube-music
|  |__youtube-subscriptions
|
|__starr # this is where all the apps store their configs and database
   |__autoscan
   |__bazarr
   |__deleterr
   |__deluge
   |__jackett
   |__jellyfin
   |__lidarr
   |__overseer
   |__plexmediaserver
   |__prowlarr
   |__qbittorrent
   |__radarr
   |__readarr
   |__sonarr
   |__tautulli
   |__whisparr
   |__youtube-dl
   |__youtube-dl-mongodb
```

## Installation

- Copy the compose.yml file
- Make the required changes: the timezones, volume mounts, and IP address for plex and jellyfin sections and save it
- Run it using ```docker compose up -d```
- Go through the web-ui of all the apps and do all the settings and connections like connecting overseerr to radarr and sonarr, and connecting prowlarr to radarr, sonarr, lidarr, etc.
- Go to Plex and/or Jellyfin web-ui and set up all your media folders. Like Movies = /media/movies.
- Since autoscan and deleterr do not have a webui, they have to be configured using config files. Copy the config files for autoscan and deleterr (optional) and make changes to it as per your needs and save them.
- Restart the entire stack by going into the directory with the compose.yml file and entering ```docker compose up -d --force-recreate```

## How to use

Once you setup and install everything and do all the configs and connections right, you can go to ```ovs.example.com``` to request a movie/show and everything else should be done automagically in the backend, and the media will be available on your plex/jellyfin to enjoy!

For everything else other than movies/shows, you have to visit the respective app to request for the media you want.
