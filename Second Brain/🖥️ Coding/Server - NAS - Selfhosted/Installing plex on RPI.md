```yml 
version: "2.1"
services:
  plex:
    image: ghcr.io/linuxserver/plex:arm32v7-latest 
    container_name: plex
    network_mode: host
    environment:
      - PUID=1000
      - PGID=1000
      - VERSION=docker
      - PLEX_CLAIM= #optional
    volumes:
      - /home/pi/Plex/config:/config
      - /media/NAS/Series:/tv
      - /media/NAS/Movies:/movies
      - /media/NAS/Anime:/anime
    restart: unless-stopped
	```
	
	
Something to note here I had to link together my NAS and RPI and I have to document how I did it. Its straight forward to be honest just used this command: 

`192.168.0.24:/volume1/video /media/NAS nfs defaults,_netdev 0 0`

After I configured the Fileshare on my Synology NAS 