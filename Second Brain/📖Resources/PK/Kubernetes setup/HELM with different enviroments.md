
Blogpost about the issue
https://blog.tarkalabs.com/handling-multiple-environments-with-helm-kubernetes-f214192f8f7b 

https://codefresh.io/blog/helm-deployment-environments/ 

Should look into our use case where we want to have a simple tooling for spinning up a local and a dev enviroment. 

# Custom CLI tool in GO? 

Nope, I will write it in NodeJS as its easier and faster to make 

# Starting point

What I did, is I created a `values-test.yaml` and used that to run a `helm install`. The first step is:

`kubectl create namespace test`

then I started the Helm charts inside that namespace: 

`helm install beg-pkl-e2e . -n test -f values-test.yaml`

Then I can start the helm normally as I did and it would start normally on the `default` namespace. 

Now the problem is that I need to figure out how to run specific charts in my `test` namespace. 

# Something I found about subcharts

https://stackoverflow.com/questions/54032974/helm-conditionally-install-subchart


# DBeaver with Helm charts

https://artifacthub.io/packages/helm/homeenterpriseinc/cloudbeaver 

- Figure out how to add this on load?
