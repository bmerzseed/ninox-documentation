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

Once the scenario has accepted the data, it starts by downloading the file from the url, this file contains a PDF of the packet design generated from Ninox.

It then generates and resizes a barcode based on the batch number data. This barcode is then uploaded to Dropbox, into /Sales/Ninox/Drop Print Folders/barcodes

Next, it sleeps for a second to try and avoid Dropbox timeouts

Now, there is a router which goes in one direction for bulk labels (type = bk), and another for small packets (type = sm). The only difference between the two paths is the folder which Dropbox will upload the downloaded packet design to

- /Sales/Ninox/Drop Print Folders/smIn for small packets
- /Sales/Ninox/Drop Print Folders/bkIn for bulk labels

We then sleep for a second once again, and rename the uploaded file to `{Batch Num}-{Batch Size}.pdf`, e.g. to '15123-50.pdf' using the example data.

If at any point during the above stages of executions a Dropbox upload fails, the [batch print err handling](batchPrintErrHandling.md) scenario will be called. If calling this scenario fails, an email will be sent directly to the Seed Shop email alerting you of this.

Additionally, if other (non Dropbox upload) steps of the scenario fail, Emails will also be sent to Seed Shop, though this is far less likely.
