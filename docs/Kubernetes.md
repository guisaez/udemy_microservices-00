### Whirlwind Tour of Kubernetes (K8S)

We use the following to interact with Kubernetes
```shell
kubectl
```

### Terminology
* Kubernetes Cluster: A collection of node + a master to manage them
* node: A virtual machine that will run our containers.
* Pod: More or less a running container. Technically, a pod can run multiple containers.
* Deployment: MOnitors a set of pods, make sure they are running and restarts them if they crash.
* Service: Provides an easy-to-remember URL to access a running container. 

### Config Files:

* Tells Kubernetes about the different deployments, pods, and Services (referred to as 'Objects') that we want to create.
* Written in YAML syntax.
* Always store these files with our project source code - they are documentation!
* We can create Objects without config files - do not do this. COnfig files provide a precise definition of what your cluster is running. 
    * Kubernetes docs will tell you to run direct commands to create objects - only do this for testing purposes. 
    * Blog posts will tell you to run direct commands to create objects - close the blog post!

### Creating a Pod

```
apiVersion: v1 // K8S is extensible - we can add our own custom objects. 
               // This specifies the set of objects we want K8S to look at.
kind: Pod      // Type of object we want to create
metadata:      // Config options for the object we are about to create
    name:posts  // When the pod is created, give it a name of 'posts'
spec:          // The exact attributes we want to apply to the object we 
               // are about to create
    containers: // We can create many containers in a single pod
        - name: posts // Make a container with a name of 'posts'
        image: <container> // The exact image we want to use.
```

```shell
kubectl apply -f <filename>.yaml
```

### Commands
```shell
kubectl get pods 
```

```shell
kubectl exec -t [pod_name][cmd]

kubectl logs [pod_name]

kubectl dele pod [pod_name]

kubectl apply -f [config file name]

kubectl describe pod [pod_name]
```





