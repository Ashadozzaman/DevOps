**Here's a basic Dockerfile for a Python "Hello, World!" application.**

**Steps 1** Create a `app.py` file and add print("Hello, World!")

`print('Hello, World!') > app.py`

**Steps 2** Create a `Dockerfile` and write Dockerize Python `Hello, World!` application.
```bash
# Use an official Python runtime as a parent image
FROM python:3.8-slim
# Set the working directory in the container
WORKDIR /app
# Copy the current directory contents into the container at /app
COPY . /app
# Run app.py when the container launches
CMD ["python", "app.py"]
```
**Steps 3** Build and run docker image.\
`docker build -t ashadozzaman/hello-python:0.0.1 .`\
`docker run ashadozzaman/hello-python:0.0.1`


## `With project details click` [Here](https://github.com/Ashadozzaman/docker-images/tree/main/python)