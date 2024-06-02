# Docker cheat sheet

### Checking Docker is installed

`$ docker info`

## Basic commands for docker container

### The docker run command

`$ docker run -i -t ubuntu /bin/bash`

### Listing Docker containers

`$ docker ps -a`

### Naming a container

`$ docker run --name bob_the_container -i -t ubuntu /bin/bash`

### Starting a stopped container

`$ docker start bob_the_container`

### Attaching to a running container

`$ docker attach bob_the_container`

### Stopping the running Docker container

`$ docker stop bob_the_container`

### Deleting a container

`$ docker rm bob_the_container`

### Deleting all containers

`` $ docker rm -f `sudo docker ps -a -q`  ``

## Refference:

- [The Docker Book by James Turnbull](https://dockerbook.com/)
