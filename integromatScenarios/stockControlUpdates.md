# Stock control updates

The stock control updates scenario is used to update whether or not a product is for sale on Shopify based on the ninoxCanSell state on the saleable product.

It is called via webhook, with the request body including:

```json
{
  "ninoxID": "the id of the saleable product record on Ninox",
  "shopifyProdID": "the Shopify product id, stored on the saleable product on Ninox",
  "shopifyVarID": "the Shopify variant id, stored on the saleable product on Ninox",
  "shopifyNewPolicy": "whether or not we are updating Shopify to continue selling the product, or deny (stop) selling the product",
  "shopifyNewState": "whether the new ‘shopifyIsForSale’ state on the saleable product in Ninox should be true or false",
  "prodCode": "the product code of the saleable product in Ninox"
}
```

It is called when ‘saleStateChanged’ is true for a product, this will either be via the ‘stock control timed trigger’ integromat scenario creating a trigger & checking a stock group, or when an order item is added to an order (as we check for saleStateChanged then).

Once the data is recieved, the scenario does 2 things

- It sets the ‘shopifyIsForSale’ state on Ninox to ‘shopifyNewState’, making ninoxCanSell and shopifyIsForSale equal, and therefore saleStateChanged false.
- It also sets the for sale policy on Shopify, allowing the product to continue selling/ deny from selling.

In order to stop/ allow selling on Shopify, the stock of all products is less than or equal to zero, the policy referred to above is whether or not we continue or deny selling the product if the stock is less than or equal to zero.

We planned on passing stock levels directly to Shopify at one point, but this would have been far more complicated, and would also have used far more Integromat operations
