
Issues with istio.io, used these resources to fix it: 
https://istio.io/latest/docs/setup/install/helm/ 
https://istio.io/latest/docs/setup/platform-setup/minikube/
https://github.com/istio/istio/issues/7583

>  [Internal error occurred: failed calling webhook "validation.istio.io"](https://stackoverflow.com/questions/71698267/internal-error-occurred-failed-calling-webhook-validation-istio-io)

````
kubectl delete validatingwebhookconfiguration istiod-default-validator 
````

## issue with pulling image from the kubernetes cluster
https://stackoverflow.com/questions/54517251/pull-azure-container-registry-image-in-kubernetes-helm

> Your kubernetes cluster needs to be authenticated to the container registry to pull images, generally this is done by a docker secret

```bash
kubectl create secret docker-registry regcred --docker-server=pklhub --docker-username=<your-name> --docker-password=<your-pword> --docker-email=<your-email>
```

This seems to not be my problem.. but the below is a bit more informative. 

Configuring my local cluster to use the azure container registry: 
https://learn.microsoft.com/en-us/azure/container-registry/container-registry-auth-kubernetes 

Creating a ACR_NAME
creating a SERVICE_PRINCIPAL_NAME [[Service Principal for Kubernetes and Azure]]

new Error message: 
```
The client 'isa1wi@bosch.com' with object id '7c554600-d9f3-478c-a164-582d660997b6' does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/34da224e-3f6d-4628-83f5-e13ea67bd149/resourceGroups/DefaultResourceGroup-WEU/providers/Microsoft.ContainerRegistry/registries/pklHub/providers/Microsoft.Authorization/roleAssignments/d02692d8-f2b2-4179-befd-43fdbc032677' or the scope is invalid. If access was recently granted, please refresh your credentials.
```


trying out this command: 
`az acr show --name $ACR_NAME --query id --output ts`

## THis should fix the issue with the acr-auth

https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ 

Fixed by using the credentials from the azure PKLHUB



## TLS handshake timeout

https://stackoverflow.com/questions/65119776/kubectl-logs-returning-tls-handshake-timeout

Not sure how to fix this issue still .

### Kubernetes cluster unreachable  

[microk8s] kubectl config view --raw > ~/.kube/config

# Issue with kubelogin

This was the fix: https://github.com/Azure/kubelogin had to install the azure kubelogin