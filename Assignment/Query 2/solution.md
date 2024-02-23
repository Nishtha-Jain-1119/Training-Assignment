2. Shipment by Tracking number:
    * View or analyze shipments based on their unique tracking numbers. Each shipment is identified and tracked using a specific tracking number.
  
 Solution:
 ```SQL
select 
  distinct TRACKING_CODE, 
  SHIPMENT_ID 
from 
  shipment_package_route_seg sprs 
where 
  sprs.TRACKING_CODE is not null;

```

Result:

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/50edf901-7494-465d-a192-a0b384a02464)
