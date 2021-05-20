# Past Sales

Past sales is a fairly simple table, it is a child of [saleable products](saleableProds.md), meaning there are many `past sales` records to a single `saleable products` record, however, in reality this is a 1 to 1 relationship.

It is used to display sales figures when creating new [batches](batches.md) via the [packets dashboard](packetsDash.md), this gives users an indication of how many packets they should make.

It contains a product code field, this is not used within functionality, and only exists from when legacy data was being imported from Unleashed.

For each month of the year, we have 2 fields in each record

- a number field storing 2020 data
- a formula field calculating total sales of the previous occurance of that month
  - if it is currently May 2021, the May data shown will be for May 2020
  - if it is currently May 2021, the April data shown will be for April 2021

The formula fields work by passing the current month number(1 - 12), and the `saleable product` record into the [getSalesCount()](../ninoxGeneral/globalFunctions/getSalesCount.md) global function.

- e.g. `getSalesCount(4, 'saleable product')` for April

The formula considers the 2020 data imported from unleashed too.

Once it is 2022, the global function can be modified to ignore 2020 data, and the 2020 data number fields can be removed.
