1.  Total number of shipments in January 2022 first quarter:
    * Determine the total count of shipments made during the first quarter of 2022, specifically in the month of January.
  
Solution
```SQL
select 
  count(distinct SHIPMENT_ID) AS First_Quarter_Shipment_Count, 
  (
    select 
      count(distinct SHIPMENT_ID) 
    from 
      shipment_status ss 
    where 
      STATUS_ID = 'SHIPMENT_SHIPPED' 
      and STATUS_DATE between '2022-01-01' 
      and '2022-01-31'
  ) as January_Count 
from 
  shipment_status ss 
where 
  STATUS_ID = 'SHIPMENT_SHIPPED' 
  and STATUS_DATE between '2022-01-01' 
  and '2022-03-31';

```
Result
![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/f24a713f-d056-424c-a1ab-3e85c41a55f7)

