# Overnight Routines

This table was created by Tom from Arctec, it serves the purpose of automatically sending invoices to Xero.

It is triggered by the [Overnight Routine to Create Xero Invoices from Ninox 11am and 9pm](../integromatScenarios/overnightRoutineXero.md) Integromat scenario creating a record in this table, with the `on create` trigger then firing.

The content of the create trigger itself is very simple.

It sets the `date/ time` field to `now()`, and calls the [sendAllXeroInvs()](../ninoxGeneral/globalFunctions/sendAllXeroInvs.md) global function.
