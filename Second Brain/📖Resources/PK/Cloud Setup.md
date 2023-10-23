
Reference: https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/containers/aks-microservices/aks-microservices 
https://learn.microsoft.com/en-us/azure/architecture/browse

- [x] Understand how to deploy locally to Azure AKS ✅ 2022-11-24
- [x] Understand what the architecture should look like ✅ 2023-01-27

## Architecture 
tags: #aks #architecture #tutorial 
ref: https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/containers/aks-microservices/aks-microservices 

[[24-11-2022]]

I've deployed the cluster into the cloud / AKS. the deployed cluster is noething more then my own smaller one with the following services: VOS, Postgres, Mosquitto, TB, SBOD, KTS, keycloak. 

Now the task is to figure out if I need the SBOD. 

## AKS and Helm deployment (separate page?)
tags: #aks #helm #tutorial #deployment
ref: https://learn.microsoft.com/en-us/azure/aks/quickstart-helm?tabs=azure-cli 

Renaming the `beg-pkl-e2e` did not work. Still if I rename the charts they fail. 

- Search codebase for `beg-pkl-e2e` 
- Rename to `pk-test`
- Helm charts won't start various mounting Volume issues

- Running the helm charts with `beg-pkl-e2e`, even after renaming does not work. 

I can execute the helm / kubectl commands. Now what I need to test is how and where to execute them. 

Probably Helm uninstall and helm install. I will try that out first tomorrow.



