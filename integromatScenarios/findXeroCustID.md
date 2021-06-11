# Find Xero Customer ID and Update Ninox Customer

This scenario was created by Tom from Arctec, as a result the documentation may be more limited. It is unlikely anyone but Tom will touch this scenario in the future

The scenario itself is triggered by webhook, called by the [getCustXeroID()](../ninoxGeneral/globalFunctions/getCustXeroID.md) global function

It accepts the following json data:

```json
{
  "custRec": "the id of the customer record in Ninox",
  "custName": "the name of the customer",
  "custE": "the customers email",
  "custP": "the customers phone number"
}
```

that global function is called by the [createCNXero()](../ninoxGeneral/globalFunctions/createXeroCreditNote.md) global function should a customer ID be needed

There is also a version of the global function which sends invoices to xero in progress which called this function

- as of June 2021 this was still in progress

It first tries to find the [customer](../ninoxTables/customer.md) by name in Xero

- if they exist
  - we update the customer record in Ninox with the Xero customer ID
  - execution stops
- otherwise
  - we continue

Then, we try to find the customer record by email in Xero

- if they exist
  - we update the customer record in Ninox with the Xero customer ID
  - execution stops
- otherwise
  - we continue

Finally, if both attempts to find the customer failed, we create a new customer in Xero and update the customer record in Xero with the customers ID.
