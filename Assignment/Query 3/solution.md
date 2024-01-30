3. In the period following the New Year, what is the number of orders shipped from stores in the first 25 days?

Query
```SQL
select 
  count(s.SHIPMENT_ID) as SHIPPED_ORDERS_COUNT 
from 
  order_item_ship_group oisg 
  join facility f on f.FACILITY_ID = oisg.FACILITY_ID 
  join facility_type ft on f.FACILITY_TYPE_ID = ft.FACILITY_TYPE_ID 
  join shipment s on oisg.ORDER_ID = s.PRIMARY_ORDER_ID 
  and s.PRIMARY_SHIP_GROUP_SEQ_ID = oisg.SHIP_GROUP_SEQ_ID 
  join shipment_status ss on ss.SHIPMENT_ID = s.SHIPMENT_ID 
where 
  ss.STATUS_ID = 'SHIPMENT_SHIPPED' 
  AND ft.PARENT_TYPE_ID = 'PHYSICAL_STORE' 
  AND ss.STATUS_DATE >= '2024-01-01' 
  AND ss.STATUS_DATE < '2024-01-01' + INTERVAL 25 day;
```

Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/c3c6b850-c7ad-4dd3-9289-51c277d38e89)
