# Stock groups

This table is part of the stock control/ updating functionality.

Stock group records are all linked to the main [stock](stock.md) parent record, and also have a number of [saleable products](saleableProds.md) as children.

When designing that functionality there was a number of issues, and this was one of the solutions to those issues.

Initially, we were attempting to check every single [saleable product](saleableProds.md) at each check. Although this would have used less operations & allowed us to check all products more frequently, the check would time out every time (however we tried).

So, rather than check all products at once, we split the products into a number of 'stock groups', allowing us to check less products at once and avoid time outs.

Currently, there are a total of 10 stock groups, and checks are done once every 6 minutes, this is more than enough for current levels of demand (May 2021), this results in all products being checked once an hour

As demand rises, there is potential to increase the frequency of the checks

- Either by increasing the frequency of the checks (to as frequent as once a minute)
  - note this will greatly increase the number of integromat operations used
- Or by reducing the number of stock groups
  - Given each is taking 3-4 seconds at the moment (and integromat times out at 40 seconds), having as little as 2 stock groups may be feasible.
  - Though note, the system & these checks may be slower in busy periods

The functionality itself works as follows

- a [stock control trigger](stockGroupTriggers.md) record is created via the [stock control triggers](../integromatScenarios/stockControlTrigger.md) integromat scenario
- This causes the `on create` trigger to run.
- The on create trigger gets the next stock group to check
- if any of the products within this stock group have changed their saleable state, we call the [stock control updates](../integromatScenarios/stockControlUpdates.md) scenario
- the stock group is incremented

There are instructions on the [stock control trigger](stockGroupTriggers.md) record in Ninox on how to update the stock groups should you want to.
