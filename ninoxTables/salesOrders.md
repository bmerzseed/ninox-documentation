# Sales orders

The sales orders table is central to the systems order management functionality, and has links to many other areas of the system.

Given it is the main table of order management functionality, it has many child tables relating to this functionality, some of which have their own child tables (represented by identation).

- [Order Items](salesOrderItems.md)
- [Shipments & Invoices](shipmentsAndInvoices.md)
  - [Invoices View](invoicesView.md)
  - [Shipment/ Invoice line items](shipmentInvoiceLines.md)
- [Additional costs](additionalCosts.md)
- [Payments](payments.md)
- [Credit Notes](creditNotes.md)
  - [Credit note refunds](creditNoteRefunds.md)
  - [Credit note items](creditNoteItems.md)
  - [Credit note costs](creditNoteCosts.md)

There are also a few important (non composition relationships)

- [Email form](emailForm.md)
- [Delivery/ billing addresses](addresses.md)
- [Customers](customers.md)

And a relationship to [saleable products](saleableProds.md) which adds form functionality to add items to the order.

Records in this table are generally accessed from 2 places by users

- [order management](salesOrderDash.md)
- [all orders](allOrders.md)

In admin mode, they can also be accessed directly through the table

Orders can be added to the Ninox system in 2 ways

- firstly via the `new order` buttons on the [homepage](home.md) and the order management dashboard
  - these orders will have SO-XXXX order codes
  - e.g. SO-1975
- or via Shopify, through the [shopify orders to Ninox](../integromatScenarios/shopifyOrdersToNinox.md) integromat scenario
  - these orders will have #-XXXXX order codes
    - e.g. #11931
  - they will also have the shopify import state set to true, this locks users from editing some areas of the order which would otherwise be accessible.

At the top of the table is some information about the order

- The customer (relationship field)
- The delivery and billing addresses (relationship fields)
- When the order was placed
- The order code
- The customer reference
- Order state & state override
  - `If` the `order complete` boolean field is set on the order, the state will be completed
    - `order complete` is generally set once a shipment is completed that sets the order state to be completed, sometimes this fails to set, these cases are caught by the [set unset ninox order complete states](../integromatScenarios/setUnsetOrderStates.md) integromat scenario.
    - this exists to avoid the expensive order state calculation on every single order in various places in the system
  - `Else if` the order state override is set, the order state will be equal to this.
  - `Else`, we calculate the state
    - `If` nothing has been added to shipments/ credit notes, the order is `parked` (default state)
    - `Else if` the number of order items in shipments/ cn's is not equal to the total quantity of items on the order, the order is `backordered`
    - `Else if` the number of items in shipments is not equal to the number of batch allocated items, the order is `placed`
    - `Else if` all shipments are completed, the order is `completed`
    - `Else`, the order is `Allocated`, this state usually only exists very briefly between all items being alocated and the user completing the shipment
  - As the state calculations are using `else`, we don't need to check for every condition at each step, only a single defining condition of that state.
- Discount
  - This field is generally unused
  - if it is set, any items added will automatically be given that discount
  - the discount can be applied to existing items via the `apply order discount to existing items` button
    - this only works for orders which are not from Shopify, and which are not `completed`

Next are a number of formula fields

- order items in shipments
- order items in cn's
- order items in shipments & cn's
  - sum of order items in shipments & order items in cn's
- allocated order items
  - sum of order item quantity which has been allocated to a batch within a shipment
- wholesale prices
  - `true` if the attached customer is a `retailer`
  - if this is `true`, wholesale prices are used rather than retail prices when manually adding items to the order.
- order weight
  - total weight of all order items, used in postage calculations
- total additional costs
  - sum of additional costs
    - mainly shipping
    - sometimes other things e.g. shares
- total order items value
- total order value
  - total additional costs + total order items value - credit note values
- amount paid
  - sum of payments
- paid
  - if amount paid > total order value

Then, functionality to create picklists (shipments) and to duplicate the order

- all items ready?
  - if there are no items left to assign to shipments/ cn's this will be `false`
  - if all items remaining to be assigned to shipments/ cn's have sufficient available quantity, it will be `true`
    - available quantity includes the quantity in batches (which do not have to be assembled yet) minus quantity which has already been assigned to a shipment
