# CONTENT => Kubernetes(K8s)

Kubernetes => `Kubernetes = Container Orchestrator`. K8s is basically used to manage containerized apps(Docker images). K8s automatically run, manage, scale, deploy, restart, and monitor. Also K8s is cloud agnostic i.e., cloud independent.

Google's Borg later evolved as K8s, and donated to `CNCF - Could native computing foundation` and made open-source.

### K8s cluster has 2 main components =>

1. Control Plane (Master Node), node that runs cluster management components  =>
- `API Server`              => Entry point, Exposes Kubernetes API
- `Controller Manager`,     => Ensures desired state
- `Scheduler`,              => Decides where pods run
- `etcd (cluster database)` => Stores cluster state
  
2. Worker modes (nodes that actually run the pods) => `kubelet`, `kube-proxy`, `CRI => pods(containers)`

**NOTE :** In Small Local Clusters (like Docker Desktop or Minikube) there’s only one node that acts as both: `Control Plane (manages)` AND `Worker Node (runs pods)`

#### Cluster info

- `kubectl cluster-info`
- `kubectl get nodes`
- `kubectl describe node <node-name>`
- `kubectl get all` 

  
#### Pods

- `kubectl get pods`                                      => List all pods
- `kubectl get pods -n kube-system`                       => List system pods
- `kubectl describe pod <pod-name>`                       => Detailed pod info
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



In prod, the control plane usually runs on multiple nodes that span across several data center zones
