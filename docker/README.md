# Docker Cheat Sheet

## Linux Installation
```
curl -sSL https://get.docker.com/ | sh
```

## Useful commands

### Build
```
docker build -t <tag> .
```

### Build with arguments
```
docker build --build-arg NAME=value
```

### Tagging
```
docker tag <image-id> <username>/<image name>:<version or tag>
```

### Push
```
docker push <image name>
```

### Running a container interactive mode
```
docker run -it <image name>
```

### Running a container daemon mode
```
docker run -d <image name>
```

### Running a container with name
```
docker run --name=<name> <image-name>
```

### Run container with a networking type
```
docker run --net=<type>
```

### Exposing ports
```
docker run -p <image-name> # assigns random ports to the EXPOSE ports in dockerfile
docker run -p $HOSTPORT:$CONTAINERPORT <image-name>
```

### Mounting Volumes
```
docker run -v /path
docker run -v <host/path>:<container/path>
```

### Attach to stopped container
```
docker commit $STOPPED_CONTAINER user/test_image
```

### Start/run with a different entry point (/bin/bash)
```
docker run -it --entrypoint=/bin/bash user/test_image
docker exec -it <id or name> /bin/bash
```


### Getting Logs
```
docker logs <container>
docker container logs <container> -f # follow logs
```

### Remove image
```
docker rmi -f <image id>
```

### Remove all stopped containers
```
docker rm -f $(docker ps -aq)
```

### Stop all containers
```
docker stop $(docker ps -q)
```

### Remove all images
```
docker rmi -f $(docker images -q)
```

### Remove everything
```
docker system prune -af
```

## Starting and Stopping

* `docker start` starts a container so it is running.
* `docker stop` stops a running container.
* `docker restart` stops and starts a container.
* `docker pause` pauses a running container, "freezing" it in place.
* `docker unpause` will unpause a running container.
* `docker wait` blocks until running container stops.
* `docker kill` sends a SIGKILL to a running container.
* `docker attach` will connect to a running container.

## Getting Info

* `docker ps` shows running containers.
* `docker logs` gets logs from container.
* `docker inspect` looks at all the info on a container
* `docker events` gets events from container.
* `docker port` shows public facing port of container.
* `docker top` shows running processes in container.
* `docker stats` shows containers' resource usage statistics.
* `docker diff` shows changed files in the container's FS.

## Networking
### Types
* Bridge (default)
* Host: Uses host stack
* None: no network connection

## Dockerfile
### Instructions
* `.dockerignore`
* `FROM <imagename>` Sets the Base Image for subsequent instructions.
* `RUN [<command>]` Execute any commands in a new layer on top of the current image and commit the results.
* `CMD [<command>]` Provide defaults for an executing container (overridable)
* `ENTRYPOINT [<command>]` Configures a container that will run as an executable. (non-overridable)
* `EXPOSE <port>` Informs Docker that the container listens on the specified network ports at runtime (does not expose them)
* `ENV <name>=<value>` Sets environment variable.
* `LABEL <key>=<value>` Apply key/value metadata to your images, containers, or daemons.
* `ADD <src> <dest>` Copies new files, directories or remote file to container.  Invalidates caches. Avoid `ADD` and use `COPY` instead.
* `COPY <src> <dest>` Copies new files or directories to container.
* `VOLUME <path>` Creates a mount point for externally mounted volumes or other containers.
* `USER <user>[:<group>]` Sets the user name for following RUN / CMD / ENTRYPOINT commands.
* `WORKDIR <dir>` Sets the working directory.
* `ARG <name>=<value>` Defines a build-time variable.
* `ONBUILD [<instruction>]` Adds a trigger instruction when the image is used as the base for another build.
* `STOPSIGNAL <signal>` Sets the system call signal that will be sent to the container to exit.


### Examples
```
FROM node:carbon-alpine

LABEL MAINTAINER <email>

# Setting the working directory
WORKDIR /usr/src/

# Setting the env variables for npm install and execution
ENV NODE_ENV=production
EXPOSE 3000

# Copy files and installing dependencies
COPY . .
RUN npm install

# Running the application
CMD npm start
```
