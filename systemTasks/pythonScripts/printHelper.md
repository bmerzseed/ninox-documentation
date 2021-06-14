# Printing script

This script is used as part of the system process which prints small packets and bulk labels. It executes on startup of the iMac in the packing shed via a shell script called from login items. It then runs, checking all of the folders every 30 seconds.

The source code can be found at

When batches are requested to print, the [batch printing](../../integromatScenarios/batchPrintingBarcode.md) scenario will ultimately be called, this scenario uploads packet designs/ barcodes to folders inside `/seed co-op dropbox/sales/ninox/drop print folders`. The folders used are set within the `config.json` file

- small packets go into the `smIn` folder
- bull labels go into the `bkIn` folder
- barcodes go into the `barcode` folder

The script will ignore any files which do not have precisely the expected filenames, examples are:

- random files
- duplicate files with a `-1` if the integromat scenario fails

These files will also be cleaned at the end of each day via the [dropbox cleaning](../../integromatScenarios/clearDropboxFolders.md) integromat scenario

It is at the point that both the packet pdf and the barcode image are in their corresponding dropbox folders that this script will act. We match them up by filename. I.e...

- the barcode will be in the format `batchNum`.png
- the packet design will be in the format `batchNum`-`batchSize`.pdf

If we find a match, the script will do the following:

- add the barcode image onto the pdf
  - the exact position of the barcode is configured via `config.json`
- move the pdf with barcode into the `smToDupe`/ `bkToDupe` folder
- next, it uses the batch size in the file name, and creates a pdf with this number of pages of the design
- this is then moved into `smToPrint`/ `bkToPrint`
- at this point,
  - if it is a small packet
    - it is printed by `batch print pdf` on the office iMac
  - if it is a bulk label
    - it is printed by `drop print` on the seed shop iMac
