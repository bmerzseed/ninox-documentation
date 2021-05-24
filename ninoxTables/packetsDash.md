# Packets Dashboard

The packets dashboard is one of the most complicated tables in the system, it is used for performing and recording a number of different operations on [Batches](batches.md) and [Seedlots](seedlots.md). This was one of the first parts of the system to be created.

In hindsight, things likely would have been cleaner if each operation lied within its own table, but migrating all of the logic and data to do this would be time consuming with little to no functional benefit.

Records in this table are created and accessed via buttons under the `new packets and adjustments` section on [home](home.md), buttons on the [packing dashboard](packingDash.md), and buttons on other packets dashboard records.

The table works by displaying/ hiding fields based the value of 2 choice fields

- `batch action` for creation/ adjustment/ disassembly of batches
- `seedlot action` for the adjustment (and previously creation) of seedlots

Additionally, the `locked` field is used throughout to restrict data entry/ modification once an operation has been completed (via the `writable if` option).

Operations performed through this table can be seen via the `operations log` option of the `show view` choice on batch/ seedlot records.

Below, the way in which each of the possible operations work is explained.

# Batch creation

Batch creation accessed via the `new packets` button on other parts of the packets dashboard, and also on the packing dash, or through the `set-up new packest and labels` button on the homepage.

It consists of

- batch action 1 (creation)
- seedlot action 2 (adjustment)

As to make a batch, we also need to adjust the quantity remaining in a Seedlot. When inputing information to create the new batch, seedlot action is not set (in order to hide seedlot adj fields), once the batch has been created, the seedlot action is set and these fields become visible.

The process itself requires choosing the packet type (`sm` or `bk`), when a new batch creation is created, this option will automatically be set to its last value

- This means users can easily make many bulks/ small packets consecutively without having to manually set this value every time.

The next step of the batch creation process is to select the saleable product which you would like to make up.

- The previously selected `product type` will be used as a constraint in this selection to only show small packets or bulk labels depending on the selection.
- Additionally, once the saleable product is selected, a table of displaying past sales for this product will be displayed.
  - This uses data from the [past sales](pastSales.md) table

Once a saleable product is selected, the next step is for the user to select the seedlot which will be used to make the selected product.

- The previously selected saleable product will be used as a constraint here in order to only show relevant seedlots of the relevant component product.
- Once a seedlot is selected, a button to `use up seedlot` will appear, pressing this will auto fill the comments section, and set the number of packets to make to the expected maximum possible from the selected seedlot.

Next, the user inputs the number of packets to create (defaults at 1).

- there is an on update trigger on this field in order to make sure that the number to make is
  - not zero
  - a whole number
  - not greater than the max able to make from the selected seedlot.
- if any of these conditions are broken, the entered value will be cleared.

Before completing the creation, the user can add any comments, these will show when users are assembling the packets.

Finally, the user can create the batch

Throughout this section, there are a number of additional formula fields which display ore information about the product being created, and expected usage figures. These formulae appear to the right of any input fields.

# Batch adjustment/ disassembly

# Seedlot adjustment

# Seedlot zeroing & batch creation

# Seedlot creation
