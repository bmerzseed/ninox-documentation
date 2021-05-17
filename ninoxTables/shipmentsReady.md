# Shipments ready to pick

The shipments ready to pick table is a fairly simple single record table.

It contains navigation buttons to [home](home.md)/ [shipments not ready to pick](shipmentsNotReady.md)/ [order management](salesOrderDash.md), and a view showing all shipments where all items are ready to be picked.

The view shows all [shipment and invoices](shipmentAndInvoices.md) records where ‘shipment complete’ is false, and ‘readyToPick’ is true.

readyToPick takes the minimum value of ‘readyToAllocate’ for all lines in the shipment, meaning if ready to pick is false for any of the items, the order will not be ready to allocate, and will instead be shown on the ‘shipments not ready to pick’ table.
