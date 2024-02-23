4. Shipped units By Location:
    * Identify the number of units that have been shipped, categorized by different locations. Gain insights into the distribution of shipped units across various locations.

Solution:
```sql
select 
  sum(si.QUANTITY) UNIT_COUNT, 
  s.ORIGIN_FACILITY_ID 
from 
  shipment s 
  join shipment_item si on s.SHIPMENT_ID = si.SHIPMENT_ID 
where 
  s.status_id = 'SHIPMENT_SHIPPED' 
group by 
  s.ORIGIN_FACILITY_ID 
order by 
  UNIT_COUNT desc;
```

Result:

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/9ae360b3-284d-4529-ab4a-8faa6d926690)

