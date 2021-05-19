# Set unset Ninox order complete states

This scenario came about after looking to optimise the 'order state' formula on [Sales orders](../ninoxTables/salesOrders.md) within Ninox.

I realised that the order state calculation was being calculated for each and every order in multiple places.

Though this calculation was fine for a single order, as the number of orders grew on the system, various areas were getting slower and slower.

The solution was to add an 'order complete' state to the sales orders, if this is true, we can set the order state to completed without doing the whole calculation, speeding things up significantly (thus improving the scalability of the system).

Generally, we set this 'order complete state' upon completing shipments. Once the shipment is completed, we check if the (calculated) order state is now completed, if so we set the state.

However, for some reason this did not work 100% of the time (potentially something to do with desync?), and auto-completed orders with just catalogues on were also not getting this state set.

So, this scenario was created.

It works by making a request to a view on the sales order table (via the 'share this view' functionality on Ninox), the view is called 'state complete no bool (do not touch)'

This request grabs some JSON data, containing an array of all of the orders that need their 'order complete' state manually setting.

If there are any items in this list, we iterate over the array, and update the 'order complete' state to `true` for each, using the given ID.

This scenario is set to execute once a day at 1am.
