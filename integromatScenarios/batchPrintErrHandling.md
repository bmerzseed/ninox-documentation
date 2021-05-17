# Batch print dropbox err handling

This scenario was created to handle errors from the ‘batch printing/ barcoding’ scenario.

Initially, we were only occasionally having batches fail to print (usually 1x a week) due to dropbox 429 runtime errors (too many writes), which occur when multiple sources are trying to write to dropbox simultaneously. We could quickly reprint these batches within Ninox and it was only a small issue.

After one weekend, these errors started occurring much more frequently (close to 1/3 batches).

One solution was to add sleep timers throughout the batch printing scenarios, causing less writes to dropbox, but while this helped it did not completely solve the problem, so something was needed to handle the errors still occuring.

The scenario works via a webhook, this webhook is called from the ‘batch printing/ barcode’ scenario should a dropbox upload fail. The webhook takes the following data:

```json
{
  "url": "the url used to download the batch pdf",
  "data": "the batch number",
  "size": "the size of the batch, and number of packets/ labels to be printed",
  "type": "whether the batch is of bulks (bk) or small packets (sm)",
  "errString": "the error string from ninox, contained in the error email in this scenario if it fails too many times"
}
```

Once the data has been accepted, we check for the existence of the batch number in a data store, depending on if it already exists, we either create it in the data store, or get its value from the data store.

We use the data stores to keep state between cycles of the scenario, allowing us to retry printing a given number of times (in this case the scenario is setup to retry 5x)

If the batch number does not exist in the datastore, we create it with the batch number as the key, and numExecs = 2 (numExecs represents the number of retries). We then sleep for 5 seconds, and resend a request to the ‘batch printing/ barcoding’ scenario webhook with the url, data, size and type fields, causing that scenario to retry.

If the batch number is in the datastore, we use a router to check if numExecs is greater than 4.

- If it is, we have already tried to print this batch 5 times, and we send a failure email.
- If not, we increment the datastore by 1, sleep for 5 seconds, and retry the ‘batch printing/ barcode scenario by sending it a webhook request.
