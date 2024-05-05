## Running Jenkins in a Docker container using Docker Compose

Running Jenkins in a Docker container using Docker Compose is a convenient way to manage the Jenkins service along with its dependencies. Below is a basic example of a Docker Compose file (docker-compose.yml) that sets up Jenkins:
```
version: '3'

services:
  jenkins:
    image: jenkins/jenkins:lts
    container_name: jenkins
    ports:
      - "8080:8080"
      - "50000:50000"
    volumes:
      - jenkins_home:/var/jenkins_home
    networks:
      - jenkins-net

networks:
  jenkins-net:

volumes:
  jenkins_home:

```

Save this configuration to a file named `docker-compose.yml`. This configuration specifies a service named jenkins, which is based on the official Jenkins LTS Docker image (`jenkins/jenkins:lts`). It maps the container's ports `8080` (Jenkins web interface) and `50000` (Jenkins agent communication port) to the same ports on the host machine.

It also mounts a volume named `jenkins_home` to persist Jenkins data such as configurations and plugins. This ensures that data isn't lost when the container is stopped or removed.

To run Jenkins using Docker Compose, navigate to the directory containing the `docker-compose.yml` file and run:

```
docker-compose up -d
```
This command will start Jenkins in detached mode (-d), meaning it runs in the background. You can then access Jenkins by navigating to http://localhost:8080 in your web browser.

When you want to stop Jenkins, run:
```
docker-compose down
```
This will stop and remove the Jenkins container, but the data will persist in the jenkins_home volume, so it will be available when you start Jenkins again.