# Shipments not ready

Shipments not ready is a simple, single record dashboard table which displays shipments which have not been completed, but are not ready to pick.

It is primarily accessed via a `not ready to pick` button on the [order management](salesOrderDash.md) and [shipments ready to pick](shipmentsReady.md) tables.

It contains some navigation buttons at the top, a view of the `shipments not ready to pick`, and the standard `displayRecordButtons` formula field (containing the [displayRecordButtons](../ninoxGeneral/globalFunctions/displayRecordButtons.md) global function) hidden outside of admin mode

The view itself uses a select statement to show [shipment & invoice](shipmentsAndInvoices.md) records where `readyToPick` is false, and which have not been completed.
