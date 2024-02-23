8. Orders that have more than one item in a single ship group.

Solution:
```sql
select 
  ORDER_ID, 
  SHIP_GROUP_SEQ_ID, 
  count(ORDER_ITEM_SEQ_ID) as item_count 
from 
  order_item_ship_group_assoc oisga 
group by 
  ORDER_ID, 
  SHIP_GROUP_SEQ_ID 
having 
  item_count > 1;
```

Result:

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/c2001342-a31b-4381-bfde-ee29eb8aebc1)
