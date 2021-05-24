# createXeroInvoice(si: ‘Shipments & Invoices’)

This function was created by Tom from Arctec as part of the integration that adds the invoices to Xero. This is linked to the [Overnight Routine to Create Xero Invoices from Ninox 11am and 9pm](../../integromatScenarios/overnightRoutineXero.md) integromat scenario, and the [Overnight Routines](../../ninoxTables/overnightRoutines.md) table.

The function itself is called from the [sendAllXeroInvs()](sendAllXeroInvs.md) global function

It works by taking in a [Shipment & Invoices](../../ninoxTables/shipmentsAndInvoices.md) record as an argument, and using this record to calculate a series of values which are needed for the Xero invoice.

Once the values are calculated, a post request is made via the http function (inside a do as server block), the body of this request contains the variables calculated in the initial stage of the function.
