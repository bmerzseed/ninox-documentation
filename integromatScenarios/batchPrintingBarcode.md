# Batch Printing/ Barcoding

This scenario is responsible for the printing of small packets and bulk labels.

It accepts data via webhook. This data will generally come from 3 places.

- Via the [multiple batch printing](multipleBatchPrinting.md) Integromat scenario, triggered when a user presses the print all buttons on the [packing dashboard](../ninoxTables/packingDash.md) within Ninox
- Directly from Ninox via the reprint batch buttons on a [batch](../ninoxTables/batches.md) record
- After a previous failure of this scenario triggers the [batch print err handling](batchPrintErrHandling.md) scenario

Example data is as follows:

```json
{
    "type": "sm",                                       `whether small packet (sm) or bulk (bk)`
    "url": "https://dbde0027.ninox.com/data",           `file download url`
    "data": 15123,                                      `batch number`
    "size": 50                                          `batch size`
}
```
