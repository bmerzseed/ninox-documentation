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
  - `Else`, if the order state override is set, the order state will be equal to this.
  - `Else`, we calculate the state
    - `If` nothing has been added to shipments/ credit notes, the order is `parked` (default state)
    - `Else if` the number of order items in shipments/ cn's is not equal to the total quantity of items on the order, the order is `backordered`
    - `Else if` the number of items in shipments is not equal to the number of batch allocated items, the order is `placed`
    - `Else if` all shipments are completed, the order is `completed`
    - `Else`, the order is `Allocated`, this state usually only exists very briefly between all items being alocated and the user completing the shipment
  - As the state calculations are using `else`, we don't need to check for every condition at each step, only a single defining condition of that state.
