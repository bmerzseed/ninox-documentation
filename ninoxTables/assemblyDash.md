<!-- # Assembly Dashboard

The Assembly Dashboard will primarily be accessed via the [packing dashboard](packingDash.md), and is used when users of the system are filling small/ bulk packets.

Assembly dashboard has a single relationship - 1 [batch](batches.md) can have many assembly dashboard records. In reality, this is a 1 to 1 relationship, as every (new)  [batch](batches.md) should have an assembly dashboard record, but should never have more than 1 record. Upon the creation of a  [batch](batches.md) via the [[packets dashboard](packetsDash.md)](packetsDash.md), we generate and link this assembly dashboard record to the  [batch](batches.md) record.

The basic idea of the dashboard is to give users an overview of what they’re making, how much they’re making, and what they need to make it. It also serves as a way of recording how much seed they actually end up using, whether or not they managed to make up the whole  [batch](batches.md), and whether or not they finished off the seedlot. If the data entered seems erroneous, there are also checks in place to warn them of this.

At the top of the dashboard is a navigation bar, telling the user they’re on the assembly dashboard and also providing buttons to close the record/ navigate to home.

Next are 4 fields, showing the user the product they are making, how many packets they are making, the  [batch](batches.md) number, and the seedlot to use. These cannot be edited & are just for information.

Following that is the main area of the dashboard, providing information about how much seed to weigh out to start with, the units of the seed, and what packet size should be used for the product they are creating.
Along with being a source of information, this is also where users can enter data about the assembly.

seedlot weight/ count (before) and (after) are used by entering the amount of seed the user weighed out before making the packets in (before), and then entering the remaining amount of seed after making the packets in (after), from this we can calculate the total amount of seed that they used.

The amount of seed that they should weigh out before making the packets is suggested by ‘approximate weight to start with’, which is equal to 1.4 times the expected amount of seed that they are going to use.

In the case of bulk labels, the values for weight/ count before and after will be autofilled when the  [batch](batches.md) is created via the [packets dashboard](packetsDash.md).

Also, if you are in admin mode at this step, there will be additional usage information visible to you:

- an actual estimated figure, rather than the estimated \* 1.4 figure
- the actual used figure (start weight/ count - end weight/ count)

### lots more here abt how the buttons work etc -->

# Assembly Dashboard

The assembly dashboard serves as a place for users to `assemble` [batches](batches.md), recording the amount of seed they used, and whether they were able to make the entire [batch](batches.md). Depending on the data they give, the [batch](batches.md) size and the size of the [seedlot](seedlots.md) used to create the [batch](batches.md) will be adjusted

Along with being an interface for users to perform assemblies through, it also serves as a storage of the information they entered while assembling a [batch](batches.md).

Records of the assembly dashboard have a relationship with the [batches](batches.md) table

- there can be many assembly dashboard records to a single [batches](batches.md) record
- in reality, there should only ever be a single record
  - [batches](batches.md) imported from the old system will have no records
  - if a [batch](batches.md) somehow has 2 records, a warning will be displayed when completing the assembly telling the user to alert an admin
  - if a [batch](batches.md) has no records, it will not be shown on the [packing dashboard](packingDash.md) and will therefore likely be missed by users
    - if it is caught that it's missing, there will be a button to create the missing assembly dashboard record on the [batches](batches.md) record

Users will primarily access assembly dashboard records via the [packing dashboard](packingDash.md), where there are views showing the small packets/ bulk labels to assemble, with links to their assembly dash records

Additionally, given the complicated nature of this table, its relative age, and the lack of changes made to it since the switch to the Ninox system, this table could likely do with some work, potential ideas are:

- tidying button logic
- more standardisation between different units/ packet sizes
- general tidying up
- switching from many `on update` triggers to formula fields
  - this would make the tables logic easier to understand at a glance
  - and also easier to change
  - initially we used `on update` triggers on data fields rather than formula fields to try and preserve the state of the assembly upon completion as much as possible into the future
    - in reality, much of the information could still be preserved using formula fields

