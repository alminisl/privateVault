
I have not documented how vaultwarden works. 

However I found the guide for now which I use to update to the new version, so I'm documenting it now. 

First up command docker stop vaultwarden 

Command used to start the vaultwarden server after update: 
```bash
sudo docker run -d --name=vaultwarden -p 3012:3012 -p 5151:80 -e ADMIN_TOKEN=Idezecputem123 -v /volume1/docker/bitwarden:/data --restart always vaultwarden/server
```
Admin token seems to be unneeded here. 
