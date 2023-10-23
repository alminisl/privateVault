tags: #pk #debugging #containers

## Explain what the issues is


## Difference in namespaces Local vs AKS(on azure cloud)

![[Pasted image 20221108172023.png]]

Follow up 
- `istiod` WE MUST install this first
- Also Try to access the other namespaces somehow, look at the commands in the e2e docupedia page 

## Enable istio in microk8s
https://istio.io/latest/docs/setup/platform-setup/microk8s/

This installs istio on the microk8s thingy, not sure if that is the right approach for my usecase. 

So what I did is used microk8s to manage all my kubernetes stuff and it worked. So What I will need to try todo is make a new ubuntu VM / Machine and re-do everything 

## Configuring a Gateway and loadbalancer

After executing a `istioctl analyze` I figured that I have the gateway missing. So next step is to configure that, using this link: https://istio.io/latest/docs/tasks/traffic-management/ingress/ingress-control/ 

However, this includes also configuring a loadbalancer. 
`kc get virtualservice`  I will probably write my own loadbalancer here. 

Created a gateway, however, I still have no EXTERNAL-IP in the load balancer.. 

**EXTERNAL-IP** is impossible to have on a local setup. Something new which I learned 

Coming back to the liveness error, found a few interesting articles: 
https://stackoverflow.com/questions/69227517/k8s-liveness-and-readiness-probe-failing-on-a-multi-container-pod 
https://stackoverflow.com/questions/70956057/k8s-spring-boot-pod-failing-readiness-and-liveness-probe


Figuring out what ticks in this case  is something I wanna find out. 

Solution to problems is that I have to manually "UNLOCK" the DB: https://stackoverflow.com/questions/15528795/liquibase-lock-reasons
https://stackoverflow.com/questions/56086473/how-to-fix-liquibase-database-lock-that-does-not-get-cleared

See [other question here](https://stackoverflow.com/questions/30386274/is-there-a-liquibase-lock-timeout/30398337). If the lock happens and the process exits unexpectedly, then the lock will stay there.

Issue with mounting https://stackoverflow.com/questions/47423453/mountvolume-setup-failed-for-volume-nfs-mount-failed-exit-status-32


## Some impromptu solutions to do today

- [x] Make Prometheus work or grafana so I can have normal monitoring for the app ✅ 2022-11-10
    - [x] Checkout how the remote one is working for it ✅ 2022-11-10
- [x] Make the app less and write a custom GO tool for tracking the performance of the pods ✅ 2022-11-16