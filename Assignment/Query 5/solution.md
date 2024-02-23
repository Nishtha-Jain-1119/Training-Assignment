5. Last week imported orders & items count:
    * Identify and count the orders and items that were imported in the system during the last week.
Solution:
```sql
select 
  count(distinct oh.order_id) as order_count, 
  count(oh.order_id) as item_count 
from 
  order_header oh 
  join order_item oi on oh.ORDER_ID = oi.ORDER_ID 
where 
  oh.ENTRY_DATE >= curdate() - INTERVAL 1 WEEK;

```
Result:

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/dab59afd-085e-4a5d-83c1-d85103adb283)
