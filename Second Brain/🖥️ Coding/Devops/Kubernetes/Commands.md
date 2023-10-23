
## Kubectl commands

`kubectl apply -f <filename>` - Deploys and creates containers based on a deployments.yml

`kubectl get all` - Gets all pods and services and replicas

`kubectl get pods -o wide` - show pods with ip address and images

`kubectl get pods` - shows pods

`kubectl get deployments` - Shows which deploymens yml is being used and for what 

`kubectl get namespaces` - Gets all the namespaces

`kubectl delete namespace <namespace>` - Deletes namespace 

`kubectl edit deployment istiod -n istio-system` - Edit he Istio config

`kubectl delete -n NAMESPACE deployment DEPLOYMENT` - Delete a pod 

`kubectl delete --all pods --namespace=foo` - DELETE all pods

`kubectl -n default rollout restart deploy` - kubectl recreate all pods

## Handling webhook

`kubectl delete -A ValidatingWebhookConfiguration ingress-nginx-admission` - Delete a webhook 

`kubectl get validatingwebhookconfigurations.admissionregistration.k8s.io` - Get webhook

## Auth issues fixing: 
`kubectl create secret docker-registry acr-auth --docker-server pklhub.azurecr.io --docker-email almin.islamovic@at.bosch.com --docker-username pklhub --docker-password BxQQI3MCGRmxVc7ldGHKSC/pafyFKVyu`

https://stackoverflow.com/questions/40686151/kubernetes-pod-gets-recreated-when-deleted 

