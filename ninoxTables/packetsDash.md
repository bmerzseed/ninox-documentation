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

## Batch creation

Batch creation accessed via the `new packets` button on other parts of the packets dashboard, and also on the packing dash, or through the `set-up new packest and labels` button on the homepage.

It consists of

- batch action 1 (creation)
- seedlot action 2 (adjustment)

As to make a [batch](batchces.md), we also need to adjust the quantity remaining in a [Seedlot](seedlots.md). When inputing information to create the new batch, seedlot action is not set (in order to hide seedlot adj fields), once the batch has been created, the seedlot action is set and these fields become visible.

The process itself requires choosing the packet type (`sm` or `bk`), when a new batch creation is created, this option will automatically be set to its last value

- This means users can easily make many bulks/ small packets consecutively without having to manually set this value every time.

The next step of the batch creation process is to select the [saleable product](saleableProds.md) which you would like to make up.

- The previously selected `product type` will be used as a constraint in this selection to only show small packets or bulk labels depending on the selection.
- Additionally, once the saleable product is selected, a table of displaying past sales for this product will be displayed.
  - This uses data from the [past sales](pastSales.md) table

Once a [saleable product](saleableProds.md) is selected, the next step is for the user to select the [seedlot](seedlots.md) which will be used to make the selected product.

- The previously selected saleable product will be used as a constraint here in order to only show relevant seedlots of the relevant [component product](componentProds.md).
- Once a [seedlot](seedlots.md) is selected, a button to `use up seedlot` will appear, pressing this will auto fill the comments section, and set the number of packets to make to the expected maximum possible from the selected [seedlot](seedlots.md).

Next, the user inputs the number of packets to create (defaults at 1).

- there is an on update trigger on this field in order to make sure that the number to make is
  - not zero
  - a whole number
  - not greater than the max able to make from the selected seedlot.
- if any of these conditions are broken, the entered value will be cleared.

Before completing the creation, the user can add any comments, these will show when users are assembling the packets.

Finally, the user can create the [batch](batches.md)

Throughout this section, there are a number of additional formula fields which display ore information about the product being created, and expected usage figures. These formulae appear to the right of any input fields.

## Batch adjustment/ disassembly

Batch adjustment and disassembly works by a very similar mechanism, with some of the fields being shared between the two.

When we are changing the size of a batch, we do not directly change the remaining size (as this is a formula field). Instead, the remaining size takes into account any completed adjustments.

Batch adjustment is

- batch action 2
- accessed via
  - `change packets` button on other areas of the packets dash and packing dash
  - `changes to number of packets` button on the home page

Batch disassembly is

- batch action 3
- seedlot action 2
  - as we are also adjusting the seedlot when making a batch disasembly.
- accessed via
  - `empty packets back to seedlots` button on home
  - `empty packets` button on other areas of the packets dashboard and the packing dashboard.

We use the difference in batch action to differentiate between the two, allowing us to show slightly varied fields/ treat data slightly differently/ different complete buttons.

Both follow the same steps when completing the process.

First, select the batch.

- this has a lengthy on update trigger which is used to update the adjustment/ disassembly information fields shown to the right of the input fields.
  - these fields are primarily used with disassemblies.
  - the update trigger calculates these values using data from the assembly dashboard when the batch was assembled.

Next, the user can input the number of packets they would like to adjust the batch by/ disassemble.

- there is an update trigger on this field which will update some of the information fields as above.
- the update trigger will also clear the value entered if
  - it will adjust the batch to be greater than the start size
  - it will adjust the batch to be less than 0
  - it is a decimal

Before completing the adjustment/ disassembly the user can add a comment.

Finally, the user can complete the adjustment/ disassembly.

There are 2 different buttons depending on whether it is a batch/ disassembly.

- if it is an adjustment
  - we clear the information fields
  - set information in other areas of this record
    - likely unnecessary now...
  - set this record to `locked`
  - then finally create a new adjustment record and open it
- if it is a disassembly
  - we do as above,
  - but we also adjust the size of the seedlot
  - set the seedlot action to 2
  - add seedlot adjustment information to this record for future reference
- a lot of the logic (particularly which sets values on other areas of the packets dash) could likely be removed with no consequence
- It exists as...
  - this is one of the oldest parts of the system
  - when switching between operations in the past, we just changed the batch/ seedlot action of the current record, and cleaned up any fields when operations were completed.
  - now, we create a new record if we want to switch operation, meaning we do not have to worry about information in other areas.

## Seedlot adjustment

Seedlot adjustments involve a change to the remaining size of a seedlot.

Unlike batch adjustments, the remaining size of a seedlot is not a formula calculated based on its child adjustments, it is instead a numerical field whos value is changed when the adjustment is completed. The seedlot adjustment packets dash record then just serves as a record of this.

Seedlot adjustments have `seedlot action` of 2

They are also part of batch creation/ batch disassembly.

They are created via the `changes to seedlots` button the [homepage](home.md) and the `change seedlot` button on the [packets dash](packetsDash.md) / [packing dash](packingDash.md)

The form itself works in the following way

- first the user selects whether they want to adjust the seedlot by an amount, or to a certain amount
  - depending on this selection, the `*amount to adjust seedlot by` / `*amount to adjust seedlot to` fields will be writable/ unwritable, and a box showing the user where to input information will appear
- next, the user selects the seedlot, this will automatically fill the `amount remaining in seedlot` field to display to the user how much is left, and also to serve as a record of how much was left when the adjustment is completed
- next, the user should enter data in either `*amount to adjust seedlot by` or `*amount to adjust seedlot to` depending on the `*adjustment type` they selected
- the user can then (optionally) add a comment

Once all of the data has been input validly, the user wil be able to complete the adjustment

The completion button will

- Check the adjustment is valid
- Check the adjustment is not too large
  - if it is larger than the size of the largest bulk of this product, the user will have to confirm they would definitely like to complete the adjustment
- assuming it is fine to go ahead we continue
- then we lock the record so no future changes can be made
- we change the size of the seedlots `remaining size`
- we create a new `seedlot adjustment` and open this record

## Seedlot zeroing & batch creation

Seedlot zeroing and batch creation serves as a way of finishing off a seedlot, whilst making a given number of small packets.

Though this could be done via a seedlot adjustment/ batch creation, this was created to allow users to complete the task in a single, simple action.

Actions of this type have

- batch action 4
- seedlot action 3

They are created via the `Tiny batches to empty seedlot` button on other records of the [packets dash](packetsDash.md) and [packing dash](packingDash.md)

Creating one of these actions on the packets dash via the buttons will autofill the comments with a message

Using the form just requires the user to select a seedlot, and give a number of packets they would like to create from the seedlot

Once this is done, they can complete via the `zero seedlots and create packets` button, this will do the following

- Calculate the batch number and check it is valid & things have not desyncd
- Create a new batch, filling in the relevant fields
- create a new assembly dash record for the batch, autofilling comments and the `finished seedlot` field
- create the print queue record
  - this allows users to print the batches packets when they are ready via the buttons on the packing dash
- lock this record and switch to a new one

## Seedlot creation

This was originally created as a way of adding new seedlots to the system

It has never been used, as seedlots are intended to be added via some purchase order functionality, which is not yet implemented

Instead, seedlots are manually added by interacting with the table directly.

This action uses seedlot action 1

It is likely very little of this code will be used when the purchase order functionality is finally implemented
