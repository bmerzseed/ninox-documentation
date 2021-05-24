# Ninox to Xero New Invoice 2.0

This scenario was created by Tom at Arctec, as a result the documentation will be relatively limited and it is also unlikely anyone but Tom will make changes.

The scenario itself is called via webhook from 2 different places, and always via the [createXeroInv()](../ninoxGeneral/globalFunctions/createXeroInvoice.md) global function

The first place is directly from a [shipment and invoices](../ninoxTables/shipmentsAndInvoices.md) record, called by pressing the `send invoice to xero` button. This is far less common

The other (and main) way this scenario is called is via the following chain

- The [overnight routine](overnightRotuineXero.md) scenario is called
- It creates an [overnight routine](../ninoxTables/overnightRoutines.md) record in Ninox
- This triggers the [sendAllXeroInvs()](../ninoxGeneral/globalFunctions/sendAllXeroInvs.md) global function
- Which triggers the [createXeroInv()](../ninoxGeneral/globalFunctions/createXeroInvoice.md) global function for all relevant invoices...
- Which finally triggers this scenario.

The scenario itself splits into number of paths, creating invoices on Xero with various number of lines depending on the presence of tax/ additional costs/ shipping etc...

As part of this process, the `send to xero` state is toggled on the shipment and invoice record, stopping it from being sent again.
