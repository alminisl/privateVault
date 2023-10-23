There are several ways to achieve multi-tenancy with PostgreSQL on Azure, depending on the specific requirements of your application. Some common approaches include:

1.  Schema-based multi-tenancy: Each tenant is assigned its own schema within a single database. This approach allows for easy data isolation, but it can make it difficult to share data between tenants.
    
2.  Database-based multi-tenancy: Each tenant is assigned its own database. This approach offers better data isolation than schema-based multi-tenancy, but it can be more difficult to manage and more resource-intensive.
    
3.  Using Azure Database for PostgreSQL Hyperscale (Citus) which is a scale-out version of PostgreSQL that allows you to shard your data horizontally, you can use that to create a logical isolation by creating a shard per tenant.
    

You can also use Azure Policy to ensure that each tenant's resources are restricted to a specific resource group or virtual network.

4.  Using Azure AD authentication: You can use Azure Active Directory (AD) to authenticate users and control access to the tenant's data. This allows you to use Azure's built-in role-based access control (RBAC) to manage permissions and ensures that each tenant's data is only accessible by authorized users.

Another option is to use Azure Arc enabled PostgreSQL instances, this allows you to run postgres instance on-premise or in other clouds and manage them through Azure Arc, and manage multi-tenancy by applying policies, RBAC and monitoring all in one place.

It's important to consider the trade-offs between data isolation and data sharing when choosing an approach for multi-tenancy. And also consider the size of your tenants and the expected growth, as well as the number of tenants and the amount of data you'll be storing for each tenant. It's also good to consult a specialist to help you design and implement a multi-tenancy strategy that fits your use case and technical requirements.

---


## Some usefull links: 
- [# Multitenancy Options for PostgreSQL](https://severalnines.com/blog/multitenancy-options-postgresql/#:~:text=Multi%2Dtenancy%20in%20a%20software,on%20those%20criteria%20and%20objectives) - Differenciates between hard and soft separation 
- [Multi tenant db CosmoDB - Azure - Postgres](https://learn.microsoft.com/en-us/azure/cosmos-db/postgresql/tutorial-design-database-multi-tenant?tabs=direct)
	- A Azure Cosmos DB for PostgreSQL deployment stores table rows on different nodes based on the value of a user-designated column. This "distribution column" marks which tenant owns which rows.
- [Multitenancy Azure](https://learn.microsoft.com/en-us/azure/architecture/guide/multitenant/service/postgresql)
- Partitioning is done.. I can showcase what My findings are


## Conclusion
- first up I need to figure out what does this entail. 
	- We have different components with their own DBs and we will need to migrate those DBs to the azure DB. 
	- The question is will that work for us? 
- We should be able to add a simple DB change which would entail adding a table "vendor" or something in that regard which would help us understand the table schema and how / what is connected
- https://learn.microsoft.com/de-de/azure/cosmos-db/postgresql/tutorial-design-database-multi-tenant?tabs=direct - Multitenant for the AzurePostgresql 

So my first step is to generate table schemas for the DBs. 
	 [[DB Schemas]]