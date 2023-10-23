
[[22-12-2022 1]] Attending a helm workshop. 

# Consolidate configuration sprawl 

exactly what we need, different enviroments with different enviroment values. 


# helm hooks

https://helm.sh/docs/topics/charts_hooks/ 

Something like web hooks and we can install / configure stuff when some stuff is happening. 

- pre/post-install
- pre/post delete
- pre/post upgrade
- pre/post rollback
- test 

Something hooks are used for is setting data after the cluster is running. 

## DB update with post-install

We can execute a script which enters some sql data after the cluster is being run using the post-install maybe experiment with that. 

- Create generic templates for the team
	- values.yaml
	- the directory level is whats used. ![[Pasted image 20221222155412.png]]
	- Both are fin in the end. 
	- We can use functions from `go templates` and we can use something like `{{quote .Values.name.firstName}}`
	- 
- How can you version sensitive data

RBAC 
- Use proper policies for users, groups and service accounts that are running Pods

 Lab3: https://github.com/AdminTurnedDevOps/PearsonCourses/blob/main/Helm-Charts-For-Kubernetes/Segment4/lab.md 


# Real world use cases 

- Manage multiple enviroments
- packaged like an app 

# Registry

artifact hub - the docker hub for helm charts

# Using subcharts or charts inside charts is maybe the way to go with the kubernetes / helm charts deployment of dbeaver. I would love to configure dbeaver and not just use the default pgadmin but question is it worth the cost?

