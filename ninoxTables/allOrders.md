# All Orders

All orders is a simple single record dashboard.

It contains a button to return to [home](home.md).

It also contains a view which displays all [orders](salesOrders.md) which are not of state 'Address' and which are not considered newOrders (i.e. have no order items).

It is similar to the [order management](salesOrderDash.md), but is slightly more stripped down.

As is similar with many other tables, it includes the displayRecordButtons formula, which contains the [displayRecordButtons](../ninoxGeneral/globalFunctions/displayRecordButtons.md) global function. This formula field is visible when admin mode is activated, and will hide the create/copy/print/delete buttons if admin mode is not activated.
