# Credit notes

Credit notes are part of the order management functionality, they are children of [sales orders](salesOrders.md)

- meaning there is a composition relationship
- there can be many credit notes to a single sales order

Credit note records are created via the `create credit note` button on a sales order record, this will take the user to the credit note they have created.

Users can access existing credit notes via the `credit notes` option under `show view` on an order.

Credit notes have a number of other relationships to their own subtables, these are all composition one to many relationships (one credit note record can have many of the other records)

- [credit note items](creditNoteItems.md)
  - stores information about the individual lines of the credit notes
  - linked to a sales order item
- [credit note refunds](creditNoteRefunds.md)
  - stores information about refunds sent to customers as a part of this credit note
  - akin to [payments](payments.md) but in reverse...
- [credit note costs](creditNoteCosts.md)
  - stores information about [additional costs](additionalCosts.md) credited on the credit note
  - linked to an additional cost record

They also have relationships with [sales order items](salesOrderItems.md) and [additional costs](additionalCosts.md)

- There are many credit notes to a single sales order item/ additional cost
- though these are technically relationships, they only serves the purpose of allowing users to create [credit note items](creditNoteItems.md), linked to the selected order item or [credit note costs](creditNoteCosts.md) linked to the selected additional cost

At the top of the credit note record form view (which users see) is the following

- the standard navigation bar with links to [home](home.md) and the ability to close the record
- the credit note code
  - unique identifier
  - generated when the credit note is generated
  - CN-[order number]
- Customer/ customer ref
  - formula fields which the customer name/ customer reference from the sales order record
- credit note costs total (ex VAT)
  - sum of ex VAT total from linked credit note costs records
- credit note items total (ex VAT)
  - sum of ex VAT total from linked credit note items records
- credit note total (vat amt)
  - sum of VAT from linked credit note items and credit note costs records
- credit note total (inc VAT)
  - sum of inc VAT (ex vat + vat amt) values from linked credit note items and credit note costs records
- amount refunded
  - sum of the refund amount of linked credit note refunds records
  - this is expected to be a negative value, though it'd work as a positive value, the maths is setup such that a negative value gives the correct results
- amount to refund
  - difference berween the inc VAT credit note total and the amount refunded
- comments
  - displays the comments from the parent sales order record within a formula field

Next is the `show view` choice section, this works the same as the `show view` section on many other tables throughout the system, showing different views depending on the selected choice

- items
  - shows a list of attached credit note items
  - also has an option to manually create credit note items and link them to a sales order item (as mentioned above)
  - and an option to automatically add all items on the linked order which have `quantity remaining to assign to shipments/ cn's > 0`
- refunds
  - shows a list of attached credit note refunds
  - also has a section allowing users to add a refund consisting of a refund amount and a refund method
  - refund amount should be less than 0
- costs
  - shows a list of attached credit note costs
  - also has an option to add an additional cost to the credit note manually
  - and an option to automatically add all additional costs which are not yet on a shipment/ credit note

Finally is the admin section, this is only visible if `isAdminMode()` is `true`

- sales orders
  - relationship field which links to the parent sales order record
- creation datetime
  - creation datetime field which is populated when the credit note is created
- posted to Xero/ Date posted to Xero/ Post Credit Note to Xero
  - These fields are part of the integration which is used to send credit notes through to Xero
  - posted to Xero
    - must be `false` or the user must be an admin to send a credit note through
    - set to `true` once the credit note has been sent to Xero via integromat
  - date posted to Xero
    - set to the current datetime once the invoice has been sent to Xero via integromat
  - Post credit note to Xero
    - triggers the [createXeroCreditNote](../ninoxGeneral/globalFunctions/createXeroCreditNote.md) global function
    - Assuming the credit note is okay, and passes the scenarios filters, it will be sent to Xero and the date posted/ boolean posted fields will be filled.
