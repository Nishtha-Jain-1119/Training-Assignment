4. What is the total number of orders originating from New York?

Query
```SQL
select 
  count(distinct or2.ORDER_ID) 
from 
  order_role or2 
  join party_contact_mech_purpose pcmp on or2.PARTY_ID = pcmp.PARTY_ID 
  join postal_address pa on pa.CONTACT_MECH_ID = pcmp.CONTACT_MECH_ID 
where 
  or2.ROLE_TYPE_ID = 'PLACING_CUSTOMER' 
  and pcmp.CONTACT_MECH_PURPOSE_TYPE_ID = 'SHIPPING_LOCATION' 
  and pa.city = 'New York';
```

Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/34756e90-f0ee-4ca7-94bf-4fb6dc0aae63)

Query with different approach
```SQL
select 
  count(distinct s.PRIMARY_ORDER_ID) as orders_count 
from 
  shipment s 
  join postal_address pa on s.ORIGIN_CONTACT_MECH_ID = pa.CONTACT_MECH_ID 
where 
  (
    s.SHIPMENT_TYPE_ID = 'SALES_SHIPMENT' 
    or s.SHIPMENT_TYPE_ID = 'PURCHASE_SHIPMENT'
  ) 
  and (
    s.STATUS_ID = 'PURCH_SHIP_SHIPPED' 
    or s.STATUS_ID = 'SHIPMENT_SHIPPED'
  ) 
  and pa.CITY = 'New York';
```

Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/d4f93db1-0e65-40fa-9c1f-638f38ee2ae2)
