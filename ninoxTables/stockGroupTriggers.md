# Stock Group Triggers

This table is part of the stock control/ updating functionality.

It serves as a way of checking if the saleable status of a product has changed at timed intervals.

This time checking works via an 'on create' trigger on this table, along with the [stock control trigger](../integromatScenarios/stockControlTrigger.md) Integromat scenario which creates records at an interval (currently every 6 minutes)

The trigger works by first getting the next [stock control group](stockGroups.md) to check and process, it gets this via the `next stock control group to process` field on the singular [Stock](stock.md) record.

We then select the [products](saleableProds.md) in this stock group which have changed, and loop over them.

For each, we send a request to the webhook on the [stock control updates](../integromatScenarios/stockControlUpdates.md) Integromat scenario. This triggers a change of the `sale policy` on Shopify, and also of the `shopifyIsForSale` field on the saleable product record on Ninox.

Finally, we increment the `next stock control group to process` field on the stock record, and delete this trigger record.
