# Docker
Get started with docker and containerization


NOTES :

1)Docker is a platform for developers and sysadmins to develop, deploy, and run applications with containers. 
2)The use of Linux containers to deploy applications is called containerization
3) An image is an executable package that includes everything needed to run an application--the code, a runtime, libraries, environment variables, and configuration files.
4)A container is a runtime instance of an image--what the image becomes in memory when executed (that is, an image with state, or a user process). 

** List of running containers :- docker ps

5) Containers and virtual machines
  A container runs natively on Linux and shares the kernel of the host machine with other containers. 
  It runs a discrete process, taking no more memory than any other executable, making it lightweight.
  By contrast, a virtual machine (VM) runs a full-blown “guest” operating system with virtual access to host resources through a hypervisor.
  In general, VMs provide an environment with more resources than most applications need.
  
  docker --version
  docker version
  docker info 
  docker run hello-world
  
  *** 
  To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
   
   docker images 
   docker image ls
   docker container ls --all --> container (spawned by the image) which exits after displaying its message. If it were still running, you would not need the --all option:
   
   Recap and cheat sheet
## List Docker CLI commands
docker
docker container --help

## Display Docker version and info
docker --version
docker version
docker info

## Execute Docker image
docker run hello-world

## List Docker images
docker image ls

## List Docker containers (running, all, all in quiet mode)
docker container ls
docker container ls --all
docker container ls -aq


## development environment 

If you want to write a python app, you can just grab a portable Python runtime as an image, no installation necessary.
Then, your build can include the base Python image right alongside your app code, ensuring that your app, its dependencies, and the runtime, all travel together.
These portable images are defined by something called a Dockerfile.


Define a container with Dockerfile
Dockerfile defines what goes on in the environment inside your container.
Access to resources like networking interfaces and disk drives is virtualized inside this environment,
which is isolated from the rest of your system, so you need to map ports to the outside world, and be specific about what files you want to “copy in” to that environment.

## build the app 
$ ls
Dockerfile		app.py			requirements.txt
docker build --tag=finaldocker .
can mention the version :- --tag=finaldocker:v0.0.1.

## Run the app
Run the app, mapping your machine’s port 4000 to the container’s published port 80 using -p:

docker run -p 4000:80 finaldocker  --> http://localhost:4000/

you mapped port 80 of that container to 4000

use docker container stop to end the process, using the CONTAINER ID, like so:

docker container stop 1fa4ab2cf395

## uploading a built image
$ docker login / $ docker login --username yourusername

The notation for associating a local image with a repository on a registry is username/repository:tag
This puts the image in the get-started repository and tags it as part2.
docker tag image username/repository:tag
For example:
$ docker tag finaldocker yourusername/get-started:part2

Run docker image ls to see your newly tagged image.

## Publish the image
$ docker push username/repository:tag --> docker push shitaljumbad/get-started:part2

From now on, you can use docker run and run your app on any machine with this command:

docker run -p 4000:80 username/repository:tag

If the image isn’t available locally on the machine, Docker pulls it from the repository.

No matter where docker run executes, it pulls your image, along with Python and all the dependencies from requirements.txt, and runs your code. It all travels together in a neat little package, and you don’t need to install anything on the host machine for Docker to run it.



