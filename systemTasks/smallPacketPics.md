# Converting and adding small packet images to Ninox

First, drag \*.pages file(s) onto the ‘pages to pdf’ automator file in the ‘packets pdfs’ folder, this will dump the outputted pdfs into the ‘packets pdfs’ folder

now, with your pdfs, drag the pdf(s) onto the ‘pdf to image’ automator file in the ‘packets jpg (no crop) folder, this will dump the outputted jpegs into the ‘packets jpg (no crop) folder.

next, packet jpgs need to be cropped, visit [anycrop.com](https://anycrop.com)

We have original jpgs at 600dpi, & we want to take off 10mm from the top and bottom, and 5mm from the left and right.

This works out at 236 pixels off each of the top & bottom, and 118 pixels off of each of the left and right sides.

On anycrop.com, cropped area should therefore be

- x = 2364
  - 2600 - 2 \* 118
- y = 4728
  - 5200 - 2 \* 236

Make sure the ‘image format’ is set to jpg, and the ‘image quality’ is set to 100%

Finally, upload the image to the field on the corresponding [component product](../ninoxTables/componentProds.md) record in Ninox

This process could likely be automated far more e.g. by

- automating the whole file conversion/ cropping process to a single operation
- automating the upload of the files to Ninox
  - via the api, either with Integromat or more manual interaction

Though ultimately, the pictures are uploaded so infrequently (after the initial migraton) this just is not worth while.
