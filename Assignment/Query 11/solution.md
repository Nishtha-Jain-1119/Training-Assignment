11.Orders completed hourly:
    * Analyze and present the distribution of completed orders on an hourly basis.
Solution:
```sql
SELECT 
  EXTRACT(
    HOUR 
    FROM 
      STATUS_DATETIME
  ) AS hour_of_day, 
  COUNT(*) AS order_count 
FROM 
  order_status 
where 
  STATUS_ID = 'ORDER_COMPLETED' 
GROUP BY 
  EXTRACT(
    HOUR 
    FROM 
      STATUS_DATETIME
  ) 
ORDER BY 
  hour_of_day;

```

Result:

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/1e940000-c178-4849-abd1-e79f194fb3fb)
