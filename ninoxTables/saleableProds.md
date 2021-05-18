# Saleable products

Saleable products stores information about products which are sold, for example small packets and bulk labels.

It has a number of relationships

- Firstly, it is a child of [Component Products](componentProds.md)
  - There are many saleable products to one component product

It also has 2 subtables/ children

- [Batches](batches.md)

  - There are many batches to one saleable product

- [Past Sales](pastSales.md)
  - There are many past sales records to a saleable product.
  - Though this is a one to many composition relationship, in reality there should only be one past sales record to a single saleable product record.

Along with a number of other relationships

- [Stock](stock.md)
  - There are many saleable product records to a single stock record.
  - In reality, there is only 1 stock record which (almost) all of the saleable product records are linked to.
  - This relationship is used to display a list of all of the saleable products on the stock record, and whether or not they need to be updated on Shopify.
  - It is also used when the manual 'update stock' button is pressed on that stock record.
- [Stock Groups](stockGroups.md)
  - There are many saleable product records to one stock group record.
  - In order to avoid timeouts, automated stock update checks via [stock group triggers](../integromatScenarios/stockControlTrigger.md) are not done for all products at once, instead they are split into seperate groups
  - At the time of writing this, there are 10 seperate stock groups, across which saleable products are (fairly) evenly split, they are set using the modulus of the ID's
- [Sales Orders](salesOrders.md)
- [Sales Order Items](salesOrderItems.md)
- [Packets Dashboard](packetsDash.md)
- [Packaging](packaging.md)
