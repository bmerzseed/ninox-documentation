# Missing Shopify Orders Sent to Ninox

This scenario was created by Tom from Arctec, as a result the documentation may be more limited. It is unlikely anyone but Tom will touch this scenario in the future

This scenario was created to push through missing orders in February time, this was a 1 off usage and it has not been used since. It could possibly be deleted along with its sister [missing orders](../ninoxTables/missingShopifyOrders.md) table in Ninox, but as they're not causing any problems, they have not yet been deleted...

The scenario is triggered by pressing the `Get from Shopify` button on orders in this [missing orders](../ninoxTables/missingShopifyOrders.md) table within Ninox.

This sends a webhook request with the `order number` to the scenario.

The scenario then works in a very similar way to the main [scenario which sends orders from Shopify to Ninox](shopifyOrdersToNinox.md), sharing much of its functionality.

The difference being, rather than `watching` the orders, it just searches for the order requested, and sends that to Ninox
