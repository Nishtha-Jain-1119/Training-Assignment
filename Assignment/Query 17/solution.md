17. BOPIS orders Revenue in the last year:
    * Calculate the revenue generated from BOPIS orders over the past year.

Solution:
```sql
select 
  sum(oi.UNIT_PRICE * oi.QUANTITY) as revenue 
from 
  order_item oi 
  join order_item_ship_group oisg on (
    oi.ORDER_ID = oisg.ORDER_ID 
    and oisg.SHIPMENT_METHOD_TYPE_ID = 'STOREPICKUP'
  ) 
  join order_status os on (
    oisg.ORDER_ID = os.ORDER_ID 
    and os.STATUS_ID = 'ITEM_COMPLETED'
  ) 
where 
  os.STATUS_DATETIME >= date_sub(
    current_date(), 
    interval 1 year
  );

```
Result:

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/7fa92248-241f-443e-b8c5-4ede38a3a430)
