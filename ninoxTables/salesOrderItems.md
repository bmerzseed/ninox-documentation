# Sales order items

Sales order items are children of [sales orders](salesOrders.md)

- this is a composition relationship
- there are many sales order items to a single sales order

They are also linked to a [saleable product](saleableProds.md)

- there are many sales order items to a single saleable product
- this relationship is used to link to to the product the sales order item is for

Additionally, they have a relationship with both [shipment and invoice lines](shipmentInvoiceLines.md), and [credit note lines](creditNoteItems.md)

- these are both one to many relationships
  - i.e. one credit note item to many shipment lines/ cn lines
- they are used to `assign` quantites of the order item line to credit notes/ shipments
  - this means the quantity of a shipment/ order item line will not necessarily be equal to the order item line quantity, as items can be split between multiple shipment lines/ credit note lines/ a mix of the two
  - however, the sum of the quantities should never exceed the order item line quantity

Next are a series of information fields

- order item line quantity
  - number of that item on this line of the order
- line item discount
  - generally this will be 0
  - either set when adding items to the order
  - or can be set after the fact
    - there is an update trigger on this field to automatically update the line price/ line VAT if it is changed later
- line item price (exc discount)
  - this is set when the item is created
  - if a discount is later added, the value in the exc discount field is used to calculate the new inc discount amount
- line item price (inc discount)
  - generally the same as the exc discount amount
  - if a discount is set, this will be a percentage of the exc discount figure
  - this is the value used on the invoice/ invoice calculations
- line item VAT (exc discount)
  - this is set when the item is created
  - if a discount is later added, the value in the exc discount field is used to calculate the new inc discount amount
- line item VAT (inc discount)
  - generally the same as the exc discount amount
  - if a discount is set, this will be a percentage of the exc discount figure
  - this is the value used on the invoice/ invoice calculations

After these are a number of formula fields:

- total line price (inc VAT)
  - line item price (inc discount) \* order item line quantity
- line weight
  - total weight of line used for postage calculations
  - weight of prod \* line quantity
- quantity assigned to shipments
  - quantity of this item on shipments
  - sum of quantities of attached [shipment lines](shipmentInvoiceLines.md)
- quantity assigned to cn's
  - quantity of this item on credit notes
  - sum of quantites of attached [credit note lines](creditNoteItems.md)
- quantity assigned to shipments + cn's
  - sum of 2 above
  - used to determine if item needs assigning to shipment/ credit note when pressing buttons to automatically generate them/ add items to them
- quantity allocated to batches
  - sum of quantity of shipment lines which have been allocated to a batch
- quantity remaining to assign to shipments/ cn's
  - line quant - quantity assigned to shipments/ cn's
  - if 0, no more can be added to shipment/ cn's
- quantity remaining to allocate to batches
  - line quant - quantity allocated to batches

Next, the `show view` choice field which appears on many tables form views

- order item allocations
  - shows a view of all linked shipment lines
- credit note items
  - shows a view of all linked credit note items

Finally, the admin section, this will only be shown if `isAdminMode()` evaluates to `true`

- temp fields - [...] posted to Xero
  - created by Tom
  - used when there were issues with VAT on orders that came from Shopify to figure out affected orders
  - SHOULD now be okay to delete...
- display record buttons/ enable record deletion
  - display record buttons works via the [displayRecordButtons()](../ninoxGeneral/globalFunctions/displayRecordButtons.md) global function
  - it hides the ability to create/ duplicate/ delete records via the icons in the top right corner
  - if admin mode is activated, or enable record deletion has been selected, users are able to override this to delete records
  - users may want to delete records if, when adding an order to the system, they make a mistake on a particular line
