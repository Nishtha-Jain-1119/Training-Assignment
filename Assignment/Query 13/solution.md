Fetch the following details for orders completed in August of 2023.
- PRODUCT_ID
- PRODUCT_TYPE_ID
- PRODUCT_STORE_ID 
- TOTAL_QUANTITY
- INTERNAL_NAME 
- FACILITY_ID
- EXTERNAL_ID 
- FACILITY_TYPE_ID 
- ORDER_HISTORY_ID 
- ORDER_ID
- ORDER_ITEM_SEQ_ID
- SHIP_GROUP_SEQ_ID

Solution
```SQL
select 
  oi.PRODUCT_ID, 
  p.PRODUCT_TYPE_ID, 
  oh.PRODUCT_STORE_ID, 
  oi.QUANTITY as TOTAL_QUANTITY, 
  p.INTERNAL_NAME, 
  oisg.FACILITY_ID, 
  oh.EXTERNAL_ID, 
  f.FACILITY_TYPE_ID, 
  oh2.ORDER_HISTORY_ID, 
  oh.ORDER_ID, 
  oi.ORDER_ITEM_SEQ_ID, 
  oisga.SHIP_GROUP_SEQ_ID 
from 
  order_header oh 
  join order_item oi on oh.ORDER_ID = oi.order_id 
  join order_item_ship_group_assoc oisga on oisga.ORDER_ID = oi.ORDER_ID 
  and oisga.ORDER_ITEM_SEQ_ID = oi.ORDER_ITEM_SEQ_ID 
  join order_item_ship_group oisg on oisg.ORDER_ID = oisga.ORDER_ID 
  and oisg.SHIP_GROUP_SEQ_ID = oisga.SHIP_GROUP_SEQ_ID 
  join order_status os on os.ORDER_ID = oi.ORDER_ID 
  join product p on oi.PRODUCT_ID = p.PRODUCT_ID 
  join facility f on f.FACILITY_ID = oisg.FACILITY_ID 
  left join order_history oh2 on oh2.ORDER_ID = oi.ORDER_ID 
  and oh2.ORDER_ITEM_SEQ_ID = oi.ORDER_ITEM_SEQ_ID 
where 
  os.STATUS_ID = 'ORDER_COMPLETED' 
  and (
    os.STATUS_DATETIME between '2023-08-01' 
    and '2023-08-31' );
```

Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/c3f0bfaa-cf2d-432b-9867-7c55e77abe23)
![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/70fbc3a7-6e6c-4376-bba2-defd45141a1d)

