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
    - a more detailed explanation of how can be found on the [Stock Groups](stockGroups.md) documentation page
- [Sales Orders](salesOrders.md)
  - There are many sales order records for a single saleable product record
  - This relationship is not used directly, but instead serves as a way of adding new items to orders.
  - It can be found under the 'Add order lines' on '\*OPTIONS TO ADD TO ORDER'
- [Sales Order Items](salesOrderItems.md)
  - There are many sales order items to a single saleable product record.
  - Sales order items are made for a particular product
  - Quantities from this relationship are used in many dfferent places
- [Packets Dashboard](packetsDash.md)
  - There are many packets dashboard records for a single saleable product record.
  - This relationship is used when selecting the product to make up batches for on the packets dashboard
- [Packaging](packaging.md)
  - There are many saleable product records to a single packaging record.
  - This relationship is used to store information about which type of packaging should be made when making up a batch of a particular saleable product.

The table also stores a variety of information within it, and has a collection of formulas which serve various purposes & which are used in many places throughout the system.

- Product name and product code
- Product type
  - whether the product is a bulk label or small packet
  - this property is used/ checked a lot throughout packet creation/ assembly functionality
- Estimated seed usage
  - the amount of seed used for this product when creating batches, measured in terms of the units stored on the component products.
  - used for expected usage where a more accurate value (e.g. using seedcounts) is not available
- Product weight
  - used when calculating order weights
  - includes the weight of the packet as well as the weight of the seed
- Product vat rate
  - whether vat is 0% or 20%
  - 20% for flowers, 0% for everything else
- Packet units
  - Whether the size of batches of this product are measured in terms of number of seeds or weight.
- Packet size
  - The amount of the above specified packet units in batches of this particular saleable product
- needToAllocate
  - whether or not items need to be manually allocated to batches during the picking process
  - at this time, only catalogues and gift cards are not considered 'needToAllocate'
  - items which do not need to be allocated should be auto added to a batch when picklists are generated
- Prices
  - Retail inc/exc vat
    - used when manually adding order items if wholesale prices is false
  - Wholesale inc/ exc vat
    - used when manually adding order items if wholesale prices is true
    - i.e. the customer is a retailer

## quantity formulas likely to change

- Shopify product ID/ variant ID
  - internal product ID's stored within Shopify
- Create batch
  - shortcut to creating a batch of this product, opens the product dashboard with some prefilled information
