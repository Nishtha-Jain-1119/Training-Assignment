15. Shipping Revenue last month:
    * Determine the total revenue generated from shipping in the last month.
Solution:
```sql
select 
  sum(oa.AMOUNT) as total_revenue 
from 
  order_adjustment oa 
  join shipment s on (
    s.PRIMARY_ORDER_ID = oa.ORDER_ID 
    and oa.ORDER_ADJUSTMENT_TYPE_ID = 'SHIPPING_CHARGES'
  ) 
  join shipment_status ss on s.SHIPMENT_ID = ss.SHIPMENT_ID 
where 
  ss.STATUS_ID = 'SHIPMENT_SHIPPED' 
  and ss.STATUS_DATE >= curdate() - INTERVAL 1 month;

```

Result:

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/eac784df-25ef-4b0c-868f-2183d6dcc59a)
