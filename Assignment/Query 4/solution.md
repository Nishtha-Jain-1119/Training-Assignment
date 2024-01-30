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
