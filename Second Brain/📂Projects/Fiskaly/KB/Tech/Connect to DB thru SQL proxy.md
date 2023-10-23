#proxy #db #connect
## Connecting to Database thru proxy 

`cloud-sql-proxy --port 5432 fiskaly:europe-west3:postgres-dev-3-replica --credentials-file ./postgres/sign-de-v1.json`

This method is used to connect to the databases on the cloud. This one specifically is for the Dashboard. 

To get other DBs go to Google cloud and find the needed DB connection string. 