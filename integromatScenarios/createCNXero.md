# Create Credit notes in Xero from Ninox 1.0

This scenario was created by Tom from Arcte, it is used to push credit notes on Ninox to the Xero accounting system.

It is triggered via the `post credit note to Xero` button on a [credit note](../ninoxTables/creditNotes.md) record within Ninox, this button calls the [createXeroCreditNote()](../ninoxGeneral/globalFunctions/createXeroCreditNote.md), which calls the scenario via webhook.

The scenario itself grabs some details about the customer and the credit note.

Depending on the data it has gathered, it will go down a specific path of the router, creating different lines on the credit note in Xero

After creating the credit note in Xero, it will set the `sent to Xero` state in Ninox to `true`, regardless of which path it went down.

Note, this scenario is unlikely to be touched by anyone but Tom...
