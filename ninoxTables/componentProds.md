# Component Products

A component product is a top level table used to store information about a particular type of seed, for example BEAN; DWARF FRENCH; Marona.

The component products table has 2 main relationships

- [Saleable products](saleableProds.md)
  - Saleable products are children of a single component product
  - One component product to many saleable products
  - Saleable products have a number of subtables themselves
    - [Past Sales](pastSales.md)
    - [Batches](batches.md)
- [Seedlots](seedlots.md)
  - Seedlots are children of a single component product
  - One component product to many seedlots

It also has 2 additional relationships, though both of these are unused.

- [packets dashboard](packetsDash.md)
  - This was originally used in the seedlot creation area of the packets dashboard, though this is not used in the current version of the system
- [purchase order items](purchaseOrderItems.md)
  - Purchase orders have yet to be properly implemented, so this relationship is not critical either

In terms of the information stored within this table, there is the following

- The default shelf number for seedlots of this product
  - Note this can be overridden by manually setting a different shelf number on the individual seedlot
- The product code, name, variety, botanical name and species
  - These are all used in various places within the system, though we primarily use the product code and product name
- The units that seedlots of this product are stored in.
- The purchase quantity
  - This value is yet to be used in the new system, it relates to purchase order functionality
- Regs text
  - This is displayed on packets printed
- Plant passport species
  - Determines if we add the plant passport on packets printed or not
- Regulated seed
  - Determines if we show 'Standard seed' on bulk labels printed or not
- Mean seedlot wt/1000 seeds
  - takes the mean value of recorded seed counts
- Total remaining quantity in seedlots & stock control rem quant
  - Total remaining quantity in seedlots is the sum of the remaining size in the seedlots of this product
    - $\sum seedlots.'remaining size'
  - Stock control rem quant is equal to the total remaining quantity in seedlots, minus
    -

If admin mode is activated, users will also have some additional information available to them.
