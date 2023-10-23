Helm is a package manager for Kubernetes that makes it easy to take applications and services that are either highly repeatable or used in multiple scenarios and deploy them to a typical K8s cluster


## What is helm? 

Package manager for kubernetes, something like npm. 

- Helm charts are just Bundles of YML files. 
- Download and use exisitng ones. 
`helm install` some chart to install helm packages so to say 

### Templating engine 

Write once and re-use the yaml files. 

example: 

```
name: {{.Values.name}}
```

comes from the `values.yaml`

.Values object created from the `values.yaml`

Practical for CI/CD, so we need that for our deployment. 

![[Pasted image 20221102140548.png]]

### Structure

Chart.yaml - meta info about chart

values.yaml - Default values and can be overrited 

chards folder -  chart dependencies

templates folder - the actual template files 


