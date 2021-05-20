# Print Queue Items

This table is used as part of the print queue functionality.

When a batch is created via the packets dashboard, we create a record in this table & link it to the batch. These records then serve as a list of batches which are yet to be printed.

Once the print buttons on the [packing dashboard](packingDash.md) are pressed, these records are populated with printing information, printed is set to true, and they are linked to a [print queue/ seedlot list](printQueueSeedlotList.md) record.

A request is also sent to the [multipleBatchPrinting](../integromatScenarios/multipleBatchPrinting.md) Integromat scenario with information collected from these records.
