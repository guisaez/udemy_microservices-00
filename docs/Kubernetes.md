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

### Deployment Commands

```shell
kubectl get deployments

kubectl describe deployment [deployment name]

kubectl apply - f [config file name]

kubectl delete deployment [dpl_name]
```

### Types of Services

* Cluster IP: Sets up easy-to-remember URL to access a pod. Only exposes pods in the cluster.
* Node Port: Makes a pd accessible from outside the cluster. Usually only used for dev purposes.
* Makes a pod accessible from outside the cluster. THis is the right way to expose a pod to the outside world.
* Redirects an in_cluster request to CNAME url ...

### Creating a Node Port Service

```
apiVersion: v1
kind: Service
metadata:
  name: posts-srv
spec:
  type: NodePort
  selector:
    app: posts
  ports:
    - name: posts
    protocol: TCP
    port: 4000
    targetPort: 4000
```

Notes:
* Port vs. TargetPort: Application listen through port and sends info through targetPort. 
* Port and TargetPort do not need to be identical. 

### Create A Cluster IP:

```
apiVersion: v1
kind: Service
metadata:
  name: posts-clusterip-srv
spec:
  type: ClusterIP
  selector:
    app: posts
  ports:
    - name: posts
      protocol: TCP
      port: 4000
      targetPort: 4000
```

### Load Balancer Service

Have a one single point of entry in our cluster. the Load Balancer will route the request to the correct cluster.

* Load Balancer Service: Tells Kubernetes to reach out to its provider and provision a load balancer. Gets traffic into a single pod.
* Ingress or Ingress Controller: A pod with a set of routing rules to distribute traffic to other services. 

 

