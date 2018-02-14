# Docker Cheatsheet

## Linux Installation
```
curl -sSL https://get.docker.com/ | sh
```

## Networking
### Types
* Bridge (default)
* Host
* None

`docker run --net=<type>`

## Dockerfile
### Instructions
* `FROM <image name>`: Specify base image
* `RUN <command>`: Run a command
* `CMD [<command>, <arg1>, ...]`: Run a command (can only have one in a Dockerfile)
* `LABEL <key>=<value>`: Adding meta data to image
* `MAINTAINER <name>`: Sets the author of generated image
* `ADD <src> <dest>`: Adds new files, also from URL
* `COPY <src> <dest>`: Copy new files
* `ENV <key> <value>`: env variable
* `EXPOSE <port>`: Opening a port
* `ENTRYPOINT [<command>, <arg1>, ...]`: Command to run when docker executes
* `LABEL`
* `USER`
* `WORKDIR`
* `VOLUME`
* `STOPSIGNAL`

### Arguments
`ARG NAME=<optional-value>`

`docker build --build-arg NAME=value`


## Useful commands

### Volumes
To mount a volume on the container

`docker run -v /path`

`docker run -v <host/path>:<container/path>`

### Seeing the output
`docker logs <container>`

### Name a container
`docker run --name=<name> <image-name>`

### Build
`docker build -t <tag> .`

### Tagging
`docker tag <image-id> <username>/<image name>:<version or tag>`

### Push
`docker push <image name>`

### Remove image
`docker rmi -f <image id>`

### Attach to stopped container

`docker commit $STOPPED_CONTAINER user/test_image`

### Start/run with a different entry point (/bin/bash)
`docker run -it --entrypoint=/bin/bash user/test_image`

`docker exec -it <id or name> /bin/bash`

