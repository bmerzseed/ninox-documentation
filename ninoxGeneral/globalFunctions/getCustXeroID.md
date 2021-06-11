# getCustXeroID(c : Customer)

This function works as part of the integration which sends invoices and credit notes from Ninox to Xero

As of June 2021

- it is only called by the [createXeroCreditNote](../ninoxGeneral/globalFunctions/createXeroCreditNote.md) global function
- there is also another global function in development which changes the way invoices are sent from Ninox to Xero
  - this also calls the `getCustXeroID()` function

It works by generating JSON data from the customer record in Ninox

This data is in the form:

```json
{
  "custRec": "the id of the customer record in Ninox",
  "custName": "the name of the customer",
  "custE": "the customers email",
  "custP": "the customers phone number"
}
```

It then sends the data via webhook to the [findXeroCustID()](../../integromatScenarios/findXeroCustID.md) Integromat scenario
