
- npm 
- docker  
- env? 


### Testing
- Sinon - https://sinonjs.org/ 
- Ava - https://github.com/avajs/ava 


## Infra 

https://k8slens.dev/ for infra monitoring? 
Grafana dashboard? 
https://min.io/ - Minio - High performance object storage 
ley for DB Migrations https://github.com/lukeed/ley - Does it make sense to look into https://www.prisma.io/ ? 



### Starting the app 

- Currently issues with the startup as some ports seem to be taken, even tho they should not be. Debugging this more. 

```bash
sudo netstat -pna | grep docker-proxy
```

#### Solution to isse with Docker-proxy

kill the docker proxy manually by restarting the docker service ```

```bash
sudo service docker stop && sudo service docker start 
```


## Components

DSFINV - Fastify 

Ckuebt - REST API - DSFIN communication 
DASHBOARD - Create api key and secret 

https://kassensichv-middleware.fiskaly.com/api/v2 auth process happens here - send data from Dashboard 

Read and write when auth - Write / Read DB 
 - Sign DE API + DB 

cash point closing workers - verify info from SignDE and then exeute the worker and return a status




# TODO 

- Update plugins Tmux - https://github.com/tmux-plugins/tpm
- Update VSCode ext 