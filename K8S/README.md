# CONTENT => K8S

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
- `kubectl exec -it <pod-name> -- /bin/bash`              => Open shell inside pod
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

