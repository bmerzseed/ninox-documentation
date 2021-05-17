# Multiple Batch Printing

Multiple batch printing is used to print multiple batches at once. We opted to use a scenario to loop over and make the individual requests as making multiple requests within Ninox is blocking, but if we instead do this via Integromat, the requests can run in the ‘background’ after the initial request is made.

Multiple batch printing is triggered via webhook. The request is made from the ‘print small packets’/‘print bulk labels’ buttons on the ‘assembly dashboard’ table within Ninox.

It accepts an array of objects, with the objects containing information about the type of thing to print (bulk or sm), the url to download the design from, the batch number and the size of the batch.

The scenario works by accepting the data by webhook, and iterating over the array. For each item in the array, the JSON data is parsed into a format integromat can work with, and a request is then made to the batch printing/ barcoding scenario.

At each stage, if there is an error then an email will be sent to alert ‘seedshop@seedcooperative.org.uk' of the failure. Though this scenario has yet to fail.
