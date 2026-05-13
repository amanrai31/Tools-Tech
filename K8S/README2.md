First understand the BIG picture

Your cluster is basically:

```
Big Machine Cluster
    └── Kubernetes
            └── Runs applications
```

Now Kubernetes needs ways to:

- organize apps
- run apps
- restart crashed apps
- store data
- expose networking
- scale apps

That is why all these concepts exist.

1. Namespace → Folder/Room

A Namespace is just a logical grouping.

Think:

Namespace = Folder

Example:

ocis
monitoring
default
kube-system

Inside a namespace you can have:

Deployments
Pods
Services
PVCs
Secrets
ConfigMaps

Example:

Namespace: ocis
    ├── Deployment: search
    ├── Deployment: frontend
    ├── Pod: search-xxx
    ├── Service: search
    └── PVC: search-data

So YES:

✅ Deployments live INSIDE namespaces.

They do NOT exist independently.

2. Deployment → App Manager

Deployment says:

"I want 1/2/3 copies of this app always running."

Example:

Deployment: search

This deployment manages pods.

If pod crashes:

Deployment recreates it automatically

Real chain:

Deployment
    ↓
ReplicaSet
    ↓
Pods

You usually interact only with Deployment.

3. Pod → Actual Running Container

Pod is the REAL thing running.

Inside pod:

Container (Docker container)

Example:

search-6d84fc5464-wgtzm

This is a pod.

Inside it your OCIS search service is running.

4. Service → Stable Network Name

Pods die and recreate.

So pod IP changes.

Service gives stable access.

Example:

Service: search

Other apps call:

http://search

instead of pod IP.

5. PVC → Persistent Disk Storage

PVC means:

Persistent Volume Claim

Think:

"Please give me storage/disk."

Without PVC:

Pod dies → data lost

With PVC:

Pod dies → data survives

Example:

databases
Elasticsearch
uploaded files

need PVC.

6. Helm Release → Installed App Instance

This confuses almost everyone.

Helm is basically:

npm install for Kubernetes

A Helm Chart is a template.

When you install it:

helm install ocis

Kubernetes creates:

deployments
services
pods
PVCs
secrets

That installed instance is called:

Release

Example:

Release Name: ocis

So:

helm install ocis ./chart

means:

Install chart instance named "ocis"
Your actual system

You likely have:

Namespace: ocis

Inside it:

Release: ocis

That release created:

Deployments:
    search
    frontend
    graph
    gateway
    users

Those deployments created:

Pods:
    search-xxx
    frontend-xxx

Some of them may use:

PVCs

for storage.

Full Mental Model
```
Cluster
   └── Namespace (ocis)
           ├── Helm Release (ocis)
           │
           ├── Deployment (search)
           │       └── Pod
           │
           ├── Deployment (frontend)
           │       └── Pod
           │
           ├── Service (search)
           ├── PVC (search-data)
           └── Secrets / ConfigMaps
```

## MOST IMPORTANT THING

Kubernetes is mostly:

Desired State Management

You tell it:

"I want 1 search pod running"

Kubernetes continuously ensures it.

If pod dies:

Kubernetes recreates it
Commands mapping
See namespaces
```
kubectl get ns
```
See deployments in namespace
```
kubectl -n ocis get deployments
```
See pods
```
kubectl -n ocis get pods
```
See services
```
kubectl -n ocis get svc
```
See PVCs
```
kubectl -n ocis get pvc
```
See Helm releases
```
helm list -n ocis
```

Once this hierarchy clicks, 70% of Kubernetes becomes understandable.
