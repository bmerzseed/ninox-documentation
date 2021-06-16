# Stock Updates

There are 2 ways to change stock update frequency...

By changing the scenario run frequency on integromat

- this can be done by navigating to the [stock control timed trigger](../integromatScenarios/stockControlTrigger.md) scenario
- and then changing its schedule setting
- each time it runs, it will update 1 stock group

By changing the number of stock groups

- The number of stock groups can be changed by creating/ deleting stock groups records until you have the desired amount.
- Then go to the 'stock groups' view of the saleable products table and go to 'update multiple records'. Set the calculated value for stock group to:

- ```
  let thisID := number(id)
  let numStockGroups := cnt(select 'stock groups')
  first(select 'stock groups'[groupNum = thisID % numStockGroups + 1])
  ```
- This will automatically split the saleable product records (fairly evenly) between the specified number of stock groups

The total time to update all stock groups is equal to `number of stock groups` \* `time interval of [stock control timed trigger](../integromatScenarios/stockControlTrigger.md)`
