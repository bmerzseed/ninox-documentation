# sendAllXeroInvs()

This function was created by Tom from Arctec as part of the integration that adds the invoices to Xero. This is linked to the ‘Overnight Routine to Create Xero Invoices from Ninox 11am and 9pm’ integromat scenario, and the ‘Overnight Routines’ table.

This function is triggered on creation of a record in the ‘overnight routines’ table, which is triggered by the running of the ‘Overnight Routine to Create Xero Invoices from Ninox 11am and 9pm’ integromat scenario.

The function itself works by selecting the completed ‘shipments & invoices’ records which have yet to be posted to xero. It then loops over them, calling the createXeroInv() function with each as the argument.
