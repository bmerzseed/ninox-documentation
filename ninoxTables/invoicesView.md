# Invoices View

Invoice view records are a child of [shipment](shipmentsAndInvoices.md) records

- i.e. there can be many invoice view records to a shipment record
- however, in actuality there should only ever be a single invoice view record in normal use as records from this table are only created when a shipment is completed

Records of this table will generally be accessed from 2 places

- the `open invoice record` button on a completed shipment
- the [invoices dash](invoicesDash.md) accessed via the [homepage](home.md)

The table itself does the following

- acts as a view of invoice information without opening the invoice PDF
- it also stores an attachment of any completed invoices
- it contains buttons to print the invoice/ send an email
  - these buttons also exist on the shipment record
