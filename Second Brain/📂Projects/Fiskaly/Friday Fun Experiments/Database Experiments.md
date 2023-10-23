
```sql
REATE TABLE cpc_partition_completed (  
    CHECK (state = 'COMPLETED')  
) INHERITS (cash_point_closings);  
  
CREATE TABLE cpc_partition_error (  
    CHECK (state = 'ERROR')  
) INHERITS (cash_point_closings);  
  
INSERT INTO cpc_data_completed SELECT * FROM cash_point_closings WHERE state = 'COMPLETED';  
INSERT INTO cpc_data_error SELECT * FROM cash_point_closings WHERE state = 'ERROR';  
  
-- Percentage of successful CPC data for the COMPLETED partition  
SELECT (COUNT(*)::float / (SELECT COUNT(*) FROM cpc_partition_completed)::float) * 100 AS percentage_completed  
FROM cpc_partition_completed;  
  
-- Percentage of successful CPC data for the ERROR partition  
SELECT (COUNT(*)::float / (SELECT COUNT(*) FROM cpc_partition_error)::float) * 100 AS percentage_error  
FROM cpc_partition_error;
```


Current SQL Query to get the percentages: 

```sql
SELECT  
    (COUNT(CASE WHEN state = 'COMPLETED' THEN 1 END) / CAST(COUNT(*) AS FLOAT)) * 100 AS completed_percentage,  
    (COUNT(CASE WHEN state = 'ERROR' THEN 1 END) / CAST(COUNT(*) AS FLOAT)) * 100 AS error_percentage  
FROM  
    cash_point_closings;
```

Next up is to figure out the following: 

Calculate the percentage of successfully processed Cash Point Closings as they reach the a finished state (COMPLETED and ERROR unless E_UNKNOWN)
	- A = COMPLETED + (ERROR-E_UNKNOWN)
	- B = A + E_UNKNOWN + (WORKING where time_creation is older than 20 seconds)
	- Availability for Cash Point Closings = A / B
- From the time the `insertCashPointClosing` was requested, to the time it was inserted to the database to the time where it reached a finished state must be less or equal to 20 seconds. Otherwise it is also counted as **not available** even though it reached a finish state.
    
- Add a widget to the [DSFinV-K API Health Monitoring Dashboard](https://console.cloud.google.com/monitoring/dashboards/builder/eef8acc3-9f17-444d-be9b-ca879c1afcb6?project=fiskaly "https://console.cloud.google.com/monitoring/dashboards/builder/eef8acc3-9f17-444d-be9b-ca879c1afcb6?project=fiskaly")

