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

- Finally, start a container named **greet** using the built image
```bash
    docker run --name greet greet
```

## Advance Task
Make the docker image customisable, and have the Docker image print **“Hello, [your name]!”** instead of **“Hello, Captain!”**.

One possible approach to this problem is illustrated below
- Update your dockerfile as shown:
```dockerfile
    FROM alpine:latest
    # Define the default Name to be used, if not specified at build time
    ARG MY_NAME="Captain"
    ENV NAME="${MY_NAME}"
    # Execute our command in shell format
    CMD echo "Hello, ${NAME}!"
```
- Rebuilding the image without a custome name
```bash
    docker build -t greet:v1 .
```
- Start a new container **customegreet1** off the new image **greet:v1**
```bash
    docker run --name customegreet greet:v1
```
Result:
    **Hello, Captain!**
- Rebuilding the image with a custome name
```bash
    docker build --build-arg MY_NAME=Godwin -t greet:v2 .
```
- Start a new container **customegreet2** off the new image **greet:v2**
```bash
    docker run --name customegreet greet:v2
```
Result:
    **Hello, Godwin!**

### Note:
- We have two ways of defining variables in a Dockerfile, Namely:
    - ARG
    - ENV
- The Value of a variable defined using **ARG** is passed only at **build-time**. Hence, the value is not accessible after build time
- The Value of a variable defined using **ENV** is passed only at **run-time**. Hence, the value is accessible only at run time
- The **CMD** command only **runs after build time** and can be executed in two formats given below
```dockerfile
    #  exec format
    CMD ["executable","param1","param2"]
```
    ```dockerfile
    # shell format
    CMD command param1 param2
    ```
- You can also define an **ENV** variable and customise it at run time using the **-e** flag when running the container.
  This way, you don't need to first define the variable as **ARG** type as used in the example above
  This is shown below:
  - Update your dockerfile as shown:
```dockerfile
    FROM alpine:latest
    # Define the default Name to be used, if not specified at build time
    # ARG MY_NAME="Captain"
    ENV NAME="Captain"
    # Execute our command in shell format
    CMD echo "Hello, ${NAME}!"
```
- Rebuilding the image 
```bash
    docker build -t greet:v3 .
```
- Start a new container **customegreet3** off the new image **greet:v3** without a custom name
```bash
    docker run --name customegreet3 greet:v3
```
Result:
    **Hello, Captain!**

- Start a new container **customegreet4** off the new image **greet:v3** with a custom name
```bash
    docker run -e MY_NAME=Godwin --name customegreet4 greet:v3
```
Result:
    **Hello, Godwin!**

For more information about this project, visit [roadmap](https://roadmap.sh/projects/basic-dockerfile)

