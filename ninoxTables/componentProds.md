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

It also has 2 additional relationships, though both of these are currently unused.

- [Packets Dashboard](packetsDash.md)
  - This was originally used in the seedlot creation area of the packets dashboard, though this is not used in the current version of the system
- [Purchase Order Items](purchaseOrderItems.md)
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
  - Stock control rem quant is equal to the total remaining quantity in seedlots, minus the expected usage of any batches waiting to be made up

Below these fields is 'show view', which is a choice box with four possible options, depending on which one is selected, we show/ hide different fields/ views.

- Saleable Products
  - Shows a view of saleable products linked to this component product record
- Seedlots
  - Shows a view of seedlots linked to this component product record
- Purchase order items
  - Shows a view of purchase order items linked to this component product record
  - Note purchase order functionality is not implemented and so this is current unused
- Images
  - Displays the small packet image and the variety image
    - The small packet image is used to generate designs for packets.
      - We use an image here rather than design the packet fully on the print view due to limitations of the print view.
      - For example, text cannot be upside down, font options are limited etc.
      - In the small amount of testing I've done, it seems possible to use the Ninox html() function to use html/ css to format the packets, though centering text inside the html() function seems to be a problem (without doing maths with margins)
      - Changing the design to use the Ninox print view would however drastically reduce the file size of small packets, and potentially speed up printing slightly
    - An image of the variety
      - None of these have been added & this is therefore not currently used.

If admin mode is activated, users will also have some additional information/ options available to them.

- Exemption from seedcount
  - If this is set, users do not have to perform seedcounts when making small packets of this product
  - This is used for some seed packets filled on the seed counting machine, and also seed where the small packets are measured in terms of grams rather than seeds (e.g. bee mixture)
- Get Product Variants from Shopify
  - Creates saleable product records in Ninox for all of the variants for this component product in shopify.
  - Works via the [Get new Shopify porducts and add variants to Ninox](../integromatScenarios/getNewShopifyProds.md) Integromat scenario
- Find Shopify Product ID
  - Populates the 'Shopify Product ID' field on this component product record
  - Works via the [Get Shopify product ID and add to component product in Ninox](../integromatScenarios/getShopifyID.md) Integromat scenario
- Shopify Product ID
  - The internal ID for this component product on Shopify
- Returned info from Shopify Search
  - ???
- Display record buttons
  - Hides the record create/ duplicate/ print/ delete buttons if the user is not in admin mode
  - Works via the [displayRecordButtons](../ninoxGeneral/globalFunctions/displayRecordButtons.md) global function
