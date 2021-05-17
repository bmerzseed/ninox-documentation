# getNextManualOrderCode()

This function is used to generate SO- order codes, it works by selecting the numbers record and getting the current order number.

It then prefixes it with SO-, and increments the value in the numbers record by 1, it then returns the order code

It is called once the first order item has been added to an order, the generated order code is then set on that order.
