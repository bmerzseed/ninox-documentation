# Stock control timed trigger

This ‘stock control timed trigger’ scenario works as part of the system which updates whether or not products are for sale on Shopify.

It is a timed trigger, currently running every 6 minutes.

The scenario itself is very simple, just creating a record in the [stock group triggers](../ninoxTables/stockGroupTriggers.md) table in Ninox.

the basic idea is that it will check a [stock group](../ninoxTables/stockGroups.md) for updates, if there are any updates, these will be sent to the [stock control updates](stockControlUpdates.md) scenario, finally the next stock group to check will be incremented on the [stock](../ninoxTables/stock.md) record in ninox.

We check in groups (currently there are 10) rather than checking all of the products for performance reasons, as checking all of the products at once would cause a timeout.

Instructions to change the frequency of checks can be found at '[how to change stock update frequency](../systemTasks/stockUpdates.md)'
