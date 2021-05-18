# Saleable products

Saleable products stores information about products which are sold, for example small packets and bulk labels.

It has a number of relationships

- Firstly, it is a child of [Component Products](componentProds.md)
  - There are many saleable products to one component product

It also has 2 subtables/ children

- [Batches](batches.md)

  - There are many batches to one saleable product

- [Past Sales](pastSales.md)
  - There are many past sales record to a saleable product.
  - Though this is a one to many composition relationship, in reality there will only be one past sales record to a single saleable product record.

Along with a number of other relationships

- [Stock](stock.md)
- [Stock Groups](stockGroups.md)
- [Sales Orders](salesOrders.md)
- [Sales Order Items](salesOrderItems.md)
- [Packets Dashboard](packetsDash.md)
- [Packaging](packaging.md)
