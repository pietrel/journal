# Kubernetes Architecture

Kubernetes architecture is based on a master-slave model. The master node (now called control plane) is responsible for managing the cluster, while the worker nodes are responsible for running the applications.

### Control plane

The control plane is responsible for managing the cluster. It consists of the following components:

- **API Server**: The API server is the central management entity that receives and processes REST requests for the cluster.
- **Scheduler**: The scheduler is responsible for scheduling the pods on the worker nodes.
- **Controller Manager**: The controller manager is responsible for managing the controllers that regulate the state of the cluster.
- **etcd**: etcd is a distributed key-value store that stores the cluster state.
- **Cloud Controller Manager**: The cloud controller manager is responsible for managing the cloud provider-specific components.

### Worker nodes

The worker nodes are responsible for running the applications. They consist of the following components:

- **Kubelet**: The kubelet is responsible for managing the pods on the node.
- **Kube-proxy**: The kube-proxy is responsible for managing the network connectivity between the pods.
- **Container runtime**: The container runtime is responsible for running the containers.
- **Pods**: Pods are the smallest deployable units in Kubernetes. They consist of one or more containers that share the same network and storage.