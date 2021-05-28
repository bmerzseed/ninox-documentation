# Shipment Invoice Lines

Records in this table are children of [shipments](shipmentsAndInvoices.md)

- Meaning each shipment has many shipment lines

Each record in this table also has a relationship with [sales order items](salesOrderItems.md)

- There can be many shipment invoice lines records to a single sales order item
- This is as items can in theory be split into multiple shipments

Each record also has a link to [batches](batches.md)

- this is used to select the batch to allocate the line to
- one batch can have many shipment and invoice lines

Shipment lines are generally accessed via shipment and invoice records, usually using the `open next` button, or via the `open next` button on other shipment and invoice line records.

The table itself serves 2 main purposes

- to store [batch](batches.md) allocation information for the items on a shipment
- to serve as an interface for users

Data from this table is also used in the generation of invoices, and when invoices are sent to Xero.

When looking at records on this table, the first thing shown is a series of information about the packet to be picked

- a link to the order item
  - this was what users saw in previous versions of the system, it remains here as some users prefer to use this when picking
  - it can also be used to access the order item
- the order code
- the product name
- whether the product is a small packet or bulk label
  - with different colours for each
- the quantity to pick
  - if this is greater than 1, it will be highlighted red

Next is the relationship field to batches, this shows if the item has `needToAllocate` != `false`

- we use to use a `popup` relationship here, this had slow loading times often
- once Ninox added the options to use radio buttons, we switched to them as it works out quicker for users to allocate
- this is styled via the `SELECT-BATCH NUMBER styling` field in the admin section
- this field also has an update trigger on it
  - if a line is allocated to a batch with remaining size less than the quantity of the line
  - we change the quantity of this line to the remaining size of the batch
  - and then generate a new line with the difference between the lines new quantity and old quantity
  - this allows lines on 1 shipment to be allocated to multiple different batches.

If `needToAllocate` is `false`

- `how many of this item did you pick?` will instead be shown
- this field is used to confirm items which do not need to be allocated to a batch have been seen by the person picking

Next are 2 buttons

- close
  - this just closes the record..
- open next
  - this works the same as the open next button on the shipment record
  - it gets the first item of the shipments `toPickArray`
  - it pops up that record and closes this record
  - if there is no more items in `toPickArray`, it will just close this record as it has nothing to open

There is also a large admin section, shown if admin mode is activated (`isAdminMode()` = `true`), here you can see:

- QTY
  - this is where the actual quantity value of the shipment line is stored
  - the above quantity values are just formulas of this value
- invoice line order item quantity
  - this is the `order item line quantity` displayed on the invoice
  - it was created as it appeared confusing to users when the total order item line quantity appeared multiple times where shipment lines were split between multiple batches
- shipments
  - this is the relationship field to the shipment record
- TAXABLE...
  - These were created by Tom from Arctec
  - they are fields used in the Xero integration
- Vat Amount/ Line Inc Vat/ Line Ex Vat
  - these fields are all used in invoice total calculations, and displayed on the invoice
- SELECT - BATCH NUMBER styling
  - this is used to style the batch selection radio buttons
  - it works by setting custom css styling for the `.choiceradio-item-text` class
- readyToAllocate
  - Determines whether a shipment is ready to allocated
  - `true` if
    - the item is already allocated
    - there is sufficient quantity of the saleable product to allocate to
- allocated
  - `true` if
    - if the product has `needToAllocate` != `false`
      - if is has been allocated to a batch number
    - else
      - if `how many of this item did you pick` has a value entered