The first section of the assembly dash serves as a navigation section/ display of general information

- firstly, there are buttons to close the record, and to return to the homepage.
- saleable product
  - formula field showing the product name that is being assembled
- number of packets to make
  - equal to the start size of the [batch](batches.md)
  - this is the number of packets/ labels that should have printed
- [batch](batches.md) number
- formula field showing the [batch](batches.md) number of the linked [batch](batches.md)
- seedlot
  - formula field showing the seedlot to take seed from when assembling this [batch](batches.md)
  - this is also the seedlot the adjustments will be applied to

The next section is the main data input area when users are completing assemblies. The exact fields seen here will depend on the type of [batch](batches.md) being assembled (`sm` or `bk`, and `seeds` or `grams`)

- Seedlot weight count (before/ after)
  - these are used by users to enter the seed they weighed before filling the packets, and the remaining amount of this seed once they finished filling the packets
    - the difference will be used in adjustment calculations and shown in fields on this table if the user has admin mode activated
  - these fields will be autofilled for bulk labels
- approximate weight to start with
  - this gives users an idea of how much to weigh out for their starting weight figure
  - it is equal to `1.4 times` the expected usage amount
  - this formula field contains a semi-complicated rounding formula, showing a varying number of decimal places depending on the size of the figure
    - i.e. more decimal places for a smaller value
  - the expected usage figure it uses in its calculations will ne
    - equal to the packet size `if`
      - `stored as` = `seeds`
      - `product type` = `bk`
      - `seedcount exempt` = `true`
- units
  - formula field which shows the units this product is stored in
  - takes the value directly from the component product
  - `seeds` or `grams`
- actual seedlot adjustment amount
  - only shown if `isAdminMode()` = `true`
  - displays the difference between the `seedlot weight/ count (before)` and `seedlot weight/ count (after)`
  - `after` - `before`
  - number field which is updated via `on update` triggers on the `before`/ `after` fields
- est seedlot weight adjustment
  - only shown if `isAdminMode()` = `true`
- `WERE YOU ABLE TO MAKE UP ALL PACKETS?` / `HOW MANY WERE YOU ABLE TO MAKE UP?` / `Batch size adjustment amount`
  - all 3 of these fields interact with eachother, providing users the ability to make all/ only part of the given [batch](batches.md)
    - these links work via on update triggers on each of the fields, clearing/ calculating values depending on options selected and values entered
  - were you able to make up all packets?
    - boolean field
    - if `yes`
      - all packets have been assembled
      - the [batches](batches.md) starting `remaining size` will be equal to the [batches](batches.md) `start size`
      - no adjustment will be created once the assembly is complete, and so the [batch](batches.md) will be the full size
    - if `no`
      - not all packets could be assembled
      - the [batches](batches.md) starting `remaining size` will be less than the [batches](batches.md) `start size`
        - it could potentially be as low as zero
      - an adjustment will be created once the assembly is complete, this will adjust the [batch](batches.md)
      - `how many were you able to make up` will show, allowing the user to input the number they were actually able to make
  - how many were you able to make up?
    - if not all packets could be made, this field needs a value
    - an adjustment will be created on completion to adjust the [batch](batches.md) to this size
    - changing this value updates `batch size adjustment amount`
  - [batch](batches.md) size adjustment amount
  - this is the size of the adjustment created on the [batch](batches.md) once the assembly is completed
  - as [batch](batches.md) remaining size works via a formula, the existence of this adjustment will change the size
- 200 seeds wt
  - this will only show if the [batch](batches.md) requires a seedcount, and the seed count has been completed
  - it calculates the weight of 200 seeds based on the 1000 seed weight
  - it can be used to quickly calibrate the scales with their largest supported sample size
- spoons used
  - a simple text field
  - users should enter the spoon they used in this box, doing this will display the spoon used for future small packet assemblies using this seedlot
