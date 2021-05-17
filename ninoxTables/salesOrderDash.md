# Sales Order Dashboard

Sales order dashboard is used for order management, accessed via the order management button on the [homepage](home.md), or via the ‘sales order dashboard’ option on the pop out menu.

It is a fairly simple single record table, containing navigation buttons to [Home](home.md)/ [shipments ready to pick](shipmentsReady.md)/ [shipments not ready to pick](shipmentsNotReady.md).

It also has a time period filter, and a new order button to create a blank new order.

Then is a view of sales orders, this displays records in the ‘select formula’ formula field. We do this using a separate formula field so the ‘create picklists’ buttons can access the records quickly without having to re-select them.

Select formula contains all [sales orders](salesOrders.md) records which do not have the ‘address’ order state override, which are not ‘newOrders’ (i.e. have at least one order item), and which are within the specified time period.

The time period filter works using bindings, this means its value is stored in memory, and different users can choose different options, it filters select formula by calculating the start of the specified time period, and checking the order creation date is greater than it.

The view itself has orders grouped by states, with a number of count/ sum fields.

The create picklists buttons both work almost identically, the only difference being one filters the orders in ‘select formula’ for parked orders, and the other filters for backordered orders

The buttons work by filtering ‘select formula’ by order state, and then filtering the resulting orders for only those with ‘all items ready?’, we then sort this list so the oldest orders are prioritised.

The list of orders is then looped through, for each, we check ‘all items ready?’ Is still true (as another order could have used packets required for that order), if it is true, we proceed to make the picklist.

The process of making the pick list is very similar to the create pick list button on the ‘sales order’ record.

The main difference between this process and that button is that as we check all items are definitely ready, we do not need to perform a check for each individual item and think about splitting the order items into multiple shipment lines.

instead, we can iterate over all of the items (where qty remaining to assign to shipments/ cn’s > 0), create a shipment line, and add them to the shipment just created.

The main difference here is, as we know all items are ready, we do not need to check if each individual item is ready, instead we can iterate over all of the items that have still not been assigned to a shipment, create a shipment line, and add the shipment line to the shipment created.

Once items have been iterated over, the same is done for additional costs (e.g. shipping) not yet assigned to a shipment.
