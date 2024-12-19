# Kubernetes Objects

Kubernetes uses objects to represent the state of the cluster. The following are some of the most common Kubernetes objects:

- **Pod**: A pod is the smallest deployable unit in Kubernetes. It consists of one or more containers that share the same network and storage.
- **Service**: A service is an abstraction that defines a logical set of pods and a policy by which to access them.
- **Volume**: A volume is a directory that is accessible to the containers in a pod.
- **Namespace**: A namespace is a way to divide cluster resources between multiple users.
- **Deployment**: A deployment is a way to declaratively manage a set of pods.
- **StatefulSet**: A StatefulSet is a way to manage stateful applications.
- **DaemonSet**: A DaemonSet ensures that all (or some) nodes run a copy of a pod.
- **Job**: A Job creates one or more pods and ensures that a specified number of them successfully terminate.
- **CronJob**: A CronJob creates a job on a repeating schedule.
- **ConfigMap**: A ConfigMap is a way to inject configuration data into a pod.
- **Secret**: A Secret is a way to inject sensitive data into a pod.
- **Ingress**: An Ingress is a way to expose HTTP and HTTPS routes from outside the cluster to services within the cluster.
- **PersistentVolume**: A PersistentVolume is a piece of storage in the cluster that has been provisioned by an administrator.