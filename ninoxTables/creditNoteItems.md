# Credit note items

The credit note items table is part of the credit note functionality, records of this table are a child of [credit notes](creditNotes.md) (1 credit note to many credit note items).

Records in this table also have a link to [sales order items](salesOrderItems.md) (1 sales order item to many credit note items). Quantities of an item assigned to a credit note are summed in the `quantity assigned to cn's` formula field.

The idea of this table is to allow sales order items to be credited, it works in a very similar way to sales order items being added to a [shipment](shipmentsAndInvoices.md).

Along with a link to a sales order item, there is also a quantity field, this

There are also a number of formula fields, some used for totals on the credit note record, and some made by Tom as part of the credit note Xero integration (via the [integromat scenario](../integromatScenarios/createCNXero.md))

Credit note items records are created via the `items` option on `show view` on the parent credit note.

They can either be added one by 1, with quantities manually set, or everything with remaining quantity to assign to shipments/ cn's can be added via the `add all unassigned items` button.
