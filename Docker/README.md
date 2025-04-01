1. Play with public images.
2. Create docker image for your app.
3. Lunch DB as docker container & let your container talk to it.
4. Create microservice container and let them talk to each other.
5. Run docker container in cloud like AWS/Azure.

---

**Think docker image as `class` & docker containers as `objects`**

Flags =>
1. -d(--detach),-rm (remove container after it stops),-h(--hostname)
2. -e (--env => environment), -v (Mounts a volume (binds host & container storage)), --restart (Defines the restart policy (e.g., always, on-failure).)
3. --network(Connects container to a specific network.), -p (	--publish => Maps host port → container port (host:container).), --hostname(	Sets a custom hostname for the container.)
4. -f (--file => Specifies a custom Dockerfile (docker build).), --pull (	Always pulls the latest base image during build)
5. -a(-all => Show all containers, even stopped ones.), -q(quiet => Show only container IDs.), --name (Assigns a custom name to the container.)

---

DOCKER => 1.installtion, 2. create docker file, 3. create docker image, 4. running containers, 5.pre-defined images, 6. docker hub, 7. docker volume & network, 8. Docker compose.

1. Installation

- install docker engine (local)
- install docker desktop (local)
- Docker Hub - (remote access => push your images here)

```bash sudo apt install ./docker-desktop-amd64.deb``` => installs both Docker engine & Docker desktop

We can install Linux in docker world instead of installing it in virtualBox; Docker comes with its own virtual env. We can install mongo,redis etc. in docker way so they face same conditions & bugs in local ENV as well as in PROD ENV.

- Docker engine APIs => Controls the Docker daemon (dockerd) on your machine. Used to manage containers, images, networks, and volumes programmatically. Supports both REST API & CLI commands
- Docker Hub APIs => Interacts with Docker Hub (hub.docker.com). Used to search, pull, and manage images on Docker Hub. Requires authentication for private repositories.
- Resistry APIs => Manages images in a private Docker registry (e.g., AWS ECR, Azure ACR, Harbor, GitHub Container Registry). Used to store and distribute private container images.

---

 **NOTE :** Docker images are built from multiple read-only layers. Each Dockerfile command (RUN, COPY, etc.) creates a new layer. Layers are cached and reused to speed up builds. The final running container has a writable top layer.

 ``` docker pull <image-name> ``` => pulls image

 ``` docker image ls ``` => list of images

 ``` docker run -e POSTGRES_PASSWORD=mysecretepassword -d postgres ``` => To run docker container, the postgres here is image name, we can add version here also.

 ```docker run --name <container-name> -e MONGO_PASSWORD=mypassword -d mongo``` 
 
 ``` docker ps ``` => check running containers. ```docker ps -a``` => Checks all running containers. Here ps stands for proccess status, similiar to linux.

 ```docker stop <container-name>``` || ```docker stop <container-id>```

 ```docker container prune``` => removes all stopped containers.

 **Diff b/w docker & VM =>** Docker do not have kernel, it uses host's kernel (VM requires full OS per VM). Docker users container(VM uses virtualized OS). Docker has process level isolation(VM has full OS isolation)

---

From one image we can create multiple containers with diffrenet name. Assign diff port for diff containers.
When we create/need diff container with same image?
1. scalabilty & load balancing - When handling high traffic, you run multiple instances of the same service behind a load balancer.
2. Different Configurations for the Same App(Microservices Architecture) - You can run the same image but with different environment variables or configurations OR with diff role.

```sh
docker run -d --name frontend-dev -e NODE_ENV=development myfrontend
docker run -d --name frontend-prod -e NODE_ENV=production myfrontend
```
- Both containers use the same image, but one runs in dev mode and the other in production mode.

```sh
docker run -d --name db-master postgres
docker run -d --name db-replica1 postgres
docker run -d --name db-replica2 postgres
```

- The same PostgreSQL image is used, but each container has a different role.

3. Rolling Updates (Zero Downtime Deployment)
To update a service without downtime, you create a new container with the updated version before removing the old one.

```sh
docker run -d --name api-server myapp
docker run -d --name worker-service myapp
```


