# Integromat Scenarios

This section covers the different scenarios used in Integromat. For each, there is a summary of its purpose, an explanation of how it works, and how it interacts with the rest of the system (Ninox, other scenarios, Python scripts, Xero, Shopify etc.)

As is the case with other areas of the system, part of the integration was setup by Tom from Arctec, this particularly relates to the Xero integrations, and the Shopify orders to Ninox integration. There will be a brief overview of these scenarios regardless.

There are some additional scenarios that can be found on Integromat that are not covered here. These will primarily be test/ obselete scenarios that are not of concern, though there may also be some more recent scenarios which have not been documentated, likely created by Tom.

The scenarios we use are primarily triggered via web hooks, which work by sending a HTTP POST request from some source (usually Ninox, but sometimes via a Python script or another Integromat scenario) to the web hook url, this request has a JSON body containing information which will be used by the scenario.

Some of the scenarios are also timed. Timed scenarios are especially useful when wanting to trigger some Ninox code to execute periodically, we do this by creating ‘trigger tables’ within Ninox which we add ‘on record create’ triggers to, we can then execute the code in this trigger at any timed interval we desire by creating a new record in this table.

Some common Integromat errors we recieve can be found [here](../systemTasks/integromatErrors.md).

Below is a list of links to pages for each scenario.

- [A4 Printing]
- [Batch print dropbox err handling]
- [Batch printing/ barcode]
- [Clear dropbox printing folders]
- [Multiple batch printing]
- [Ninox reprinting]
- [Seedlot barcoding]
- [Stock control timed trigger]
- [Stock control updates]
- [Ninox Duplicate Alerts]
- [Overnight routine to create Xero invoices from Ninox 11am and 9pm]
- [Send emails via Ninox]
- [Set unset Ninox order complete states]
- [Get new shopify products and add variants to Ninox]
- [Get Shopify product ID and add to component product in Ninox]
- [Missing Shopify orders sent to Ninox]
- [TEST - Updated product in Shopify]
- [Create credit notes in Xero from Ninox 1.0]
- [Find Xero Customer ID and add to component product in Ninox]
- [Ninox to Xero New Invoice 2.0]
-
