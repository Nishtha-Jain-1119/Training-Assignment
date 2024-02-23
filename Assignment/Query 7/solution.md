7. Payment captured but not shipped order items:
    * Identify orders where payment has been captured, but the items have not been shipped yet or shipment has not yet been created/initiated.
Solution:
```sql
select 
  distinct oi.ORDER_ID 
from 
  order_item oi 
  join order_payment_preference opp on (
    oi.ORDER_ID = opp.ORDER_ID 
    and opp.STATUS_ID = 'PAYMENT_SETTLED'
  ) 
where 
  (
    oi.STATUS_ID != 'ITEM_COMPLETED' 
    and oi.STATUS_ID != 'ITEM_CANCELLED'
  );
```
Result:

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/82c182ad-deaa-4ba7-94d8-07deeb1195cb)
