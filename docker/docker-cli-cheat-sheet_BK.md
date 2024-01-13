# 🚀Docker Cheat Sheet/CLI Commands🚀

## Let’s try some basic command 

1. This command is used to check the installed Docker version on your system.\
`sudo docker version`
2. Display system-wide information.\
`sudo docker info`
3. This command checks the status of the Docker service using systemd.\
`sudo systemctl status docker`
4. This command displays a list of currently running Docker containers.\
`sudo docker ps`
5. This command shows all containers, including those that are not currently running.\
`sudo docker ps -a`
6. This command lists all the Docker images that are available on your system.\
`sudo docker images`
7. This command pulls the latest version of the Nginx.\
`sudo docker run nginx`
8. The correct command to list running containers.\
`docker container list`\
*Additionally, using **sudo** might be necessary depending on your system's configuration.*
 ---

## Managing Docker Services and Sockets with Systemd

Docker service can still be activated through the Docker socket (`docker.socket`) even if you stop the Docker service (`docker.service`). The Docker socket allows communication with the Docker daemon and is used for Docker API access.

1. This command checks the status of the Docker service.\
`sudo systemctl status docker`
2. This command stops the Docker service.\
`sudo systemctl stop docker`
3. This command checks the status of the Docker service again.\
`sudo systemctl status docker`
4. This command stops the Docker socket.\
`sudo systemctl stop docker.socket`
5. This command checks the status of the Docker service once again.\
`sudo systemctl status docker`
---

## The lifecycle of a Docker container
The lifecycle of a Docker container involves creation, running, stopping, and removal. Containers are created from Docker images, run as isolated instances, can be stopped or paused, and can be removed when no longer needed.

<img src="images/Container_life.png" alt="Lifecycle of Docker Container" width="800"/>

Image: Lifecycle of a Docker container

**Example**

1. docker create:\
Purpose: Creates a new container but does not start it.\
Example:\
Creates a new container named "my-container" using the Nginx image but does not start it.\
`docker create --name my-container nginx`

2. docker start:\
Purpose: Starts one or more stopped containers.\
Example:\
Starts the container named "my-container" that was previously created but stopped.\
`docker start my-container`

3. docker run:\
Purpose: Creates and starts a new container in a single command.\
Example:\
This command combines the process of creating and starting a container named "my-container" using the Nginx image in a single step.\
`docker run --name my-container nginx`

#### How to access it in browser

```docker run -d -p 8080:80 --name my-container nginx```

`docker run`: This is the command used to run a Docker container.

`-d`: This flag stands for "detach." It runs the container in the background, allowing you to use the terminal for other commands without being attached to the container's console.

`without -d`: When you run a Docker container without the `-d` flag, it runs in attached mode. In attached mode, the terminal remains connected to the container, and you can see the output of the processes running in the container directly in your terminal.

`-p 8080:80`: This flag maps the host machine's port 8080 to the container's port 80. In other words, it exposes port 80 of the NGINX container to port 8080 on your host machine. So, if you access `http://localhost:8080` on your host machine, it will be directed to port 80 inside the running NGINX container.

`--name my-container`: This flag assigns a name to the container, in this case, "my-container". You can refer to the container by this name instead of its auto-generated identifier.

`nginx`: This is the name of the Docker image used to create the container. In this case, it's the official NGINX image from Docker Hub. Docker will pull this image from the Docker Hub registry if it's not already available locally.


4. docker pause:\
Purpose: Temporarily pause the processes in the running container.\
Example:
    ```bash
    docker pause my-container
    docker ps --filter "name=my-container"
    docker unpause my-container
    docker ps --filter "name=my-container"
    ```
5. docker stop:\
Purpose: The docker stop command is used to stop a running container.\
Example:\
This command stop a container named "my-container".\
`docker stop my-container`

6. docker rm:\
Purpose: The docker rm command is used to remove a container.\
Example:\
Want to remove container named "my-container".\
`docker rm my-container`

