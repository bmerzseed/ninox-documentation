# Stock take

The stock take table is part of the stock take functionality.

This is the top level table, meaning there is one of these records for each stock take performed.

This table has 2 children, [stock take batches](stockTakeBatches.md) and [stock take seedlots](stockTakeSeedlots.md).

- both of these are one to many relationships
  - one stock take record has many stock take batches/ stock take seedlots records
- they are also composition relationships
  - i.e. if the main stock take record is deleted, all of the children stock take batches/ stock take seedlots records will also be deleted

Records in this table can be created by the `create stock take` button on the [homepage](home.md)

- doing this will also create stock take batches and stock take seedlots records for all of the batches/ seedlots which have remaining size > 0, and link them to the newly created stock take record
- There are instructions on the stock take table on how to add a new stock take batches/ seedlots record
  - this will generally be done for seedlots/ batches which we thought had remaining size 0
  - but actually have remaining size > 0

The stock take table also serves as a way of viewing linked stock take batches/ stock take seedlots records

Once the stock take is complete, the button to complete it is on this record, it works by

- first checking a value has been entered for the new size of every linked stock take batches/ seedlots record
  - if even one record is missing a value, the user will not be able to continue
  - they will be told how many values are missing (if any)
- next, we check twice the user wants to go ahead and complete the stock take
  - we double check as completing the stock take will change the stock level of almost every batch/ seedlot in the system, so it is important it is right...
- assuming we passed the above checks, it can now be completed
- to complete we:
  - set the stock take complete state/ time
  - make adjustments to all batches which have changed
    - we loop over the stock take batches records with change != 0
    - for each, we create a batch adjustment in the [packets dashboard](packetsDash.md)
    - this changes the size of the batch and keeps a record
  - make adjustments to all seedlots which have changed
    - we loop over the stock take seedlots records with change != 0
    - for each, we change the remaining size to the new size, and create a seedlot adjustment in the [packets dashboard](packetsDash.md)
    - this changes the size of the seedlot and keeps a record

In order to delete a stock take record, users must activate admin mode, and then in the admin section at the bottom, toggle the enable deletion field, they will then be allowed to delete the stock take record
