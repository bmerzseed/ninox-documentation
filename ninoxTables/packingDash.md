# Packing Dashboard

The packing dashboard (accessed from [home](home.md) through the ‘print and fill packets’ button in the ‘new packets and adjustment section’ serves as navigation for getting to individual [assembly dashboard](assemblyDash.md) records, and also has the buttons used to print the next lot of [batches](batches.md).

At the top, there are also 4 buttons (new packets, change packets, change seedlot, empty packets). These can be used to easy create new batches (new packets), adjust a batch (change packets), disassembled packets from a batch (empty packets), or to adjust a seedlot size (change seedlot), clicking any of these buttons will open a ‘packets dashboard’ record with the corresponding batch/ seedlot action.

Below these buttons are 2 more buttons - `print bulk labels` and `print small packets`, and two formula fields below them - `batches of bulk labels to print` and `batches of small packets to print`.

Both formula fields show the number of [print queue items](printQueueItems.md) waiting to be printed, i.e. the number of bulk label batches/ small packet batches waiting to be printed.

If the value of the respective formula field is greater than 0, pressing the print buttons will print the next lot of [batches](batches.md) and a list of [seedlots](seedlots.md) which need to be collected for these batches.

Batches will be printed sequentially, and once the stop condition has been met, no later batches will be printed even if they would not go over the allowed numbers.

A maximum of 15 seedlots of bulk label batches will be printed (this could be more than 15 batches if there are multiple batches made up from the same seedlot), and a maximum of 700 packets worse of small packets will be printed.

- For example, if 8 batches of small packets had been printed, each of size 80 (total 640 packets), and the next batch was also of size 80, this would be over the allowed printing amount of 700 packets, and so no more batches will be printed after this, even if there are later batches of size less than or equal to 60, they will be ignored until the button is next pressed.

The batches which will be printed are gathered from [print queue items](printQueueItems.md), specifically we take the oldest unprinted print queue items of the specified type (bk/sm)

When the buttons run, they will generate a [print queue seedlot list](printQueueSeedlotList.md) record, all of the print queue items will be attached to this, and it will also be used to generate the list of seedlots to collect.

Assembly records are accessed via the `small packet assemblies` and `bulk label assemblies` views, by clicking on an individual record in these views.
