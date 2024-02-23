10. Orders brokered but not shipped:
    * Identify orders that have been brokered (arranged or negotiated) but have not been shipped yet or shipment has not yet been created/initiated.
Solution:
```sql
select 
  distinct oisg.order_id 
from 
  order_item_ship_group oisg 
  join order_item oi on oi.ORDER_ID = oisg.ORDER_ID 
  join facility f on f.FACILITY_ID = oisg.FACILITY_ID 
  join facility_type ft on f.FACILITY_TYPE_ID = ft.FACILITY_TYPE_ID 
where 
  ft.PARENT_TYPE_ID is not null 
  and ft.PARENT_TYPE_ID != 'VIRTUAL_FACILITY' 
  and (
    oi.STATUS_ID != 'ITEM_COMPLETED' 
    and oi.STATUS_ID != 'ITEM_CANCELLED'
  );

```

Result:

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/323ec6e7-d45d-42de-9941-182afd74b40a)
