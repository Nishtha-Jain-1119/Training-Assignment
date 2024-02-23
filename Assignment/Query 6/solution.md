6. Total $ value of shipments shipped from facility 904/906 to first quarter:
    * Calculate the total monetary value of shipments that originated from facilities 904 and 906 during the first quarter.
Solution:
```sql
select 
  sum(oi.UNIT_PRICE * oi.QUANTITY) as Total_Monetary_Value 
from 
  order_item oi 
  join order_item_ship_group_assoc oisga on (
    oisga.ORDER_ID = oi.order_id 
    and oi.ORDER_ITEM_SEQ_ID = oisga.ORDER_ITEM_SEQ_ID
  ) 
  join shipment s on (
    s.PRIMARY_ORDER_ID = oisga.ORDER_ID 
    and s.PRIMARY_SHIP_GROUP_SEQ_ID = oisga.SHIP_GROUP_SEQ_ID
  ) 
  join shipment_status ss on (
    s.SHIPMENT_ID = ss.SHIPMENT_ID 
    and ss.STATUS_ID = 'SHIPMENT_SHIPPED'
  ) 
where 
  oi.status_id != 'ITEM_CANCELLED' 
  and (
    s.ORIGIN_FACILITY_ID = '904' 
    or s.ORIGIN_FACILITY_ID = '906'
  ) 
  and year(ss.STATUS_DATE)= 2022 
  and month(ss.STATUS_DATE) between 1 
  and 3;
```
Result:

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/ace25efb-0d3d-4dfe-a898-6626bbc9a6bf)
