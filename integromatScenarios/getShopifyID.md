# Get Shopify Product ID and Add to Component Product

This scenario was created by Tom from Arctec, as a result the documentation may be more limited. It is unlikely anyone but Tom will touch this scenario in the future

The scenario itself is called via webhook from the `Find Shopify Product ID` button on the [component products](../ninoxTables/componentProds.md) table in Ninox

The webhook recieves data in the form

```json
{
  "prod": "the component products id",
  "shopifyPrNm": "the product name of the requested item",
  "shopifyVend": "the product code of the requested item"
}
```

The scenario itself works by finding the product in Shopify using these details, and grabbing its long Shopify ID

It then updates the component product record in Ninox, adding the ID
