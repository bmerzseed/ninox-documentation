# Stock control timed trigger

This ‘stock control timed trigger’ scenario works as part of the system which updates whether or not products are for sale on shopify.

It is a timed trigger, currently running every 6 minutes.

The scenario itself is very simple, just creating a record in the ‘stock group triggers’ table in Ninox. More detailed behaviour caused by this creation can be seen under the ‘stock group triggers’ section in the ‘Ninox Tables’ documentation file, the basic idea is that it will check a ‘stock group’ for updates, if there are any updates, these will be sent to the ‘stock control updates’ scenario, finally the next stock group to check will be incremented. We check in groups (currently there are 10) rather than checking all of the products for performance reasons, as checking all of the products at once would cause a timeout.
