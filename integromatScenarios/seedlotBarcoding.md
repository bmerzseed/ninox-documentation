# Seedlot barcoding

The Seedlot barcoding scenario exists to generate & attach a barcode to a seedlot record within Ninox.

The scenario is triggered by webhook, via a ‘generate barcode’ button on seedlot records. It accepts a seedlot code (used to lookup the seedlot record, & for failure email messages), and also the record ID, used as the data when generating the barcode.

It works by accepting the data, looking up the record, generating the barcode from the ID & then resizing it. Next the resized barcode is uploaded to the seedlot record as an attachment, the barcode image field is then set to this barcode attachment.

As is the case with many of the other scenarios, if there is a failure at any point, an email will be sent to ‘seedshop@seedcooperative.org.uk' to alert of the failure
