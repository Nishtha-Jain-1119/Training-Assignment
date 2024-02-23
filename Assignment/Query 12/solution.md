12. Maximum units fulfilled by location:
    * Identify the location that has fulfilled the maximum number of units. This provides insights into the efficiency of different fulfillment centers.
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

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/b2115fc6-7807-42af-bd93-5d7a02dece2e)
