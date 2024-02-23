14. Shipping Refund in the last month:
    * Calculate the refunds issued specifically for shipping charges in the last month.
Solution:
```sql
select 
  sum(ra.AMOUNT) as REFUND_AMOUNT 
from 
  return_status rs 
  join return_adjustment ra on rs.RETURN_ID = ra.RETURN_ID 
where 
  rs.STATUS_ID = 'RETURN_COMPLETED' 
  and rs.STATUS_DATETIME >= CURDATE() - INTERVAL 1 MONTH 
  and ra.RETURN_ADJUSTMENT_TYPE_ID = 'RET_SHIPPING_ADJ';

```

Result:

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/b7cd7807-4fc1-442e-877b-f28ce1c5360f)
