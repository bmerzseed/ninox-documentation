# Shipments & Invoices

The shipments and invoices table is used to store information about picklists/ shipments, invoice print views are also generated from this table.

The table is a child of the orders table, meaning any 1 sales order can have many ‘shipment & invoices records’.

The ‘shipments & invoices’ table also has 3 one to many relationships (i.e. 1 ‘shipment and invoices’ record can have many of these other records).

Firstly with ‘shipment & invoice line items’

- Each links to a ‘sales order items’ record, there can be many ‘shipment & invoice line items’ for each ‘sales order item’. When the ‘shipment and invoices’ record is generated via the generate picklists button, ‘shipment & invoices line items’ records are created for all ‘sales order items’ on the order with ‘quantity remaining to be assigned to shipments/cn’s’ > 0, these lines are then linked to the shipment record.

Secondly with ‘additional costs’

- Additional costs (very often shipping) do not need to be allocated, but we only want them to on 1 invoice, so when generating ‘picklists’/ ‘shipment and invoice’ records via the generate picklists buttons, we link any unlinked cost records the ‘shipment & invoices’ record generated in order to ensure the customer sees these costs on at least 1 invoice.

And finally with ‘invoices view’

- When a shipment is completed (via the complete shipment button), we also generate an ‘invoices view’ record and link it to the ‘shipment and invoices record’, this means under normal circumstances, there will only ever be 1 ‘invoices view’ record for each ‘shipment and invoices’ record. This table is unused, and primarily serves as a way to view the invoice data without opening a PDF.

Functionally, the shipment record itself primarily serves as the entry point to the picking process.

The records are generally accessed via the ‘shipments to pick’ table, which displays a list of all the ‘shipment and invoices’ records which are not completed, and are ‘readyToPick’

- readyToPick is a formula value on the ‘shipment and invoices’ record. It is true if all ‘shipment and invoices’ lines are themselves ‘readyToAllocate’. We calculate this by taking the min value of all of the lines ‘readyToAllocate’ value.
  - We consider lines as ‘readyToAllocate’ either if they are already allocated, or if there is enough of that ‘saleable product’ made up to allocate them.

The shipment displays a variety of fields/views/buttons, exactly which will depend on A: if the shipment is completed/ ready to be completed, and B: if admin mode is activated.

Regardless of these, the record always shows a link to the order record, the shipment code, and the customers name.

It also displays up to 3 views showing items on the order, 1 for small packets, 1 for bulk labels, and 1 for ‘other items’, such as catalogues. These have conditional formatting to show whether or not a batch has been allocated, and a formula which we sort by, this prefixes the name with either ‘a’ or ‘b’ depending if they have been allocated or not, this allows the ‘not allocated’ lines to be shown at the top of the view.

If the shipment IS NOT complete, you will also see

- varieties remaining to allocate & quantity remaining to allocate
  - these are formulas which show the number of unallocated shipment lines, and the sum of the quantity of unallocated shipment lines respectively.
- Open next item button
  - this gets the next product to pick from the ‘nextProductToPick’ field, it then selects the first shipment line for that product that has not been allocated, it then opens that ‘shipment line’ record for allocation.

If the shipment IS complete,

- A message giving the user that completed it, and what time it was completed at
- A print invoice button
  - this sends data to the ‘ninox reprinting’ scenario on integromat
- Go to invoice record
  - this opens the ‘invoices view’ record created on shipment completion
- send email invoices
  - this creates a new ‘email form’ with prefilled information (and the invoice attached), and links it to the order record in order to keep a log.
- regenerate PDF
  - this button is not used often anymore, but it regenerates the invoice PDF attached to this record, allowing the ‘print invoice’ button to work if no invoice pdf is attached to this record

If the shipment IS NOT complete, but is READY to be completed

- Complete and print button
  - This button sets the shipment to complete, and also sets the shipment completed time/ completed by fields to the current time/ user
  - It calculates the ‘invoice code’ for the ‘invoices view’ record, and generates the record
  - It generates the invoice PDF, and saves it to this record/ the order/ the invoices view record, and also sends the URL to the invoice to the ‘a4 printing’ scenario on integromat. Depending on if the order is paid or not, it will use either the ‘Invoice’ print view, or the ‘Unpaid’ print view.
  - If the order is now completed as a result of the shipment being completed, the ‘order complete’ state on the order is set to complete.
    - NOTE, this sometimes will not set correctly (usually no more than once every few days), if this happens, the ‘set unset ninox order complete states’ integromat scenario should set it.

If admin mode IS activated

- the fields/ formulas hidden outside of admin mode are rarely needed, and are primarily just for diagnostic purposes/ used as part of functionality
- the shipment complete/ completed by/ completed time fields are set by the complete and print button
- toPickArray contains a list of the products remaining to pick. It is grouped into 3 sections, first the small packets, then the bulk labels, then other items, within each group, products are sorted by name. This is used for determining whether a shipment is ready to complete, and the first item is also taken by ‘nextProductToPick’ to allow the ‘open next’ button to function’
- Calculated total fields, displayed on the print view.
- A button to manually send an invoices to Xero (though in the large majority of cases this will be done automatically via the scheduled ‘overnight routine to create Xero invoices from Ninox 11am and 9pm) scenario. There is also a state to show whether or not an invoice has already been sent to Xero, and a field to show the date when an invoice was posted to Xero.
- There is also the ‘display record buttons’ formula, which appears on almost every table on the database, this is used to hide the add/ create/ delete buttons in the top right corner unless admin mode is activated.
