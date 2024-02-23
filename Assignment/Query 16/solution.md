16. Send sale orders shipped from the warehouse:
    * Identify send sale orders that have been shipped from the warehouse.
Solution:
```sql
select 
  distinct oh.ORDER_ID send_sale_orders 
from 
  order_header oh 
  join order_item_ship_group oisg on oisg.ORDER_ID = oh.ORDER_ID 
  join facility f on f.FACILITY_ID = oisg.FACILITY_ID 
  join facility_type ft on (
    f.FACILITY_TYPE_ID = ft.FACILITY_TYPE_ID 
    and ft.PARENT_TYPE_ID = 'DISTRIBUTION_CENTER'
  ) 
  join shipment s on (
    s.PRIMARY_ORDER_ID = oisg.ORDER_ID 
    and s.STATUS_ID = 'SHIPMENT_SHIPPED'
  ) 
where 
  oh.SALES_CHANNEL_ENUM_ID = 'POS_SALES_CHANNEL';

```

Result:

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/ab26055f-9e97-413c-b8b0-9c9bf1e25d0f)
