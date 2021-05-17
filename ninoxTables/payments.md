# Payments

The payments table is a child of ‘sales orders’, it holds payments made for a particular order.

It has 4 fields:

- Payment Amount
- Payment made
- Payment added by
- Payment method

Payment amount is a numeric value, for the amount of the payment (e.g. 21.24)

Payment made is the time the payment was added, this box is autofilled when a payment is added

Payment added by is the ninox user who added the payment to the system, this is autofilled when a payment is added (for shopify imports it will be blank)

Payment method is a choice box containing different payment sources. These being stripe, cheque, bank transfer and shopify (for shopify imports, payment status will automatically be ‘shopify’).

Orders coming in from shopify will always automatically have a payment added equal to the value of the order, for some orders, which have not actually been paid, these payments will need to be manually deleted.

If a shopify imported order has had its payment deleted (and so its ‘paid’ state has changed to ‘no’), a new payment can be added by going to the ‘payments’ option of ‘show view’ on the relevant order.

For manually added orders, payments can be added by selecting the ‘add payments’ option of the ‘\*OPTIONS TO ADD TO ORDER’ choice box.

The ‘add payment’ button works by creating a new record in the ‘payments’ table, attaching it to the current order, and filling it’s fields in with the values filled in on the ‘add payment’ form on the order.

Orders also contain an ‘amount paid’ formula field, this is a sum of all the payment amounts attached to that order.

If the amount paid is greater than or equal to the order value, the orders ‘paid state’ will be “Yes”, otherwise it will be “No”
