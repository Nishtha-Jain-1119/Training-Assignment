Fetch the following columns for created orders. These should be sales orders.
- ORDER_ID
- TOTAL_AMOUNT
- PAYMENT_METHOD
- SHOPIFY_ORDER_NAME

NOTE: 
1. The total amount represents the total amount of the order.
2. The payment method is the method by which payment was made, like Cash, mastercard, visa, paypal, etc.

```SQL
select 
  oh.order_id, 
  oh.GRAND_TOTAL as TOTAL_AMOUNT, 
  pmt.PAYMENT_METHOD_CODE as PAYMENT_METHOD, 
  oi.ID_VALUE as SHOPIFY_ORDER_NAME 
from 
  order_header oh 
  join order_payment_preference opp on opp.ORDER_ID = oh.ORDER_ID 
  join payment_method_type pmt on opp.PAYMENT_METHOD_TYPE_ID = pmt.PAYMENT_METHOD_TYPE_ID 
  left join order_identification oi on (
    oi.ORDER_ID = oh.ORDER_ID 
    and oi.ORDER_IDENTIFICATION_TYPE_ID = 'SHOPIFY_ORD_NAME' 
    and (
      oi.THRU_DATE is null 
      or oi.THRU_DATE > curdate()
    )
  ) 
where 
  oh.STATUS_ID = 'ORDER_CREATED' 
  and oh.ORDER_TYPE_ID = 'SALES_ORDER';

```
Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/e09ab5c1-dbd7-4b5f-98be-d2b01f6ee056)

>**Note**:
When using a left outer join, orders with a null value for SHOPIFY_ORDER_NAME will also appear, as opposed to using inner join where only those with a value exist.
