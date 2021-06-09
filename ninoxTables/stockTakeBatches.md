# Stock take batches

Stock take batches store infomation about the change to a particular [batch](batches.md) during a [stock take](stockTake.md)

They are children of [stock takes](stockTake.md)

- this is a one to many relationship
  - there are many stock take batches records to a single stock take record
- it is also a composition relationship
  - i.e. if the stock take record is deleted, all child stock take batches records will also be deleted

It also has a relationship with [batches](batches.md)

- there are many stock take records for a single batch record

Records are created via the `create stock take` button on the [homepage](home.md)

When this is done, `stock take batches` records will be created for all `batches` with `remaining size > 0`, they will then be linked to the parent `stock take` record

instructions can be found to add new `stock take batches` records to stock take records on the parent stock take record.
