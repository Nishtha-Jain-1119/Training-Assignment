Find all the orders whose two or more items are canceled but the orders are still in the approved status.

Solution
```SQL
SELECT 
  oh.order_id, 
  oh.STATUS_ID, 
  COUNT(ORDER_ITEM_SEQ_ID) AS completed_items_count 
FROM 
  order_header oh 
  JOIN order_item oi on oh.ORDER_ID = oi.ORDER_ID 
where 
  oh.STATUS_ID = 'ORDER_APPROVED' 
  AND oi.STATUS_ID = 'ITEM_CANCELLED' 
group by 
  ORDER_ID 
having 
  count(ORDER_ITEM_SEQ_ID)>= 2;
```

Result

![image](https://github.com/Nishtha-Jain-1119/SQL-Queries/assets/127538617/f99b1900-76cc-4be6-9b09-eaad1b00b695)
