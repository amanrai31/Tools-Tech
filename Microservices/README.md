# Microservices

Backend is split into independently deployable, self-contained services, each responsible for a specific business capability (e.g., auth-service, user-service, payment-service, etc.). InShort =>  services with its own logic, config, Dockerfile, CI/CD pipeline.

Each service communicates with others via APIs (e.g., HTTP or gRPC). not through direct function calls

Each service can be deployed, updated, scaled, and monitored independently.


**NOTE : ** A frontend–backend architecture, which is not microservices. It's a standard client-server model, which is totally fine for a small app.

**Microservice can live in :** 

1. Monorepo (All microservice code in one repo. Used by Google, Uber, Jio, etc. Easier shared tooling, versioning, CI/CD.)
2. Polyrepo	(One repo per microservice. More isolated but harder to manage at large scale.)

-----


**Also we can deploy all services on a single server =>** Use Docker Compose to run all services in containers on the same server. => Usefull for small apps, development OR MVP (Simple, fast cheap BUT not ideal of large projects).  (Downs => 1. Can't scale individual services independently. 2. If one service crashes the server, everything may go down.)

#### Production-Grade deployment for microservices

- Each microservice is a Kubernetes Deployment + Service.

- Auto-scaling, rolling updates, zero-downtime deploys.

- Service discovery, config maps, secrets, health checks.

- Can run on EKS, AKS or on-prem clusters
