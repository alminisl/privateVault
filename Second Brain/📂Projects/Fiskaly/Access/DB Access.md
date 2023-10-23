
- connect to DSFVinK DB and how to? 
		- DB credentials in the 1Password  
		- Looked at the DB secrets in the Kubernetes cluster 

### Commands to attach to Databases

##### Dev database: 
```bash
../../plugins/cloud-sql-proxy --port 5432 fiskaly:europe-west3:postgres-dev-3-replica --credentials-file ./postgres/sign-de-v1.json
```

##### Prod Database
```bash
../../plugins/cloud-sql-proxy --port 5432 fiskaly:europe-west3:test-postgres-1 --credentials-file ./postgres/sign-de-v1.json
```
