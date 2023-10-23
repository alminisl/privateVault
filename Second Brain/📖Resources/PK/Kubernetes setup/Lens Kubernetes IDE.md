	tags #pk 
Currently I've installed lens for my local env and I need to figure out how to run. 

**TODO**: 
- port forwarding
- Set up the kube config, make a backup and create a new one. 
- Check why metric are not loading Prometheus? 

## Current issue

`Readiness probe failed: HTTP probe failed with statuscode: 500`

## Connected to the remote cluster
tags: #updateDocu 

Had to follow the E2E guide and its working. Also added a new namespace `pkle2e` in lens. 

This is also something which should be updated in the documentation I've been writing. 

**To Switch contexts**
Had the issue where I could not start my local Cluster, however, doing the command below helped solve it: 

`kubectl config use-context kind-beg-pkl-e2e`

also to list all contexts: `kubectl config get-contexts`

## Current issues 

The liveness checks and healthchecks failing. 
[[Figure out why my containers crash and do loopback]]


## Whats the difference between context and namespace? 
tags: #updateDocu 
source: [StackOverflow](https://stackoverflow.com/questions/61171487/what-is-the-difference-between-namespaces-and-contexts-in-kubernetes)

The kubernetes concept (and term) **context** only applies in the kubernetes client-side, i.e. the place where you run the kubectl command, e.g. your command prompt. The kubernetes server-side doesn't recognise this term 'context'.

As an example, in the command prompt, i.e. as the client:

-   when calling the `kubectl get pods -n dev`, you're retrieving the list of the pods located under the namespace 'dev'.
-   when calling the `kubectl get deployments -n dev`, you're retrieving the list of the deployments located under the namespace 'dev'.

If you know that you're targetting basically only the 'dev' namespace at the moment, then instead of adding "-n dev" all the time in each of your kubectl commands, you can just:

1.  Create a context named 'context-dev'.
2.  Specify the namespace='dev' for this context.
3.  Set the current-context='context-dev'.

This way, your commands above will be simplified to as followings:

-   `kubectl get pods`
-   `kubectl get deployments`

You can set different contexts, such as 'context-dev', 'context-staging', etc., whereby each of them is targeting different namespace. BTW it's not obligatory to prefix the name with 'context'. You can just set the name with 'dev', 'staging', etc

