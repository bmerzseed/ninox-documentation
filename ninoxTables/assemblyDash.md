<!-- # Assembly Dashboard

The Assembly Dashboard will primarily be accessed via the [packing dashboard](packingDash.md), and is used when users of the system are filling small/ bulk packets.

Assembly dashboard has a single relationship - 1 [batch](batches.md) can have many assembly dashboard records. In reality, this is a 1 to 1 relationship, as every (new) batch should have an assembly dashboard record, but should never have more than 1 record. Upon the creation of a batch via the [packets dashboard](packetsDash.md), we generate and link this assembly dashboard record to the batch record.

The basic idea of the dashboard is to give users an overview of what they’re making, how much they’re making, and what they need to make it. It also serves as a way of recording how much seed they actually end up using, whether or not they managed to make up the whole batch, and whether or not they finished off the seedlot. If the data entered seems erroneous, there are also checks in place to warn them of this.

At the top of the dashboard is a navigation bar, telling the user they’re on the assembly dashboard and also providing buttons to close the record/ navigate to home.

Next are 4 fields, showing the user the product they are making, how many packets they are making, the batch number, and the seedlot to use. These cannot be edited & are just for information.

Following that is the main area of the dashboard, providing information about how much seed to weigh out to start with, the units of the seed, and what packet size should be used for the product they are creating.
Along with being a source of information, this is also where users can enter data about the assembly.

seedlot weight/ count (before) and (after) are used by entering the amount of seed the user weighed out before making the packets in (before), and then entering the remaining amount of seed after making the packets in (after), from this we can calculate the total amount of seed that they used.

The amount of seed that they should weigh out before making the packets is suggested by ‘approximate weight to start with’, which is equal to 1.4 times the expected amount of seed that they are going to use.

In the case of bulk labels, the values for weight/ count before and after will be autofilled when the batch is created via the packets dashboard.

Also, if you are in admin mode at this step, there will be additional usage information visible to you:

- an actual estimated figure, rather than the estimated \* 1.4 figure
- the actual used figure (start weight/ count - end weight/ count)

### lots more here abt how the buttons work etc -->

# Assembly Dashboard

The assembly dashboard serves as a place for users to 'assemble' [batches](batches.md), recording the amount of seed they used, and whether they were able to make the entire batch. Depending on the data they give, the batch size and the size of the [seedlot](seedlots.md) used to create the batch will be adjusted

Along with being an interface for users to perform assemblies through, it also serves as a storage of the information they entered while assembling a batch.

Records of the assembly dashboard have a relationship with the batches table

- there can be many assembly dashboard records to a single batches record
- in reality, there should only ever be a single record
  - batches imported from the old system will have no records
  - if a batch somehow has 2 records, a warning will be displayed when completing the assembly telling the user to alert an admin
  - if a batch has no records, it will not be shown on the [packing dashboard](packingDash.md) and will therefore likely be missed by users
    - if it is caught that it's missing, there will be a button to create the missing assembly dashboard record on the batches record

Users will primarily access assembly dashboard records via the [packing dashboard](packingDash.md), where there are views showing the small packets/ bulk labels to assemble, with links to their assembly dash records

The first section of the assembly dash serves as a navigation section/ display of general information

- firstly, there are buttons to close the record, and to return to the homepage.
- saleable product
  - formula field showing the product name that is being assembled
- number of packets to make
  - equal to the start size of the batch
  - this is the number of packets/ labels that should have printed
- batch number
  - formula field showing the batch number of the linked batch
- seedlot
  - formula field showing the seedlot to take seed from when assembling this batch
  - this is also the seedlot the adjustments will be applied to

The next section is the main data input area when users are completing assemblies. The exact fields seen here will depend on the type of batch being assembled (`sm` or `bk`, and `seeds` or `grams`)
