# Updated Shopify Product to Ninox 2.0

This scenario was created by Tom from Arctec, as a result the documentation may be more limited. It is unlikely anyone but Tom will touch this scenario in the future

This scenario is triggered via a webhook connected to Shopify. It activates when a product has been updated.

When this happens, we lookup the [component product](../ninoxTables/componentProds.md) in Ninox

- if it does not exist
  - David recieves an email alerting him to create it
  - execution pauses
- if it does exist
  - we proceed

We then iterate over the product variants, trying to find each in the [saleable products](../ninoxTables/saleableProds.md) in Ninox

- if we find it
  - we update it with its most recent information
- if we do not find it
  - we create it
