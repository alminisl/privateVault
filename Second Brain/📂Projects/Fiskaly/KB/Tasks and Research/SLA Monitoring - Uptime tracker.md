

### Google cloud solutions 

- https://cloud.google.com/monitoring/uptime-checks/introduction#:~:text=There%20are%20two%20types%20of,addresses%20of%20Google%20Cloud%20resources. 


### Some third party solution

https://serverfault.com/questions/1017243/how-to-implement-cloud-monitoring-uptime-checks-for-instances-without-external-i 

https://cloud.google.com/monitoring/agent/ops-agent/third-party/nginx - Logs setup for the Nginx 


## TODO: starting the knowledge assimilation for the task at hand 

- [x] Test (@04-08-2023 11:09) 

- I've made some experiments with the Metrics explorer however I have no idea if that would / will help. 
- Currently I've made a 200 status code and a 500 status code graph and  I need somehow to merge them together and do a diff*

### To investigate / Learn 

- 95th percentile, what does that mean? Could this be a used metric? 
- Monitor per organization metrics of availability / uptime 
- Last byte in first byte out 


### Documentation for ingress nginx 

https://github.com/kubernetes/ingress-nginx/blob/main/docs/user-guide/monitoring.md 


### Metrics to check out: 

```promql
rate(nginx_connections_accepted{kube_cluster_name=~$cluster}[$__interval]) - rate(nginx_connections_handled{kube_cluster_name=~$cluster}[$__interval]) or vector(0) / rate(nginx_connections_accepted{kube_cluster_name=~$cluster}[$__interval]) * 100
```

kube_cluster_naem ? 
cluster ? 

**This is for calculating the total http calls**

```
sum by (status_code) (
  increase(http_requests_total{namespace="prod" , path="/register"}[3h20m])
)
```

Kinda working: 

```
sum(irate(nginx_ingress_controller_requests{status=~"2..|4.."}[${__interval}])) / sum(irate(nginx_ingress_controller_requests{status=~"5.."}[${__interval}])) * 100
```

```
sum(irate(nginx_ingress_controller_response_size_count{status=~"2..|4.."}[${__interval}])) / sum(irate(nginx_ingress_controller_response_size_count{status=~"5.."}[${__interval}])) * 100
```

#### Latest revision of the query 

(Total_2xx_to_4xx / Total_Responses) * 100
```sql
sum(irate(nginx_ingress_controller_response_size_count{status=~"2..|4..",host="dsfinvk.fiskaly.com"}[${__interval}])) / sum(irate(nginx_ingress_controller_response_size_count{host="dsfinvk.fiskaly.com"}[${__interval}])) * 100
```

(Total_5xx / Total_Responses) * 100

```sql
sum(irate(nginx_ingress_controller_response_size_count{status=~"5..",host="dsfinvk.fiskaly.com"}[${__interval}])) / sum(irate(nginx_ingress_controller_response_size_count{host="dsfinvk.fiskaly.com"}[${__interval}])) * 100
```

Overall Percentage 

Percentage_2xx_4xx + percentage_5xx

```sql
sum(irate(nginx_ingress_controller_response_size_count{status=~"2..|4..",host="dsfinvk.fiskaly.com"}[${__interval}])) / sum(irate(nginx_ingress_controller_response_size_count{host="dsfinvk.fiskaly.com"}[${__interval}])) * 100 + sum(irate(nginx_ingress_controller_response_size_count{status=~"5..",host="dsfinvk.fiskaly.com"}[${__interval}])) / sum(irate(nginx_ingress_controller_response_size_count{host="dsfinvk.fiskaly.com"}[${__interval}])) * 100
```


## Additional graphs

- Total number of requests 

```sql
sum(nginx_ingress_controller_requests{host="dsfinvk.fiskaly.com"})
```

- Throughput 

```sql
sum(rate(nginx_ingress_controller_requests{host="dsfinvk.fiskaly.com"}[${__interval}]))
```

## Goal 

Endpoint Availability: 

Success/totalRequest 
ex. 980/1000 = 0,98 *100 =98%

Exports: 

Completed/TotalExports 
ex. 190/200 = 0.95 * 100 = 95%

CPCs: 
CompletedUnder20Sec / totalCpcs 
ex. 45/50 = 90% 

Average availability would be then: 

endpointAvailabnility + Export  + CPCs / 3
98 + 95 + 90 / 3 = ~95% 

And this would be run any minute.. dailty.. weekly?

I think it makes sense 😅

Now for the hourly calculateion it would be something like: 

Daily Average  = (98% + 95% + 90% + All other minutes.. ) / 1,440

Then the Weekly Average =  (Sum of daily average availabilities for all 7 days) / 7

## Variables 


`nginx_ingress_controller_nginx_process_connections_total` - Total number of connections on the cluster? 

[[grafana json]]


## whats next


## Glossary 

- irate() — It **calculates the instant rate of increase of the time series in the range vector**. It graphs based on the last two endpoints. Wondering when to use each of these? 

- rate() is generally used when graphing the slow moving counters. While irate() is used when graphing the high volatile counters.

 

