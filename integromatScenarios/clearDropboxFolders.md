# Clear Dropbox printing folders

When we have a 429 error on the ‘batch printing/ barcoding’ scenario (whether handled by the error handling scenario or not), it will often manage to upload some of the files to dropbox, but fail on later ones.

Because of this, we were ending up with many files building up in the folders within ‘/sales/ninox/drop print folders’ on dropbox. Though this doesn’t break anything, it was annoying especially if you were trying to figure out why something hadn’t printed.

This scenario solves the problem by clearing out files from the ‘bkIn’/‘smIn’/‘barcodes’ folders once a day at 1:30 am.

It works by iterating over the files in each of the folders, and deleting any files found.
