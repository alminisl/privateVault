
> Writing down the progress and updates about the current state of the project with the current features and issues 


## [[17-02-2023]]

Working on the issue with the docker containers and adding tennats. 

The tenant table is only populated if I create a new one. So If I have `tenant1` it will only get populated with tables when I execute `tenant2` curl request. So I have to figure out why this is happening. 

So the thing I figured out is that the `tenant-service` needs to be restarted everytime. And After I restart it It fills the tables. 


## [[21-02-2023]]

Figuring out java spring profiles: 

spring:  
  profiles:  
    active: "local" 

- Try to trigger these programatically running docker run 
	- https://www.baeldung.com/spring-boot-docker-start-with-profile



