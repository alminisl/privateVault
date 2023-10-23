tags: #kubernetes #basics #k8s #knowledgebase 

```toc
```


## K8s provides us with


- Service discovery and load balancing
	- Can load balance traffic exposes a container using the DNS name and IP address. 
- Storage Orchstration
	- Mount sotrage system - Local, cloud etc. 
- Automated Rollouts / Rollbacks
	- Create nw container for deployment, remove existing container and adopt all their resource to the new container
- Automatic bin packaging
	- Resource managing, you tell k8s how much CPU/RAM each cotnainer needs. Fit containers onto your nodes to make the best use of resources
- Self healing 
	- Restarts containers if they fail 
- Secred and configuration management 
	- k8s restarts containers that fail replaces containers kills containers that don't respond to your user passwords, tokens and ssh keys 

## Kubernetes components 

Deploying K8s means deploying a Cluster. 

Cluster consits of **Worked machines** called **[Nodes](https://kubernetes.io/docs/concepts/architecture/nodes/)** that run containerized apps. Every cluster has at least one worker node. 

Worker nodes host **[Pods](https://kubernetes.io/docs/concepts/workloads/pods/)** that are components of the app workload.

Control Plane manages the worker nodes and the Pods in the cluster. 

In production environments, the control plane usually runs across multiple computers and a cluster usually runs multiple nodes, providing fault-tolerance and high availability.

![Components of Kubernetes](https://d33wubrfki0l68.cloudfront.net/2475489eaf20163ec0f54ddc1d92aa8d4c87c96b/e7c81/images/docs/components-of-kubernetes.svg)

### Control plane Components 

Control planes components make global decisions about the cluster for example scheduling and detecting responding to cluster events. (for example, starting up a new [pod](https://kubernetes.io/docs/concepts/workloads/pods/) when a deployment's `replicas` field is unsatisfied).

#### Kube-api server 

The API server is the fornt end for the Kubernetes control plane. 

`kube-apiserver` main implementation of the kubernetes API. 

#### etcd

Key value store used as K8s backing store for all cluster data.
You can find in-depth information about etcd in the official [documentation](https://etcd.io/docs/).

#### kube-scheduler

Control plane component that watches for newly created [Pods](https://kubernetes.io/docs/concepts/workloads/pods/) with no assigned [node](https://kubernetes.io/docs/concepts/architecture/nodes/), and selects a node for them to run on.

#### kube-controller-manager
Some types of these controllers are:

-   Node controller: Responsible for noticing and responding when nodes go down.
-   Job controller: Watches for Job objects that represent one-off tasks, then creates Pods to run those tasks to completion.
-   EndpointSlice controller: Populates EndpointSlice objects (to provide a link between Services and Pods).
-   ServiceAccount controller: Create default ServiceAccounts for new namespaces


#### cloud-controller-manager 
> TODO: Figure this out at a later date


### Node components 

#### kubelet 

An agent that runs on each [node](https://kubernetes.io/docs/concepts/architecture/nodes/) in the cluster. It makes sure that [containers](https://kubernetes.io/docs/concepts/containers/) are running in a [Pod](https://kubernetes.io/docs/concepts/workloads/pods/).

#### kube-proxy

kube-proxy is a network proxy that runs on each [node](https://kubernetes.io/docs/concepts/architecture/nodes/) in your cluster, implementing part of the Kubernetes [Service](https://kubernetes.io/docs/concepts/services-networking/service/) concept.

#### container-runtime

The container runtime is the software that is responsible for running containers. 


## Kuberentes Dashboard 

https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/ 

Also use this link to create the user for the admin and generate the token

https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md

## Usefull Commands

![[Commands]]


## Kubernetes usage - Load balancer

Exposing a pod / group of pods to a network. 

Service is being used to load balance and expose the pods. 

`service.yml`

`kubectl get service` or `kubectl describe services`




