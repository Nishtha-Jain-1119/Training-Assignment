 1. How many single-item orders were fulfilled from warehouses in the last month?

Query
```SQL
select 
  count(*) as ORDER_COUNT 
from 
  (
    select 
      oi.order_id, 
      count(oi.ORDER_ITEM_SEQ_ID) as ITEM_COUNT, 
      os.STATUS_ID, 
      os.STATUS_DATETIME, 
      oisg.FACILITY_ID 
    from 
      order_item oi 
      join order_item_ship_group_assoc oisga on (
        oisga.ORDER_ID = oi.order_id 
        and oi.ORDER_ITEM_SEQ_ID = oisga.ORDER_ITEM_SEQ_ID
      ) 
      join order_item_ship_group oisg on (
        oisg.ORDER_ID = oisga.ORDER_ID 
        and oisg.SHIP_GROUP_SEQ_ID = oisga.SHIP_GROUP_SEQ_ID
      ) 
      join order_status os on (
        os.ORDER_ID = oi.ORDER_ID 
        and os.ORDER_ITEM_SEQ_ID = oi.ORDER_ITEM_SEQ_ID
      ) 
      join facility f on f.FACILITY_ID = oisg.FACILITY_ID 
      join facility_type ft on f.FACILITY_TYPE_ID = ft.FACILITY_TYPE_ID 
    where 
      os.STATUS_ID = 'ITEM_COMPLETED' 
      and ft.PARENT_TYPE_ID = 'DISTRIBUTION_CENTER' 
      and os.STATUS_DATETIME >= curdate() - INTERVAL 1 month 
    group by 
      oi.ORDER_ID 
    having 
      count(oi.ORDER_ITEM_SEQ_ID) = 1
  ) as tt;

```
Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/f465ce51-28ca-4d54-937a-659237ef7e48)

Inner Query Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/ae89c8b6-bc4f-4155-92ad-560fabcda69c)
