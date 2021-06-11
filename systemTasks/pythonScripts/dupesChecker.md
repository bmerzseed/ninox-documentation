# Duplicate checker

This script serves the purpose of checking tables in Ninox for duplicate codes/ numbers which should be unique. These duplicates rarely occur, but if they do it is most often due to desync between Ninox clients/ their servers.

As of June 2021, it is running on the iMac in the corner of the seed shop, it is scheduled via cron (accessed with `crontab -e`) to run once every 30 minutes

Source code for the script can be found at [github.com/bmerzseed/batch-duplicates](https://github.com/bmerzseed/batch-duplicates/)

Upon run, it first gets data from the `config.json` file, this file stores information about the tables/ fields of those tables to check, example data is as follows:

```json
[
  {
    "tableName": "Batches",
        `the table name of the data we are checking, this serves as the file name for the storage of past duplicates we have checked, and is also shown on alert emails (should there be duplicates)`
    "fieldName": "Batch Number",
        `the name of the field we are checking for duplicates on. this is used as  a key when we are extracting information from the JSON data downloaded from Ninox`
    "url": "https://share.ninox.com/j6hupob1e6nmhgp4b6z9sjedtfpwy579ihee"
        `a url shared from a view in Ninox using the 'share this view' functionality in JSON form. Contains some data we check with the 'fieldName', an id, and any other field used to filter the view`
  },
  {
    "tableName": "Seedlots",
    "fieldName": "Seedlot Code",
    "url": "https://share.ninox.com/wduyr60mq1l2lhb7wk85mz874ec0t5s0rms9"
  },
  {
    "tableName": "Orders",
    "fieldName": "Order Code",
    "url": "https://share.ninox.com/dmxy4gn9ziegcdkffopwzhcollwu0v4hsiqj"
  }
]
```
