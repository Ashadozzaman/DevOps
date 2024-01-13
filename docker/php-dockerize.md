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
```
And run the Docker container
```
docker run -p 8080:80 php8-hello-world

```
Now, try accessing your PHP script at http://localhost:8080. If you encounter any further issues, let me know, and we can troubleshoot further.