- finished seedlot
  - a boolean field
  - having this option activated will cause the sisze of the seedlot the [batch](batches.md) was made from to be adjusted to zero upon completion of the assembly
  - there is an option when creating the packet (via the [packets dashboard](packetsDash.md) to leave a comment on the assembly record, giving the user a suggestion to set this option to `true`
- override warnings/ checks
  - boolean field
  - turning this to `yes` will cause the warnings/ errors displayed if the usage figures are too high/ low when completing an assembly to be ignored
- completed by
  - filled with the currently logged in user upon completion of the assembly
- percentage deviation
  - difference between expected usage and actual usage
  - filled upon completion of the assembly
- comments
  - displays comments filled during the [batch](batches.md) creation
  - also allows users to add additional comments

Once the user has filled in the required information, flipping the `completable` formula to true, they will be able to see the `complete assembly` button, this button is quite complex & does a number of things...

- First, it checks there is exactly one `batch creation` [packets dashboard](packetsDash.md) record linked to the [batch](batches.md) we are assembling
  - if there is more of less than 1 it will tell the user to alert an admin
  - this alert has not shown as of the time of writing this
- Next, we check if we should show warnings/ errors
  - if `override warnings/ checks` has been set, we can ignore this completely, as warnings and errors are ignored
  - otherwise, we calculate a boolean value for whether or not there are the below, this is based on the actual usage, the expected usage, and the error/ warning thresholds
    - upper error
    - lower error
    - upper warning
    - lower warning
  - if there is an error, the user will be unable to complete the assembly without overriding or correcting the values
  - if there is a warning, the user will be shown a dialog box, telling them the usage is somewhat out, but allowing them to complete the assembly still if they are happy
  - the error/ warning thresholds can be adjusted around lines 25-30 of this formula
- assuming the user has passed the error/ warning checks, execution can continue
- next, we check `seedlotFinished`
  - if it is `true`
    - we check the `seedlotFinishedWarning` state
    - this is `true` if the adjustment to empty the seedlot will be greater than the size of the largest bulk packet of the component product
    - if it is `true`, we display a warning to the user, they can choose to complete the assembly or stop to go and check out the large adjustment size
  - else
    - we continue execution
- finally, we are ready to complete the assembly
  - this runs via the `performAssembly()` function
    - this sets values on the [packets dashboard](packetsDash.md) [batch](batches.md) creation record
    - if the user said they were not able to make up all packets, we also create an additional [packets dashboard](packetsDash.md) record to adjust the size of the [batch](batches.md)
    - we then set the [batch](batches.md) to assembled, allowing it to be used in allocations
    - we then trick all of the other records to update in the assembly dashboard table
      - this is done due to the heavy use of on update triggers, it allows them to retain the correct values
    - finally, we set the `completed by` and `percentage deviation` fields
  - if `seedlotFinished` is `true`,
    - we also call the `processSeedlotFinished()` function
    - this adjusts the size of the seedlot to zero
    - and also creates a `seedlot adjustment` [packets dashboard](packetsDash.md) record to make a note of this
- finally, we reopen the [packing dashboard](packingDash.md)

There are also a number of fields which are shown at the bottom of the view, but only if `isAdminMode()` is equal to `true`

- `isValidAssembly`
  - This checks data has been inputted
  - for seed based bulks
    - requires able to make all is true `or` (false `and` number able to make has been entered)
  - for everything else
    - requires able to make all is true `or` (false `and` number able to make has been entered)
    - also requires before/ after figures have been entered
  - used as part of the `completable` formula
- `completable`
  - `true if`
    - batch is not assembled
    - `isValidAssembly` = `true`
    - the seed count is okay
      - either it is not needed
      - or it has been completed
      - or override warnings/ checks is on
- the relationship link to the parent [batch](batches.md)
- upper bound numeric adjustment
  - used to calculate the `usable size` of a [seedlot](seedlots.md) by subtracting this figure if the batch is unassembled
