1. Play with public images.
2. Create docker image for your app.
3. Lunch DB as docker container & let your container talk to it.
4. Create microservice container and let them talk to each other.
5. Run docker container in cloud like AWS/Azure.

---

Think docker image as `class` & docker containers as `objects`

Flags =>
1. -d(--detach),-rm (remove container after it stops),-h(--hostname)
2. -e (--env => environment), -v (Mounts a volume (binds host & container storage)), --restart (Defines the restart policy (e.g., always, on-failure).)
3. --network(Connects container to a specific network.), -p (	--publish => Maps host port → container port (host:container).), --hostname(	Sets a custom hostname for the container.)
4. -f (--file => Specifies a custom Dockerfile (docker build).), --pull (	Always pulls the latest base image during build)
5. -a(-all => Show all containers, even stopped ones.), -q(quiet => Show only container IDs.), --name (Assigns a custom name to the container.)


