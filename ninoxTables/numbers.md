# The numbers table contains a single record & 3 different number fields:

- Manual Order Number

- Purchase Order Number

- Batch Number

The ‘Manual Order Number’ field applies to manually added [sales orders](salesOrders.md) (i.e. SO-xxxx orders), an order is given this number upon being manually created once it’s no longer defined as a new order (i.e. it has at least 1 order item), the number in this table is then incremented.

Purchase Order number - not at it’s final function

The ‘Batch Number’ field applies to [batches](batches.md) created/ printed through the [packets dashboard](packetsDash.md) table. When the ‘batch action’ field on the ‘packets dashboard’ table is updated (i.e. through pressing a button to create new packets), the next batch number will provisionally be placed in the batch number field of the ‘packets dashboard’ table, once the button is pressed to complete the batch creation, the batch number will be recalculated by taking it from the numbers table, & the ‘batch number’ field in the ‘numbers’ table will be incremented.
