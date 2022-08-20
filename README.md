# learning-kubernetes
## Main components
- node: physical or virtual machine running stuff...
- pod: Abstraction layer to a container. Could be docker or something else. Usually one pod per container. Each pod has its own ip address to communicate with other pods. New ip when restart.
- service: Communication layer for pods. Has static ip. When pod dies, the service still remains. It also works as a load balancer for Replications (multiple node clones)
- ingress: External communication layer. E.g. secure domain. This is on top of the service.
- ConfigMap: External configuration of your application. Not for credentials!
- Secret: Like ConfigMap but for secret data. In base64
- Volumes: Data Storage local or remote. Outside of the kubernetes cluster. K8 doesn't manage Storage Data
- Deployment: Blueprint for pods. Abstraction layer on top of Pods. Good for replication. You defione Deployments and not single pods. Cannot replicate Stateful  pods like DB because of IO to the data storage
- StatefulSet: Abstraction layer for stateful Apps or Databases. 
- ! Important ! DB are often hosted outside k8s cluster because configuration inside StatefulSet is difficult!

## Architecture
- each node has multiple pods
- every node must have min 3 processes
  - container runtime: e.g. docker
  - kubelets: kubernetes process. interaction with node and pod
  - kube proxy: forwards requests for the services.
- Master Nodes: Controls and manages the cluster and worker nodes. Needs 4 processes
  - Api Server: Like a cluster gateway. Also Auth gate keeper.
    - Request > Api Server > validation > Forward to other processes
  - Scheduler: Intelligent manager. Where to put a new Pod. 
  - Controller manager: Detect state changes inside the cluster. E.g. pod dies, inform Scheduler to restart
  - etcd: Key / Value store. Cluster Brain! Stores information about the cluster like currently running processes etc. Not the application data. 
- Sample Cluster Setup:
  - 2 Master, 3 Node

## minikube & kubectl
- minikube: Local cluster setup. Master and node processes on one machine
  - creates virtual box
  - runs node inside vbox
  - 1 node k8s cluster
- kubectl: cli tool for communicatin with a cluster
