# Packets Dashboard

The packets dashboard is used for creating new [batches](batches.md), adjusting the size of batches, disassembling packets from batches, and adjusting the remaining size of a [seedlot](seedlots.md). There also exists ‘seedlot creation’, but this is currently obsolete & will be moved to the purchase order section.

Along with being used as a form in order to perform the actions, the underlying table data of the packets dashboard is used to save information about any actions made, allowing users to look back in future & see when and why these actions were performed, and the exact changes made. These can either be viewed directly using the table, or through the ‘operations log’ view found on both batches and seedlots.

The action done by a particular record of the packets dashboard is determined by the ‘seedlot action’, and the ‘batch action’. These 2 choice fields are used to display/ hide fields for each type of action (using ‘display if’, e.g. ‘batch action’ = 1)

For example…

- Batch creation is ‘batch action’ -> 1: ‘new packets’, and ‘seedlot action’ -> 2: ‘Adjustment’

  - This is as we are creating a new batch record, and also adjusting the size of an existing seedlot

- Batch adjustment is ‘batch action’ -> 2: ‘changes to number of packets’

  - As we are just adjusting the size of an existing batch

- Batch disassembly is ‘batch action’ -> 3: ‘empty packets to seedlots’, and also ‘seedlot action’ -> 2: ‘adjustment’

  - As we are adjusting the size of the batch and also changing the size of the seedlot

- seedlot adjustment is ‘seedlot action’ -> 2: ‘adjustment’

  - as we are just changing the size of the seedlot and making no changes to the batch

- Zero seedlot and make packets is ‘batch action’ -> 4: ‘create packets and zero seedlot’ and ‘seedlot action’ -> 3: ‘zero seedlot and create packets’

  - As we are setting a seedlot to zero, and creating packets.
    These are their own seedlot / batch actions (rather than using creation/ adjustment) in order to allow the creation of a new form for this process, without adding an additional state/ other workarounds

- There is also ‘seedlot action’ -> 1: ‘creation’.
  - This is a remnant from an earlier version of the system, and has never been used.
    It has been left as an option ready for when purchase orders were looked at.

When performing either a ‘batch creation’ or ‘batch disassembly’, the ‘seedlot adjustment’ fields will not be shown until the action is completed, this is as ‘seedlot action’ is only set upon the confirm button being pressed. This means they do not clutter up the form when performing the action, but are available to view for reference afterwards.

## Batch Creation

When creating a batch, there are a number of fields.

PRODUCT TYPE -> this select box is used as a filter when selecting the product you would like to create a batch for, i.e. if ‘small packet’ is selected, only small packets will be shown. It has its state preserved from the last batch creation you made, making it easier to bulk create batches of a certain type.

Batch number -> This is automatically calculated for you on creation of the record (specifically on update of the batch action field). It cannot be manually modified in this form. Once the button to create the batch is pressed, this number will be recalculated incase someone else is creating batches simultaneously, in order to prevent duplicates.

Batch creation date -> This is auto set to today on creation of the record, it can be manually changed. Whatever the value in this field is will be set as the batch creation date once the button is pressed

\*PACKETS TO MAKE UP - priority list -> this is a relationship field linking to saleable products (N packet dashboards to 1 saleable product), it is only used to select a saleable product, and the relationship itself is not important. A product can be selected by clicking on the field. Additionally, once a product is selected here, if the the saleable products component product is different to the currently selected seedlot, the seedlot field will be cleared.

Net stock of product (before creation) -> this is a formula field, it displays whatever the net stock is of the selected saleable product before the batch is created

Estimated usage per packet -> this is a formula field, it displays the estimated seed usage based on the selected product.
If the product is stored as seeds, this figure will be a number of seeds based on the packet size.
If the product is stored as grams,
if it is a bulk label it will be a number of grams based on the packet size,
if it is a small packet, it will either be a number of grams calculated using the selected seedlots seedcount (if it has one), if not, it will just use the estimated seed usage value of the saleable product.

## Batch Adjustments / Disassemblies

The fields used to enter information when performing a ‘batch disassembly’ or a ‘batch adjustment’ are shared, apart from the button. The difference between these two is that batch disassembly will also change the ‘seedlot action’ to 2, and will make an adjustment to the seedlot, other than that they function identically.

## Seedlot Adjustments

### unfinished

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

# Batch adjustment/ disassembly

# Seedlot adjustment

# Seedlot zeroing & batch creation

# Seedlot creation
