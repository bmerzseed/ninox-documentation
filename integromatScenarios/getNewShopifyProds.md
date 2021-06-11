# Get New Shopify Products and add Variants to Ninox

This scenario was created by Tom from Arctec, as a result the documentation may be more limited. It is unlikely anyone but Tom will touch this scenario in the future

The scenario itself is triggered by webhook from the `Get Product Variants from Shopify` button in the [component products](../ninoxTables/componentProds.md) table in Ninox

This sends a post request with the following information

```json
{
  "prod": "the component products Ninox ID",
  "shopifyID": "the component products Shopify ID"
}
```

The scenario then uses this information to find the product in Shopify.

We then iterate over the variants of this product we looked up, creating a [saleable product](../ninoxTables/saleableProds.md) record for each in Ninox, and then linking this to the main component product record