---

## Why a Docker container exits!!!
Docker containers are designed to run a specific command or process and exit when that command or process completes. The default behavior is to start the specified command or process inside the container and stop when that command or process finishes execution.\
Docker containers run as long as the process inside the container is active.\
Example:\

Default Shell Behavior (Container Stops Immediately).\
`docker run busybox`

Run an Interactive Terminal (Container Remains Running).\
`docker run -it busybox`

Run a Command to Keep Container Running (e.g., Sleep). In the third example, the sleep 3600 command will keep the container running for 3600 seconds (1 hour), and then it will exit.\
`docker run busybox sleep 3600`

---
## Docker Container Lifecycle

Run a container from an image.\
`docker run nginx`

List running containers.\
`docker ps`

List all containers (running and stopped).\
`docker ps -a`

Run a command inside a running container.\
`docker exec my-nginx ls /usr/share/nginx/html`

Here's a breakdown:

`docker exec`: This command allows you to run a command inside a running container.
`my-container`: This is the name you assigned to your NGINX container using the `--name` flag when you started it.
`ls /usr/share/nginx/html:` This is the command you want to run inside the container. In this case, you're using ls to list the contents of the 
`/usr/share/nginx/html` directory, which is the default location for NGINX's static content.

Basically this command use for access in container, bellow show steps:-

`docker exec web-server hostname` - get container hostname 

`docker exec -it web-server /bin/bash` - Enter in container 


Display detailed information about a container.\
`docker inspect my-nginx`

Stop a running container via name or ID.\
`docker stop my-nginx`

stop all running container.\
`docker container stop $(docker container ps -q)`

Start a stopped container vi name or ID.\
`docker start 24952546f818`

Restart a container.\
`docker restart 24952546f818`

Restart after 30 second.\
`docker restart -t 30 6d144a1d546b` 

Remove a stopped container.\
`docker rm 24952546f818`

Remove multiple containers.\
`docker rm 24952546f818 6d144a1d546b`

Remove all containers.\
`docker rm $(docker ps -aq)`

Temporary pause a Docker container.\
`docker pause  24952546f818`

Unpause a Container.\
`docker unpause 24952546f818`

## Container Naming and Identification:
Run a container with Name.\
`docker run --name my-container nginx`

Rename a container.\
`docker rename my-nginx new-nginx`

Get the container ID by its name.\
`docker inspect --format='{{.Id}}' nginx`


## Container Logs and Stats:
Display the logs of a container.\
docker logs <containerID>

Display a live stream of container resource usage statistics.\
docker stats <containerID>

docker exec 266 cat /var/log/nginx/access.log

## Container Interaction:
Attach to a running container (not recommended for long-term use).\
`docker attach <containerID>`

Run an interactive shell inside a container.\
docker exec -it <containerID> bash


docker container run -it ubuntu
docker container exec b71f15d hostname	//Check container host Name
docker container exec -it b71f15d33b60 /bin/bash	//Enete container bash
docker container stats	//Live stream of containers resource usage statistics
docker container top nginx 5ac4	//Single container resources consumptions
docker container stats nginx 5ac4	//Multiple containers stats by name and ID

## Docker Images and Tag:
List of all image.\
`docker image ls`

Pull an image from a registry.\
`docker pull nginx`

Show detailed information about an image.\
`docker image inspect nginx`

Tag the existing Image with the New Name.\
`docker tag old-image:old-tag new-image:new-tag`

Remove an image.\
`docker image rm my-image:tag`

Remove all unused images.\
`docker image prune -a`

Remove all images.\
`docker rmi $(docker images -q)`


## Publishing Ports:


## docker volume:
docker cp



## Docker Restart Policy:



## Container Cleanup:
docker container prune: Remove all stopped containers.
docker container stop $(docker container ps -q): Stop all running containers.
docker container rm $(docker ps -aq): Remove all containers.



[Ref](https://docs.docker.com/engine/reference/run/)
