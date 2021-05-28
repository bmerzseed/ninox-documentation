# createXeroCreditNote(c: 'credit notes')

This function was created by Tom from Arctec as part of the functionality which sends credit notes to Xero.

It is called via the `send CN to Xero` button on a [credit note](../../ninoxTables/creditNotes.md) record in Ninox, the credit note record is passed into it as an argument.

It works by grabbing & calculating information from the credit note, it then sends this information to Integromat.

Specifically, it sents the information to the [createCNXero](../../integromatScenarios/createCNXero.md) scenario