- the create picklist button
  - this works similarly to the buttons on the order management view used to create picklists (though it obviously only creates a picklist for this order)
  - the main difference is that those buttons will only make picklists if `all items ready` is true (and therefore all items can be added to a shipment)
  - this button will create partial picklists, missing out items which are not ready (thus making the order state `backordered`)
  - this button is much more rarely used now.
- the duplicate order button
  - this duplicates the order and changes a number of things
  - a new order code (SO-) is generated
  - shipments, payments and credit notes are deleted from the duped order
  - the original orders comments are added, with a note of which order it is a duplicte of
  - order states & shopify fields are cleared
  - time placed is set to `now()`

Show view is a choice box used to display/ hide different views on a sales order record. It shows these via the relationships mentioned above.
The available options are:

- order items
- shipments
- payments
- invoices
- emails
- credit notes

Options to add to order is only visible when the `canAddNewItems` formula is `true`.

- add order lines
  - allows users to select saleable products, assign a quantity, and add those products to an order
  - can optionally add a discount
  - default add order item quantity can be set to use a default quantity when adding items
  - integrated with stock control functionality
    - users will be warned when adding items which should not be sold
    - if the sale state changes as a result of adding an item, it will trigger the [stock control updates](../integromatScenarios/stockControlUpdates.md) integromat scenario
- add shipping
  - automatically calculates which shipping to use based on the order weight
  - creates, populates and links an additional cost record
- add additional costs
  - allows manual adding of additional costs to an order
  - mainly used for shares
- add payments
  - allows a payment to be added with a payment method & payment amount
  - as mentioned above, this option is possible to use without `canAddNewItems` being `true`.
  - it works via an on update trigger on the table, setting `options to add to order` to `add payments` if
    - the order is not paid
    - show view is 3
    - not `canAddNewItems`
  - in its current form, this workaround is slightly clunky, it may be something to look at

more functionality...

- save
  - does not actually save..
  - just closes the record
- default add order item quantity
  - the default quantity set when adding order lines
  - useful when adding a large order with many items quantity 5
- create credit note
  - creates and links a new credit note record to this order record
- order complete
  - set when a shipment is complete which sets the `order state` to `completed`
  - occasionally, when this fails, it is set by the [set unset order states](../integromatScenarios/setUnsetOrderStates.md)
  - if this is true, the `order state` will automatically be `completed`
    - this makes `order state` calculation much quicker over thousands of records

This section contains fields and buttons only visible if admin mode is activated (`isAdminMode()` = `true`)

- canAddNewItems
  - if `true`
    - `options to add to order` will show
  - `true` if
    - the order is not `completed`
    - the order is not a shopify import
    - a customer has been selected
- validAddNewItems
  - if `true`
    - the user will be able to add that line to the order
  - `true` if
    - the order line the user is trying to add has a product selected
    - the order line the user is trying to add has a quantity > 0
- newOrder
  - if `true`
    - the order will be hidden from some views
      - e.g [order management](salesOrderDash.md)
  - `true` if
    - the number of order items is 0
- Items missing to create picklists
  - number of order items which:
    - have quantity left to be assigned to shipments
    - have insufficient quantity remaining of that product to add the items to a shipment
  - displayed on the order management table
- Total VAT
  - sum of all VAT on the order
  - includes both order items VAT and additional costs VAT
- Items ex VAT
  - sum of the ex VAT amount of all order items on the order
- Costs ex VAT
  - sum of the ex VAT amount of all additional costs on the order
- Cancel Order
  - Double checks the user would like to cancel the order
  - if `yes`
    - sets the override to canceled
    - sets the order complete state to false
    - deletes all shipments
    - if there was at least 1 shipment which is complete
      - sends an email to `mandamerz@seedcooperative.org.uk` alerting of this
- Email pro-forma invoice
  - this allows users to send an invoice prior to any [shipment and invoice](shipmentsAndInvoices.md) being created/ completed
  - it has never actually been used.. and the print layout (`Invoice` on this record) may need some changes too..
- display records buttons/ hide create record on popup
  - display record buttons works similarly to almost every other table..
    - it uses the [displayRecordButtons()](../ninoxGeneral/globalFunctions/displayRecordButtons.md) global function
  - hide create record on popup is much less used
    - its purpose is to hide the `create record` button when selecting a saleable product to add to order
    - it works by calling the [hideCreateRecordOnPopup()](../ninoxGeneral/globalFunctions/hideCreateRecordOnPopup.md) global function if admin mode is not activated (i.e. `not isAdminMode()`)
