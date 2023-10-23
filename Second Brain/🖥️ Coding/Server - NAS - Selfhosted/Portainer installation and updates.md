
https://www.wundertech.net/how-to-update-portainer/


## How to Update Portainer

Now that we understand exactly what Portainer does, we’re going to look at how to update Portainer.

1. Connect to the host where Docker is installed. In the example below, I used SSH to access Docker, but you can access it however you’d like.

`ssh username@DOCKER_IP`

2. Run the command below to get the Docker containers that you have installed and get the **container** **ID** for Portainer.

`sudo docker container ls`

![showing the docker containers on the device.](https://www.wundertech.net/wp-content/uploads/2022/05/image-103.png)

3. Run the command below to **stop** the Portainer container.

`sudo docker stop portainer`

![stopping the portainer container.](https://www.wundertech.net/wp-content/uploads/2022/05/image-104.png)

**NOTE: If the command above does not work, stop the container using the container ID**

`sudo docker stop [CONTAINER_ID]`

![stopping a specific container by ID.](https://www.wundertech.net/wp-content/uploads/2022/05/image-105.png)

4. Delete the Portainer container by running the command below.

**NOTE: If your prior instance of** **Portainer did not have a persistent volume, your data/configuration will be lost.**

**Ensure that you have the important data that exists in the /data location of the Portainer container or you will have to recreate your user account and modify your settings.**

sudo docker rm portainer

![removing the portainer container.](https://www.wundertech.net/wp-content/uploads/2022/05/image-106.png)

NOTE: If the command above does not work, delete the container using the **container** **ID**.

`sudo docker rm [CONTAINER_ID]`

5. Pull the latest version of the Portainer container.

sudo docker pull portainer/portainer-ce:latest

![downloading the latest portainer image.](https://www.wundertech.net/wp-content/uploads/2022/05/image-107.png)

6. Recreate the Portainer container using the command below.

`sudo docker run -d -p 8000:8000 -p 9000:9000 -p 9443:9443 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest`

![re-creating the portainer container by command.](https://www.wundertech.net/wp-content/uploads/2022/05/image-108.png)

7. You can log back into Portainer and it will be updated!