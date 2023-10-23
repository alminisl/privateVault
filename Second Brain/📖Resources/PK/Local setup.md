#localsetup #pk 

<mark style="background: #FF5582A6;">Issues</mark>

```json
at org.codehaus.plexus.classworlds.launcher.Launcher.main (Launcher.java:347)
Caused by: org.apache.maven.wagon.authorization.AuthorizationException: authentication failed for https://artifactory.boschdevcloud.com/artifactory/lab000115-pkl_release-local/com/safenetinc/luna/LunaAPI/7.2.0/LunaAPI-7.2.0.pom, status: 401 Unauthorized
```

Issue with getting the package out of the artifacts. 

## Package com.bosch.pklccc:pkl-helpcenter:jar

this package is needed to be able to run the `helpcenter-backend` but to run that we need to install crypto. 

To install crypto we have to get access to artifacts. 


## To access the cloud config

Wait for my account to be approved on the Cloud Azure side

Then execute these: 

`(az login)`

`az account` `set` `--subscription 6fac4eec-5096-4bc1-9c2a-2aa6f5a7f6d7`

`az aks get-credentials --resource-group pkl-weu-sb-aks-rg --name pkl-weu-sb-aks`

`kubectl config` `set``-context --current --namespace=pkle2e`

## First stepps 

Following this guide: 
[https://phoenixnap.com/kb/create-helm-chart](https://phoenixnap.com/kb/create-helm-chart "https://phoenixnap.com/kb/create-helm-chart")

Using the HELM charts I try to install everything. 
Currently What i did is install minikube and started it. Waiting for a response. 

`helm install pk .` 


## Troubleshooting

**Local setup of the services**
- Figured that the problem with the java project is that we didn't do mvn package everytime we change something. 
- Next problem is understanding why the VOS Tomcat is not starting correctly
	- <mark style="background: #FFB86CA6;">Add to Docu</mark>
	- <mark style="background: #BBFABBA6;">The fix</mark> was to set the JAVA_HOME variable correctly with the correct files present


