# CONTENT => Docker


Docker is used to containerize apps thus giving appa an isolated ENV which is not machine-specific. `Think docker image as CLASS & docker containers as OBJECTS/Runtime Instance` OR `Think image (as OS) which can be used by many containers (Machines)`.

**NEED =>** Solves the problem of "IT WORKS ON MY MACHINE" by giving the apps an isolated ENV. Docker `Packages our app + environment -> into one portable image`

**Docker image** => It is like a snapshot or template that defines what your app and its environment look like. It contains your `app code`, `runtime(node,java etc)`, `Libraries / dependencies`, `Environment variables`, `OS files (like Ubuntu or Alpine base)`.

**Docker container** => Similar to a VM (Just uses the host's kernel & have process-level isolation). You can make as many containers for same image. See image for more clarity (We will discuss later).

Flags =>
1. `-d` (--detach) | `-rm` (remove container after it stops) | `-h` (--hostname)
2. `-e` (--env => environment) | `-v` (Mounts a volume (binds host & container storage)) | `--restart` (Defines the restart policy e.g., always, on-failure)
3. `--network` (Connects container to a specific network.) | `-p` (--publish => Maps host port → container port (host:container)) | `--hostname` (Sets a custom hostname for the container.)
4. `-f` (--file => Specifies a custom Dockerfile (docker build)) | `--pull` (	Always pulls the latest base image during build)
5. `-a` (-all => Show all containers, even stopped ones.) | `-q` (quiet => Show only container IDs.) | `--name` (Assigns a custom name to the container.)

---

DOCKER => 1. installation, 2. create Docker file, 3. create Docker image, 4. running containers, 5. pre-defined images, 6. Docker Hub, 7. Docker volume & network, 8. Docker compose.

1. Installation

- install Docker Engine (Dockerd + CLI + API)        (local)
- install Docker Desktop GUI                         (local)
- Docker Hub                                         (remote access => push your images here)

```bash sudo apt install ./docker-desktop-amd64.deb``` => installs both Docker engine & Docker desktop

We can install Linux in docker world(inside Docker container) instead of installing it in virtualBox; Docker comes with its own virtual env. We can install mongo,redis etc. in docker way so they face same conditions & bugs in local ENV as well as in PROD ENV.

- `docker engine` => `Docker Daemon (dockerd)` + `Docker CLI (docker)` + `REST API`.
- `Docker daemon (dockerd)` => listens for Docker API requests and manages containers, images, networks, and volumes.
- `Docker engine APIs` => Controls the Docker daemon (dockerd) on your machine. Supports both REST API & CLI commands
- `Docker Hub APIs` => Interacts with Docker Hub (hub.docker.com). Used to search, pull, and manage images on Docker Hub. Requires authentication for private repositories.
- `Registry APIs` => Registry is a host that stores repos => Manages images in a private Docker registry (e.g., Docker hub, AWS ECR, Azure ACR, Harbor, GitHub Container Registry). Used to store and distribute private container images.

-----

 **NOTE :** Docker images are built from multiple read-only layers. Each Dockerfile command (RUN, COPY, etc.) creates a new layer. Layers are cached and reused to speed up builds. The final running container has a writable top layer.

 ``` docker pull <image-name> ``` => pulls image

 ``` docker image ls ``` => list of images

 ``` docker run -e POSTGRES_PASSWORD=mysecretepassword -d postgres ``` => To run docker container, the postgres here is image name, we can add version here also.

 ```docker run --name <container-name> -e MONGO_PASSWORD=mypassword -d mongo``` 
 
 ``` docker ps ``` => check running containers. ```docker ps -a``` => Checks all running containers. Here ps stands for process status, similar to linux.

 ```docker stop <container-name>``` || ```docker stop <container-id>```

 ``` docker stop $(docker ps -a) ``` => stop all container

 ```docker container prune``` => removes all stopped containers.

 **Diff b/w docker & VM =>** Docker do not have kernel, it uses host's kernel (VM requires full OS per VM). Docker users container(VM uses virtualized OS). Docker has process level isolation(VM has full OS isolation), docker encapsulate app instead of whole machine

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
Now suppose we have 2 diff versions of same service (e.g. mongo) but by default they run on same port (e.g. 27017), so they will create conflict.

**PORT assign** 

``` sh
docker run -d --name mongo1 -p 4000:27017 mongo
 ```

``` sh
docker run -d --name mongo2 -p 5000:27017 mongo
 ```

Here mongo1 & mongo2 are container name(2 diff containers) of mongo(of same image)

`docker run -d -p 8025:8025 -p 1025:1025 mailhog/mailhog` => Suppose an image(app) has multiple ports  

---

 ### Docker compose

Commands in CLI can be too long e.g.

```sh
docker run -d \
--name mongo-express \
--net mongo-express \
-p 8081:8081 \
-e MONGODB_ADMINUSERNAME = admin \
-e MONGODB_ADMINPASSWORD = password \
-e MONGODB_SERVER = mongodb \
mongo-express
```

Container for mongo-express application. ( \ => changes line in CLI)

To avoid such complex command - WE have Docker Compose

Docker compose is a tool that allow you to define & run multiple docker container as a single application. Instead of running individual `docker run` commands for each container, you can manage everything using a single YAML file (docker-compose.yml). `Indentation matters in yaml file.`

Instead of manually starting a database, backend, and frontend separately, Docker Compose lets you define everything in one file and launch all services together.

- Run `docker-compose up` to start everything || `docker compose -f <fileName> up`
- Kill `docker compose -f <fileName> down`

#### Key feature 

1. dependsOn => ensures services start in order (e.g., db before backend).
2. volumes =>  Maps files from the host system into the container.
3. ports => Exposes container ports to the host. (All services/containers inside a docker-compose is by default on the same network)

**NOTE :** Docker Compose is great for local development(Used to run multi-container Docker applications on a single machine), but for production use `Kubernetes` for large-scale deployments(Used to run and manage containerized applications across a cluster of multiple machines (servers or nodes))


```yaml
version: '3.8'

services:
  backend:
    image: node:18
    container_name: my-backend
    working_dir: /app
    volumes:
      - .:/app
    ports:
      - "3000:3000"
    depends_on:
      - db

  db:
    image: postgres:15
    container_name: my-database
    environment:
      POSTGRES_USER: myuser
      POSTGRES_PASSWORD: mypassword
      POSTGRES_DB: mydb
    ports:
      - "5432:5432"
```

---

#### Docker volume

Allows data to persist even after a container stops or is removed (data survives across container restarts/deletions). Used mainly to store DB, logs & config files.

Managed by docker, stored in ```/var/lib/docker/volumes/``` - Docker manages volumes on the host machine (outside the container).

Deleting a container does NOT delete the volume, so data persists. A new container using the same volume can access old data.

`bash docker run -d --name mydb -v my_pgdata:/var/lib/postgresql/data postgres` => Data stored in my_pgdata(lives on the host machine)

---

#### Docker file

A Dockerfile is a script containing instructions to build a Docker image (defines how a container should create, what dependencies to install,what command to run when container starts etc). It is used to create custom images.

``` sh
# Use an official Node.js image as the base
FROM node:18

# Set app as working directory inside the container
WORKDIR /app

# Copy package.json and install dependencies
COPY package.json ./
RUN npm install

# Copy the rest/all of the application files into the container
COPY . .

# Expose port 3000 for the application
EXPOSE 3000

# Define the command to run the app when container starts
CMD ["node", "server.js"]
```
1. Create docker file, put all info inside.
2. Build image => ``` docker build -t <your-dockerhub-username>/<image-name>:<tag>``` => ```docker build -t amanrai31/my-app:latest```
3. Check by running a container ``` docker container run -d -p 3000:4000 my-app:latest```
4. push the custom image to hub ```docker push <your-dockerhub-username>/my-app:latest``` => ```docker push amanrai31/my-app:latest```

``` docker pull amanrai/myapp:latest``` => pull image 
``` docker run -p 3000:3000 amanrai/myapp:latest``` => run a container for that image (you can name this container, you directly run this command this will pull & run both)

**NOTE =>** We can bind only one container to our local port. Make multiple container and bind with diff ports in local machine, but we can use same port inside different containers as containers are isolated ENV but we need diff port on our local machine.

=> Learn abot configuration management tools like chef, ansible,puppet - they use config as code but they require knowledge about OS & hardware. What they solve =>
Diff system config, ; missing files, hardware or other props.


-----

1. Play with public images.
2. Create docker image for your app.
3. Lunch DB as docker container & let your container talk to it.
4. Create microservice container and let them talk to each other.
5. Run docker container in cloud like AWS/Azure.






