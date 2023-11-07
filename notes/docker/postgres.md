# Docker PostgreSQL Container Initialization Script

- [Docker PostgreSQL Tutorial with Persistent Data](https://youtu.be/G3gnMSyX-XM?si=3BlD1SeZAOLdjB6L)

Docker command to start a PostgreSQL database server inside a Docker container.

```sh
docker run -p 5432:5432 -d \
    -e POSTGRES_USER=<db-user> \
    -e POSTGRES_PASSWORD=<password> \
    -e POSTGRES_DB=<db-name> \
    -v "$(pwd)/migrations":/docker-entrypoint-initdb.d \
    -v <volume-name>:/var/lib/postgresql/data \
    postgres
```

## Command Breakdown

- `docker run`: This command is used to create and start a Docker container.

- `-p 5432:5432`: This option maps the container's port 5432 to the host's port 5432. This is necessary for accessing PostgreSQL from outside the Docker container, as 5432 is the default port for PostgreSQL.

- `-d`: Runs the container in detached mode. This means that the container starts up and runs in the background, allowing you to continue using the terminal.

- `-e POSTGRES_USER=<db-user>`: This flag sets an environment variable in the container. Replace `<db-user>` with the desired username for the PostgreSQL superuser.

- `-e POSTGRES_PASSWORD=<password>`: Sets an environment variable for the superuser password. Replace `<password>` with a secure password of your choosing.

- `-e POSTGRES_DB=<db-name>`: Specifies the default database to be created when the container starts. Replace `<db-name>` with the name of the database you want to create.

- `-v "$(pwd)/migrations":/docker-entrypoint-initdb.d`: Binds a volume from the host system to the container. This mounts the `migrations` directory from the current working directory on the host to `/docker-entrypoint-initdb.d` in the container. PostgreSQL will execute any `.sql` or `.sh` scripts found in this directory upon startup.

- `-v <volume-name>:/var/lib/postgresql/data`: This binds a persistent volume to the container at `/var/lib/postgresql/data`. Replace `<volume-name>` with the name of the volume where you want to store the database data. This ensures that the data persists even after the container is stopped or deleted.

- `postgres`: This is the name of the Docker image to use, which in this case is the official PostgreSQL image from Docker Hub.
