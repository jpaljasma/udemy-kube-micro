
# Docker Quickstart

### Pull the image

`docker image pull richardchesterwood/k8s-fleetman-webapp-angular:release0-5-arm64`

### Verify the image exists

```
% docker image ls | grep release0-5-arm64

richardchesterwood/k8s-fleetman-webapp-angular   release0-5-arm64                                                             01706f15bc22   13 months ago   21MB
```

### Run the container

Note that if you do the `docker container run` on the image that have not been downloaded yet (and does not appear in the `docker image list` output), it will be automatically pulled.

```
docker container run -p 8080:80 -d richardchesterwood/k8s-fleetman-webapp-angular:release0-5-arm64
```

#### Command-line parameters

`-d`

Runs the container int he background

`-p exposed-port:internal-port`

* **exposed-port** is a port that's visible to the outside world.

* **internal-port** internally, the traffic is being routed to a port where the service is being run locally.

As a result, the container will run and is accessible via http://localhost:8080/

We can verify that the container is running:

```bash
% docker ps

CONTAINER ID   IMAGE                                                             COMMAND                  CREATED         STATUS         PORTS                  NAMES
9dc92870bd3d   richardchesterwood/k8s-fleetman-webapp-angular:release0-5-arm64   "nginx -g 'daemon of…"   5 seconds ago   Up 4 seconds   0.0.0.0:8080->80/tcp   practical_volhard
```

Finally, we can stop the container by issuing

```bash
% docker container stop 9dc
```

That `9dc` represent a 3-character prefix of the container id. You don't need to pass full ID to a stop command, just enough to identify the unique id in the list.

And optionally, if we are interested in saving some disk space, we can issue `docker container rm` command to delete the container

```bash
% docker container rm 9dc
```