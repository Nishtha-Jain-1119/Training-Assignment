8. How many orders with a single return were recorded in the last month?

Query
```SQL
select 
 count(tt.order_id) as order_count
from 
  (
    select 
      ri.RETURN_ID as return_id, 
      ri.order_id as order_id 
    from 
      return_item ri 
    group by 
      ri.ORDER_ID 
    having 
      count(distinct ri.RETURN_ID)= 1 
      and ri.ORDER_ID is not null
  ) as tt 
  join return_header rh on rh.return_id = tt.return_id 
where 
  rh.entry_date >= CURDATE() - INTERVAL 1 month;
```

Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/f927492f-13da-4284-ac26-027eef0dc8b1)

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/998179be-7ec2-48ef-bf0f-bc17fc8c2564)
