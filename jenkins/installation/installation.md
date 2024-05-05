### INSTALLATION jenkins  
### Installing on Linux (Ubuntu)
Please Follow official instruction [Here](https://www.jenkins.io/doc/book/installing/linux/)

### EC2 User Data
Using this code install jenkins by EC2 User Data. Don't need manual installation.
```
#!/bin/bash 
sudo apt update -y 
sudo apt install openjdk-17-jre -y 
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null 
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null sudo 
apt-get update -y 
sudo apt-get install jenkins -y
sudo apt install nginx -y
```
### Running Jenkins in a Docker container
How to install Docker click [Here](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-22-04)

Run Jenkins Image:
```
docker run -p 8080:8080 jenkins/jenkins:latest
```

Execute CMD Inside Docker Container
```
docker exec -it 86a838d8ac95 bash
```
### What is Scratch?
- When building Docker containers you define your base image in your dockerfile. The scratch image is the smallest possible image for docker. 
- Actually, by itself it is empty (in that it doesn’t contain any folders or files) and is the starting point for building out images.
there is no compiler in the image so you’re left with just system calls.
- You also wouldn’t be able to login to the container either as there isn’t a shell unless you explicitly add one.

### Changing Jenkins Port
Check where jenkins are loaded:
```
sudo systemctl status jenkins
```
Output:
`Loaded: loaded /lib/systemd/system/jenkins.service;`

Change the port in this dir
```
sudo vim /lib/systemd/system/jenkins.service
```
Reload the daemon
```
sudo systemctl daemon-reload
```
Reload jenkins server
```
sudo systemctl restart jenkins
```
### Changing Jenkins Port In Docker
```
docker run -p 80:9090 jenkins/jenkins
```
Jenkins run 9090 port

Note: Task `Persisting jenkins volume in docker`
```
Task 2: Make a docker compose file to 
run jenkins expose it on port 80 
Persist jenkins data using docker hostpath volume
Delete the jenkins server
Again create new server with old volume, collecting old files
and test if new server is collecting old data

```