# Seedlot Count Form

The seedlot count form is a simple form with only 3 fields.

When users are filling small packets, via the [assembly dashboard](assemblyDash.md), they will sometimes be asked to add a seed count for a [seedlot](seedlots.md), this seed count is used to calculate expected usages.

When pressing the ‘click here to add seedcount’ button, it will create a record of the ‘seedlot count form’, which is auto linked to the [seedlot](seedlots.md) record with a one to many relationship.

The user then enters the weight of 1000 seeds in grams, and presses the confirm button, this will then update the 1000 seed count weight on the seedlot record, close the seedlot count form, and allow the user to continue with the packet assembly.
