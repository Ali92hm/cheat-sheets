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

### Best practices
#### Use `.dockerignore` file
This prevents unnecessary files in docker directory to be passed to the docker engine.

#### Use multi-stage builds
Multi-stage builds result in slimmer docker files.

#### LABEL
An image can have more than one label. Prior to Docker 1.10, it was recommended to combine all labels into a single LABEL instruction, to prevent extra layers from being created. This is no longer necessary, but combining labels is still supported.

```
LABEL com.example.version="0.0.1-beta"
LABEL vendor="ACME Incorporated"
LABEL com.example.release-date="2015-02-12"
LABEL com.example.version.is-production=""
```

#### Sort multi-line arguments
* Never use `apt-get upgrade`. Updating the package list is enough.
* Remove the `apt-get` list after installing the packages

```
RUN apt-get update && apt-get install -y \
  bzr \
  cvs \
  git \
  mercurial \
  subversion \
  && rm -rf /var/lib/apt/lists/*
```
> Note: The official Debian and Ubuntu images automatically run apt-get clean, so explicit invocation is not required.

#### Use CMD
Always use CMD in the form below

```
CMD [“executable”, “param1”, “param2”…]
```

#### ENV
Use env to version everything. 

```
ENV PG_MAJOR 9.3
ENV PG_VERSION 9.3.4
RUN curl -SL http://example.com/postgres-$PG_VERSION.tar.xz | tar -xJC /usr/src/postgress && …
ENV PATH /usr/local/postgres-$PG_MAJOR/bin:$PATH
```

#### ADD or COPY
* Always use `COPY`
* Use `ADD` to extract `.tar` files or remote URL support.

#### WORKDIR
For clarity and reliability, you should always use absolute paths for your `WORKDIR`

