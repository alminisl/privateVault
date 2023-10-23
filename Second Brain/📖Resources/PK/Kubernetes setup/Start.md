tags: #work #kubernetes #setup #initial #main #note

```toc
```

## Starting tooling for the kubernetes in the PK project

- **[[Basics]]** install, differs from System to system. 
	- For example, I've used: https://wiki.archlinux.org/title/Kubernetes 
	- This is guide for Manjaro 
- **[[Minikube]]** - Lightweight kube implementation
- [[microk8s]] - even lighter kube implementation
- **[[Helm]]** - Used this guide - https://phoenixnap.com/kb/create-helm-chart, official docu - https://helm.sh/docs/howto/charts_tips_and_tricks/ 
- **[[Kubectl]]** - Basic usage: https://kubernetes.io/docs/tasks/access-application-cluster/list-all-running-container-images/ 
- [[Kind]] - Simple kubernetes cluster manager

## How do I see what I've started? 

First and hardest step is to create a Kubernetes Cluster locally and make sure you have a kubeconfig. 

[[Commands]] - to see what or where is deployed and how

https://stackoverflow.com/questions/59452828/kubernetes-nodes-do-not-start 


## Open questions

## usefull links
![[usefull resources]]


## Docu link:
[Local k8s setup - BEG Wiki - Docupedia (bosch.com)](https://inside-docupedia.bosch.com/confluence/display/ECUSWDEV/Local+k8s+setup)


## Setting up networking

Install istio like it is shown in the istio website. 

~~Istio is the main building block for the networking. We need to install the `istioctl`
and then `istioctl install` to enable the istio services. 



**Very important part:**

to enable the "injection" of containers into the pod, which istio needs (the `istio-proxy`) we need to use `kubectl label namespace <name> istio-injection=enabled`

 kc get ns default --show-labels - to check if its working

source: [Istio Setup in Kubernetes | Step by Step Guide to install Istio Service Mesh - YouTube](https://www.youtube.com/watch?v=voAyroDb6xk)
services and pods are connected via labels.


## Setting up secrets in pods 

Currently I'm stuck at figuring out the secrets. 

fixed issue I was having the last 2 days, more infor here: [[Certificates]]

## Can't start keycloak

Currently I can't login to keycloak: 
![[Pasted image 20221107152535.png]]

Debugging this issue now. 
New command I learned - `kc port-forward service/<name of service> 8080:80`

To start the services and run them in the browser. 
#updateDocu

## Setting up Lens locally

[[Lens Kubernetes IDE]]

## Troubleshooting 
![[Second Brain/📖Resources/PK/Kubernetes setup/Troubleshooting]]

