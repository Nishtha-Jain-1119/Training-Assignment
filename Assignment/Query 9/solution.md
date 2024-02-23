9. Find orders where multiple items are grouped and shipped together in a single shipment.
Solution:
```sql
select 
  ORDER_ID, 
  SHIP_GROUP_SEQ_ID, 
  count(ORDER_ITEM_SEQ_ID) as item_count 
from 
  order_item_ship_group_assoc oisga 
  join shipment s on oisga.ORDER_ID = s.PRIMARY_ORDER_ID 
where 
  s.STATUS_ID = 'SHIPMENT_SHIPPED' 
group by 
  ORDER_ID, 
  SHIP_GROUP_SEQ_ID 
having 
  item_count > 1;
```

Result:

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/dd50989c-6fcf-4c23-8c2a-d05e0a352848)
