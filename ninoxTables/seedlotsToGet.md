# Seedlots to get

In the current version of the system, this table is not often used.

Initially, it was used for generation of the list of [seedlots](seedlots.md) to get from the cold store to fill all currently unassembled packets.

Following the introduction of the ‘print bulk labels’ / ‘print bulk packets’ buttons (which also print a list of seedlots to get), the table/ button is rarely used. Full seedlot lists can still be printed in this way via the ‘print list of all queued packets and labels’ button on the [packing dashboard](packingDash.md).

The table has a single record with a relationship to all [seedlots](seedlots.md) (one seedlots to get record to many seedlots records).

On the print view of the table, there is a filter to show only seedlots with ‘est to use’ > 0, i.e. packets currently waiting to be made up.

When the button on the [packing dashboard](packingDash.md) is pressed, the ‘seedlots to get’ record is trick updated, ensuring the data is as up to date as possible, a print url is then generated via the ‘printAndSaveRecord()’ function.

Finally, the list is sent to the [a4 printing](../integromatScenarios/a4Printing) integromat scenario, passing into the ‘sales/ninox/drop print folders/a4’ folder on dropbox, and being printed via batch print pdf in the packing room.
