
# 🚀How To Install and Use Docker on Ubuntu 22.04🚀


## Install Docker Engine on Ubuntu 22.04Lts [Reference](https://docs.docker.com/engine/install/ubuntu/)

**Install using the apt repository**

1. Set up Docker's apt repository.
   
```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```
2. Add the repository to Apt sources:
```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
Note: If you use an Ubuntu derivative distro, such as Linux Mint, you may need to use `UBUNTU_CODENAME` instead of `VERSION_CODENAME`

3. Install the Docker packages.

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

#### Specific version 
To install a specific version of Docker Engine, start by listing the available versions in the repository:
```
# List the available versions:
apt-cache madison docker-ce | awk '{ print $3 }'

5:24.0.0-1~ubuntu.22.04~jammy
5:23.0.6-1~ubuntu.22.04~jammy
...
```


4. Verify that the Docker Engine installation is successful by running the hello-world image.

`sudo docker run hello-world`

**Manage Docker as a non-root user**

The Docker daemon binds to a Unix socket, not a TCP port. By default it's the root user that owns the Unix socket, and other users can only access it using sudo. The Docker daemon always runs as the root user.\
If you don't want to preface the docker command with sudo add user to docker group.

1. Add your user to the docker group.

`sudo usermod -aG docker $USER`

2. Starts a new shell with the updated group memberships without requiring a logout.

`newgrp docker`

**Configure Docker to start on boot with systemd and disable**

```
sudo systemctl enable docker.service
sudo systemctl enable containerd.service

sudo systemctl disable docker.service
sudo systemctl disable containerd.service
```
---
## Uninstall Docker Engine

1. Uninstall the Docker Engine, CLI, containerd, and Docker Compose packages

`sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras`

2. Images, containers, volumes, or custom configuration files on your host aren't automatically removed. To delete all images, containers, and volumes.

```
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```

🎉🎉🎉 Congratulations!!! It's Done 🎉🎉🎉