Ticket: https://rb-tracker.bosch.com/tracker02/browse/PKMVP-808

![[Unbenannt-2022-12-06-1428(4).png]]

## Alerts

Use this as example: `sum by (cpu) (rate(node_cpu_seconds_total{mode="idle"}[1m]))`
This is a query which shows us the CPU usage. 

# Pull

Prometheus uses pull system benefits are: 
- Multiple prometheus instances
- easily detetect if the service is running

# data storage

Where does prometheus store data? 
- The metrics data is stored on Disk. Contains time series DB but also integrates with remote storage systems. Can't be added to relationDB. Only Time Series DB 

# Components level Grafana

- timeline of key 

---

# To research more 

PK - Digital key stuff with grafana 

Which metrics can we input from the Java spring boot? Ex. Get keys from A to B with Grafana. 
https://grafana.pkl-weu-sb.cus-sb.managed-runtime.bosch-mobility-cloud.com/explore?orgId=1&left=%7B%22datasource%22:%22P982945308D3682D1%22,%22queries%22:%5B%7B%22refId%22:%22A%22,%22expr%22:%22%7Bapp%3D%5C%22tbe%5C%22%7D%20%7C%3D%20%60pkl%60%22,%22queryType%22:%22range%22,%22editorMode%22:%22builder%22%7D%5D,%22range%22:%7B%22from%22:%22now-1h%22,%22to%22:%22now%22%7D%7D

look at this too: https://grafana.com/docs/grafana/latest/explore/trace-integration/



Using this somehow to trigger the key tracking.. 







