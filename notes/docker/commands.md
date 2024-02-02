Start docker:

```sh
sudo systemctl start docker
```

List running containers:

```sh
docker ps
```

Stop a running container:

```sh
docker stop <container-name>
```

List all containers:

```sh
docker ps -a
```

Start an existing container (detached mode):

```sh
docker start <container-name>
```

Start an existing container (attached mode):

```sh
docker start -a <container-name>
```

Run a container in detached mode:

```sh
docker run -p <local-port>:<docker-port> -d <image-id>
```

Run a container in detached mode and remove it when stopped `--rm`:

```sh
docker run -p <local-port>:<docker-port> -d --rm <image-id>
```

Name & Tag Containers (`--name`):

```sh
docker run -p <local-port>:<container-port> -d --rm --name <my-container-name> <image-id>
```

Run a container in detached mode:

```sh
docker run -p <local-port>:<docker-port> -d <image-id>
```

Attach a detached running container:

```sh
docker attach <container-name>
```

Fetch the logs of a container:

```sh
docker logs <container-name>
```

Attach a detached running container with `logs` command:

```sh
docker logs -f <container-name>
```

Launch a container in interactive mode (keep standard input open even if not attached) `-i` and allocate a pseudo-TTY ("creates a terminal") `-t`:

```sh
docker run -it <image-id>
```

Start an existing container (attached and iterative mode):

```sh
docker start -a -i <container-name>
```

Copy files/folders into or out a running container:

```sh
docker cp <local-path-name>/. <container-name>:/<path-name>

docker cp dummy/. boring_vaughan:/test
```

```sh
docker cp <container-name>:/<path-name> <local-path-name>

docker cp boring_vaughan:/test dummy
```

Remove containers:

```sh
docker rm  <container-name-1> <container-name-2> ...
```

Build an image:

```sh
docker build .
```

Name and Tag an image:

```sh
docker build -t <name>:<tag> .
```

List all images:

```sh
docker images
```

Inspect all details about an image:

```sh
docker image inspect <image-id>
```

Remove images:

```sh
docker rmi  <image-id-1> <image-id-2> ...
```

Remove all unused images:

```sh
docker image prune
```

Remove all stopped containers in Docker:

```sh
docker container prune
```

Removing Anonymous Volumes

```sh
docker volume rm <volume-name>
```

```sh
docker volume prune
```

Creating a network:

```sh
docker network create <network-name>
```

Creating Container Networks:

```sh
docker run --network <network-name> ...
```

Inspect a container:

```sh
docker inspect <container-name>
```

Execute certain commands inside a running container:

```sh
docker exec -it <container-name> <command>
```

Run a container overwriting the default command:

```sh
docker run -it <image-name> <command>

docker run -it node npm init
```
