# getNextStockTakeCode()

This function is called when creating a new [stock take](../../ninoxTables/stockTake.md) via the button on the [homepage](../../ninoxTables/home.md)

The stock take record generated will then be given a code returned from this function

The function works by getting the first record in the [numbers](../../ninoxTables/numbers.md) table

It then generates the code from the `stock take number` on that record

- "ST" + `stock take number`

And finally increments the `stock take number` on the `numbers` record
