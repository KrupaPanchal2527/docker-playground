What is **Docker**?

Imagine Docker as a virtual box that you can put your software into or your current development setup into. It's very common in developer community to have issues like, "oh, it works on my machine", Docker solves exactly this problem. 

Suppose, you are running a React project on your system with node version 16. Your colleague is trying to run the same project but on his machine the node version is 21. Definitely, some things won't work and you will scratch your hand thinking why this isn't working on his machine. Once you find out that the issue is related to the nodeJS version then you will make sure to install exact version on the new machines where you want to setup your project. Now this is not a really good way to handle this, replication of project on different machine with different environment would be really time consuming and painful.

This is where **Docker** comes into picture. It basically creates a blueprint of the services required with their exact version information which your colleague can use without worrying about installing exact version of node JS that is on your machine. 

In a nutshell, it makes it easier for developers to build, ship, and run applications without worrying about the environment they'll run in.

#### Installation

Required things -

1. Docker CLI
2. Docker Desktop (GUI for docker)

Visit docker website's download page - https://www.docker.com/products/docker-desktop/

Verify whether docker is installed or not by running command `docker --version`

#### Containers

You can call them as lightweight virtual machines. They basically package up your application/project and it's dependencies in a single unit which can be used by others to run project seamlessly without worrying about versions or exact services required.

Containers make sure that your application will run the same way regardless of where it's deployed.

##### Commands

| Description                      | Command                                       |
| -------------------------------- | --------------------------------------------- |
| list running containers          | `docker container ls`                         |
| list all containers              | `docker container ls -a`                      |
| to start a container             | `docker start <container_name>`               |
| to stop a container              | `docker stop <container_name>`                |
| execute command inside container | `docker exec <container_name> <command_name>` |

#### Images

Consider it as a blueprint or template which contains all the information that is required to create a container. Containers are just like empty boxes, images are the source which tells a container on what to run or do.

When thinking about **containers and images as a pair**, containers are isolated. So if you run same image on two different containers, they won't share their data. 

##### Commands

| Description                   | Command                       |
| ----------------------------- | ----------------------------- |
| Run image                     | `docker run <image_name>`     |
| Run image in interactive mode | `docker run -it <image_name>` |
| List images                   | `docker images`               |

#### Port Mapping

Helps map port of docker container to the host machine. Suppose you ran NodeJS server container, inside the container the server is running on port 8080, so if you try doing localhost:8080 on your host computer it will return the error "Not found". That why it is mandatory to map/expose your container port to host port to access the content.

It allows external systems to communicate with services running inside Docker containers

Syntax usually goes like - 

`docker run -p <host_port>:<container_port> <image_name>`

#### Dockerization of an application

To get started with dockerization of your application, first step is to create the image. You can do this by creating `Dockerfile` at the root of your project. 
Usually the Dockerfile goes like this - 
1. Define the base OS (ubuntu, window)
2. Install required dependencies in the container
3. Move/Copy over project files
4. Install node packages
5. Provide entry points - run command

Generate image by running `docker build -t <image_name> <dockerfile_path>`
You can further push your image to docker hub. 

While building images, Docker under the hood maintains a cache called "Layer caching", which helps us speed up the building process.

#### Docker compose

There might be situations in which to run a single project you need to run multiple containers. In this sitution, we make use of docker componse which helps us run multiple docker container as single unit.
You create a `docker-compose.yml` file. Inside that you define different services that you to start. Once the file is ready, you can execute `docker compose up` command.
