Create a new repository on Docker Hub: `dockerhub-account/example-name`

Build an image locally (remember to add a `.dockerignore`)

```sh
docker build -t <image-example-name> .
```

Rename it with `tag` command:

```sh
docker tag <image-example-name> <dockerhub-account/example-name>
```

Login into Docker Hub:

```sh
docker login
```

Push it to docker hub

```sh
docker push <dockerhub-account/example-name>

```

Pull it from the remote server

```sh
docker run -d -rm -p <host-port>:<container-port> <dockerhub-account/example-name>
```
