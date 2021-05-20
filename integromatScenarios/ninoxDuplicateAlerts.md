# Ninox Duplicate Alerts

This is a very simple scenario used for the e-mail sending aspect of duplicate alerts.

The scenario itself accepts a collection of data, for example:

```json
{
    "data": 15239,                      `the batch number/ seedlot code/ order number`
    "count": 3,                         `number of duplicates of this data`
    "tableName": "Batches",             `which Ninox table the duplicate was found in`
    "fieldName": "Batch number"         `the field of the table the duplicate was found in
}
```

This data is used to send an e-mail to seed shop alerting of the duplicate.

Duplicates are found, and the data is sent to this webhook via the [duplicate checker](../systemTasks/pythonScripts/dupesChecker.md) Python script.
