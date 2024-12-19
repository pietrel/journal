# Ingress

An Ingress is a way to expose HTTP and HTTPS routes from outside the cluster to services within the cluster. It is a layer 7 (HTTP/HTTPS) load balancer that routes traffic to services based on the request host or path.

Ingress is not a service type, but it acts as the entry point for your cluster. It is a collection of rules that allow inbound connections to reach the cluster services.

Ingress is an API object that manages external access to services in a cluster, typically HTTP. It provides HTTP and HTTPS routing to services based on the request host and path.

Ingress can provide load balancing, SSL termination, and name-based virtual hosting. It can also provide path-based routing and session affinity.

Ingress is implemented by a controller that watches the Kubernetes API server for changes to Ingress resources and updates the configuration of a load balancer in response.

Ingress controllers are responsible for fulfilling the Ingress, usually with an HTTP or L7 load balancer. Different controllers support different features, so it's important to choose the right one for your use case.

Ingress controllers can be implemented in many ways, including Nginx, Traefik, HAProxy, and Istio. They can be deployed as pods in the cluster or as external services.

Ingress controllers can be configured using annotations on the Ingress resource or by using custom resources provided by the controller.

Ingress resources can be created using YAML or JSON files and applied to the cluster using `kubectl apply`.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: minimal-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  ingressClassName: nginx-example
  rules:
    - http:
        paths:
          - path: /testpath
            pathType: Prefix
            backend:
              service:
                name: test
                port:
                  number: 80

```

Ingress resources can be created using the following fields:

- `apiVersion`: The version of the Ingress API.
- `kind`: The type of resource (Ingress).
- `metadata`: The metadata for the Ingress resource, including the name and annotations.
- `spec`: The specification for the Ingress resource, including the Ingress class, rules, and backends.
- `ingressClassName`: The class of the Ingress controller that should be used to fulfill the Ingress.
- `rules`: The rules for the Ingress, including the host and paths that should be matched.
- `http`: The HTTP rule for the Ingress.
- `paths`: The paths that should be matched for the Ingress.
- `path`: The path that should be matched.
- `pathType`: The type of path matching (Prefix or Exact).
- `backend`: The backend service that should receive the traffic.
- `service`: The name of the service that should receive the traffic.
- `port`: The port on the service that should receive the traffic.
