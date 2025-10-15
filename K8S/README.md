# CONTENT => Kubernetes(K8s)

Resource => https://www.youtube.com/watch?v=r2zuL9MW6wc&t=529s

Kubernetes => `Kubernetes = Container Orchestrator`. K8s is basically used to manage containerized apps(Docker images). K8s automatically `run`, `manage`, `scale`, `0-time deploy`, `restart`, and `monitor`. Also K8s is cloud agnostic i.e., cloud independent.

`In local/DEV ENV docker-compose manage the container, in PROD k8s manages the containers`. Docker-compose can not scale containers, can not auto-heal on crash, can not load-balance traffic, can not update without downtime(rolling updates). This is where K8s comes.

Google's Borg later evolved as K8s, and donated to `CNCF - Could native computing foundation` and made open-source.

### K8s cluster is made up of Master node & Worker node(s) =>

1. Control Plane (Master Node), node that runs cluster management components (Inside a linux machine or inside VM) =>
- `API Server`(kubectl)     => Entry point for any comm with K8S Cluster, Exposes Kubernetes API
- `Controller Manager`      => Ensures desired state, manages state of cluster
- `Scheduler`               => Decides where pods run, assigns node to newly created pods
- `etcd (cluster database)` => key-value store, has all cluster data
  
2. Worker mode(s) (nodes that actually run the pods) They are separate Linux or VM=>
- `kubelet`                 => Agent, which listens to KUBE-API and does as commanded (deploy OR destroy pods/containers etc.)
- `kube-proxy`              => Allow services to talk to other containers in other pod or in other node.
- `CRI - Container runtime` => Runs pods (usually one container per pod)

**NOTE :** In Small Local Clusters (like Docker Desktop or Minikube) there’s only one node that acts as both: `Control Plane (manages)` AND `Worker Node (runs pods)`
**NOTE :** Each pod has it's own IP.

#### Cluster info

- `kubectl cluster-info`
- `kubectl get nodes`
- `kubectl describe node <node-name>`
- `kubectl get all` 

  
#### Pods

- `kubectl get pods`                                      => List all pods
- `kubectl get pods -n <nameSpace>`                       => List system pods
- `kubectl describe pod <pod-name>`                       => Detailed pod info `(add nameSpace too)`
- `kubectl logs <pod-name>`                               => Show pod logs
- `kubectl exec -it <pod-name> -- /bin/bash`              => Open shell inside a running pod
- `kubectl delete pod <pod-name>`                         => Delete pod

#### Deployments

- `kubectl get deployments`
- `kubectl describe deployment <name>`
- `kubectl rollout status deployment/<name>`
- `kubectl rollout undo deployment/<name>`
- `kubectl apply -f deployment.yaml`                     => Create from yaml
- `kubectl delete deployment <name>`                     => delete deployment

#### Services

- `kubectl get svc`
- `kubectl describe svc <name>`
- `kubectl port-forward svc/<service-name> 8080:80`
- `kubectl delete svc <name>`

#### Namespace

- `kubectl get ns`
- `kubectl create ns dev`
- `kubectl delete ns dev`



In prod, the masterNode & workerNode usually runs on multiple nodes that span across several data center zones.


------

## HandsOn

- Containerize your app (Make Dockerfile - Declare all steps to build image)
- build image `docker build -t <tagname:version>`
- Push to dockerHub
- Now deploy app on k8s cluster using `k8s deployment` - Create `deployment object in .yaml file` 
- the yaml file has all `desired state` for your app and the app's image
  
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80

```
