3. Average number of shipments per month:	
    * Calculate the average number of shipments made per month by dividing the total number of shipments by the number of months.

Solution:
```SQL
select 
  count(SHIPMENT_ID)/ 12 Avg_Shipments_Per_Month 
from 
  shipment_status ss 
where 
  STATUS_ID = 'SHIPMENT_SHIPPED' 
  and STATUS_DATE >= CURDATE() - INTERVAL 1 YEAR

```
Result:

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/bfbb7bcc-ba46-4dd3-aec8-162362de60d1)
