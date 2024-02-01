 1. How many single-item orders were fulfilled from warehouses in the last month?

Query
```SQL
select 
  count(*) as ORDER_COUNT (
    select 
      oi.ORDER_ID, 
      oi.STATUS_ID, 
      oisg.FACILITY_ID, 
      count(oi.ORDER_ITEM_SEQ_ID) as item_count 
    from 
      order_item oi 
      join order_item_ship_group oisg on oisg.ORDER_ID = oi.ORDER_ID 
      join order_status os on (
        os.ORDER_ID = oi.ORDER_ID 
        and os.ORDER_ITEM_SEQ_ID = oi.ORDER_ITEM_SEQ_ID
      ) 
      join facility f on f.FACILITY_ID = oisg.FACILITY_ID 
      join facility_type ft on f.FACILITY_TYPE_ID = ft.FACILITY_TYPE_ID 
    where 
      os.STATUS_ID = 'ITEM_COMPLETED' 
      and ft.PARENT_TYPE_ID = 'DISTRIBUTION_CENTER' 
      and os.STATUS_DATETIME >= curdate() - INTERVAL 1 month 
    group by 
      ORDER_ID 
    having 
      item_count = 1
  ) as tt;

```
Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/592e6eee-d0fd-4e32-a2cc-38fec23115c8)

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/0f24ef3b-5198-4ac2-a0a1-ea8c6c93ed31)
