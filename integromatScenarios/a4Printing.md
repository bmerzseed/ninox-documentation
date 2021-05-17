# A4 Printing

This scenario is used to print invoices and lists of seedlots to make up batches.
It works via a webhook. We send data from Ninox to the webhook with a POST request, this data consists of:

```json
{
  "url": "the url to download the file from",
  "data": "the invoice code/ seedlot list code, used in the error emails"
}
```

Once the data is received, we download the file from that url, and upload it to the /sales/ninox/drop print folders/a4 folder in dropbox, where it is printed by ‘batch print output pdf’ from the iMac.

Additionally, it has error handling for each of the 3 operations which will send error alert emails should anything go wrong.

Usually, if there is an error from this scenario it will be a 429 runtime error from the dropbox upload, this often means something else was trying to write to dropbox simultaneously. As of late, this has only been happening once every few weeks, if it does happen the best thing is to reprint the invoice from Ninox.
