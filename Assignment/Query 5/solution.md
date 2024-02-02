Fetch the following data for completed order items in July of 2023
- ORDER_ID
- ORDER_ITEM_SEQ_ID
- SHOPIFY_ORDER_ID
- SHOPIFY_PRODUCT_ID

Solution
```SQL
select 
  oi.ORDER_ID, 
  oi.ORDER_ITEM_SEQ_ID, 
  oid.ID_VALUE as SHOPIFY_ORD_ID, 
  gi.ID_VALUE as SHOPIFY_PRODUCT_ID 
from 
  order_item oi 
  join order_status os on (
    oi.order_id = os.ORDER_ID 
    and oi.ORDER_ITEM_SEQ_ID = os.ORDER_ITEM_SEQ_ID
  ) 
  left join order_identification oid on oi.ORDER_ID = oid.ORDER_ID 
  left join good_identification gi on gi.PRODUCT_ID = oi.PRODUCT_ID 
where 
  os.STATUS_ID = 'ITEM_COMPLETED' 
  and (
    os.STATUS_DATETIME between '2023-07-01' 
    and '2023-07-31'
  ) 
  and oid.ORDER_IDENTIFICATION_TYPE_ID = 'SHOPIFY_ORD_ID' and gi.GOOD_IDENTIFICATION_TYPE_ID = 'SHOPIFY_PROD_ID'
  and (gi.THRU_DATE is null or gi.THRU_DATE > curdate())
  and (oid.THRU_DATE  is null or oid.THRU_DATE > curdate());

```

Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/7d3c9ab0-e75c-473d-8df4-84f2882832e3)
