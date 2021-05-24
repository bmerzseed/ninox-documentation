# Shopify Orders to Ninox

This scenario was created by Tom from Arctec. It is relatively complicated & unlikely to be touched by anyone but Tom, so this description will be fairly simple.

At the time of writing this, the `Shopify Orders Sent to Ninox 2.0` is being used, Tom has however been working on 3.0/ 3.1 versions of this scenario, so these may be used in the future.

The scenario runs at a timed 15 minute interval, and its purpose is to bring any new orders from Shopify into the Ninox system.

The scenario itself is essentially a series of routers, with the same core functionality living at the end of all of them.

Firstly, the scenario is split depending on if a customer needs to be made or not.

Then, the scenario is split again depending on if we need to create a [billing address/ delivery address](../ninoxTables/addresses.md).

- 1 path for existing billing/ delivery addresses
- 1 path for existing billing and new delivery
- 1 path for new billing and existing delivery
- 1 path for new billing/ delivery addresses

At the end of all these paths is the same core content

- Create the [order](../ninoxTables/salesOrders.md)
- Create the [payment](../ninoxTables/payments.md) record
- Add [additional costs](../ninoxTables/additionalCosts.md)
  - namely shipping
- Add all of the [line items](../ninoxTables/salesOrderItems.md)
