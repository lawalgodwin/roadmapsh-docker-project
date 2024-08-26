# Basic Docker file
A project that test ones ability to set up docker

In this project, I wrote a basic Dockerfile to create a Docker image.
When this Docker image is run, it should print **“Hello, Captain!”** to the console before exiting

## Requirements
- The Dockerfile should be named Dockerfile.
- The Dockerfile should be in the root directory of the project.
- The base image should be **alpine:latest**.
- The Dockerfile should contain a single instruction to print **“Hello, Captain!”** to the console before exiting.

You can learn more about writing a docker file [here](https://docs.docker.com/reference/dockerfile/)

## How I solved the Problem:
- I created a **Dockerfile** then populated it with the following content
```dockerfile
    FROM alpine:latest
    CMD [ "echo", "Hello, Captain!" ]
```
- Built the image using the command:
```bash
    docker build -t greet .
```

- To confirm image **greet** was built sucessfully, I ran the command:
```bash
    docker images | grep greet
```

- Finally, run start a container named **greet** using the built image
```bash
    docker run --name greet greet
```


