### Docker commands

Get a list of running containers:

docker ps

Get a list of running and non-running containers:

docker ps -a

Run a container:

docker run —options <container name>

Stop a container:

docker stop

Start a container:

docker start

Start a container in detached mode:

docker run -d

Delete a container:

docker rm

Get a list of images:

docker images

Bind to a port:

docker run -p<host port>:<container port> // i.e. docker run -p4443:443

Get a list of docker networks:

docker network ls

Get a shell into container:

docker exec -it <name> sh

Docker volume locations:

/var/lib/docker/volumes
