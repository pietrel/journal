# Custom Resource Definition

A Custom Resource Definition (CRD) is an extension of the Kubernetes API that allows you to define your own custom resources. Once you have defined a CRD, you can create instances of it, which are called custom resources. Custom resources are stored in the Kubernetes API and can be managed using the standard Kubernetes API operations.

CRDs are a way to extend the Kubernetes API to create, configure, and manage custom resources in a declarative way. They allow you to define your own resources and controllers to manage them.

CRDs are defined using a CustomResourceDefinition object, which specifies the structure of the custom resource, including its schema, validation rules, and status fields. Once you have defined a CRD, you can create instances of it, which are stored in the Kubernetes API and can be managed using the standard Kubernetes API operations.

CRDs are used by operators to define custom resources that represent the applications they manage. Operators watch for changes to custom resources and take action to reconcile the desired state of the resources with the actual state of the cluster.

## Creating a Custom Resource Definition

To create a Custom Resource Definition, you need to define a CustomResourceDefinition object and apply it to the cluster using `kubectl apply`. The following is an example of a CustomResourceDefinition object that defines a custom resource called `MyCustomResource`:

```yaml
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: mycustomresources.example.com
spec:
  group: example.com
  versions:
    - name: v1
      served: true
      storage: true
      schema:
        openAPIV3Schema:
          type: object
          properties:
            spec:
              type: object
              properties:
                contents:
                  type: string
                image:
                  type: string
                replicas:
                  type: integer
  scope: Namespaced
  names:
    plural: mycustomresources
    singular: mycustomresource
    kind: MyCustomResource
    shortNames:
      - mcr

```
