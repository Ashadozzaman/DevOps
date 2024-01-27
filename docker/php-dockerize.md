# 🚀 PHP Dockerize File 🚀

### `Dockerfile` and `index.php` are in the same directory, you can simply use:
```
# Use the official PHP 8 image from Docker Hub
FROM php:8.0-apache

# Copy the local PHP files to the container
COPY docker/index.php /var/www/html/

# Set the ServerName to suppress the warning
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

# Expose port 80 for Apache
EXPOSE 80

```

### This assumes your directory structure is something like:

```
/your-docker-context
|-- Dockerfile
|-- docker
|   `-- index.php

```
Make sure you are running the docker build command from the correct directory, and the context includes the necessary files.

### After fixing the Dockerfile, rebuild the Docker image:
```
docker build -t php8-hello-world .
docker build -it php8-hello-world .
```
And run the Docker container
```
docker run -p 8080:80 php8-hello-world

```
`docker build`: Initiates the building of a Docker image.

`-i`: This flag stands for interactive. It allows you to interact with the `Docker build` process, providing input if needed. In the context of docker build, it's often not necessary to use the `-i `flag, as the build process is usually non-interactive. This flag is more commonly used with running containers, where it opens an interactive session.

`-t`: Specifies the name and optionally a tag to the Docker image.

<!-- `ashadozzaman/nodejs:001`: This is the name and tag you are assigning to the image. In this case, the image will be tagged as "ashadozzaman/nodejs" with the version "001". -->

`php8-hello-world`: This is the name and tag you are assigning to the image. In this case, the image will be tagged as "php8-hello-world" with the version "001".

`.`: Indicates the build context, which is the location of the Dockerfile and any files that are used in the build process. The . refers to the current directory.

Now, try accessing your PHP script at http://localhost:8080. If you encounter any further issues, let me know, and we can troubleshoot further.

## `With project details click` [Here](https://github.com/Ashadozzaman/docker-images/tree/main/php)