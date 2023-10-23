### Ideas for working on small projects..

- Project Jellyfish 
- Make custom nginx logs / big query
- Make performance analysis and flamegraphs
- Analyse exports duration / count / length 
- Make the DB queries work 

```sql 
SELECT CASE WHEN time_start IS NOT NULL and time_end IS NOT NULL THEN  
EXTRACT (EPOCH FROM (time_end - time_start))  
ELSE NULL  
END  
FROM cash_point_closings;
```


Next steps would be to make a UI which uses prisma / nextjs https://www.prisma.io/docs/getting-started/setup-prisma/add-to-existing-project/relational-databases/introspection-typescript-postgresql 


