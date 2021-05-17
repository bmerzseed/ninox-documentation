# getNextBatchNumber()

This function works similarly to getNextManualOrderCode(), but instead applies to generated batches.

It works by selecting the numbers record to get the current batch number, and then returns this.

However, unlike the function to get the order code, it does not increment the numbers record.

This is as we generate the batch number to show on the batch creation forms before actually creating the batch, incrementing the number at this point would cause batch numbers to be skipped if users opened the form without creating a batch.

The numbers record will be incremented once the batch is actually created.
