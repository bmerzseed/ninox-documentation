# Home

The Home table is used as the central navigation point for users of the system.

There are 4 different sections of navigation options

- order management
  - Containing links to anything related to order processing
- New packets and adjustments
  - Containing links to anything related to the printing/ filling of packets, or the adjustment of batches/ seedlots
- reports
  - Containing a series of filterable views which can be used by the user to look at batches/ seedlots/ invoices/ shipments
- purchasing
  - Containing links to anything users may need related to purchase orders

The buttons on this table primarily work via the 'openTable()' ninox inbuilt function, for some areas we use 'openRecord()' instead, usually for a specific reason.

- e.g. when opening the [sales order dashboard](salesOrderDash.md), we select the first record in that table, set the time period value (if it is not already set in memory), and open that record. We do this as we're using in memory bindings, for which default values cannot be set.
