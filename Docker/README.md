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
3. --network(Connects container to a specific network.), -p (	--publish => Maps host port → container port (host:container).)
