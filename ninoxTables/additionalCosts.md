# Additiona Costs

The additional costs table is used to store information about additional costs added to an order, these will very often be shipping, but can also be other costs (for example donations).

Costs will be auto imported from Shopify on Shopify orders, for manually added orders, there are ‘add shipping’ / ‘add additional costs’ options on the orders. Depending which one is used, the ‘shipping’ boolean field will either be set to true or false.

Additionally, when adding shipping through the ‘add shipping’ option, the vat rate on the additional cost record will automatically be set to 20%, for costs added under the ‘add additional costs’ section, the vat rate can be picked (0 or 20%)

When creating the new cost through these buttons we also store a cost description (either the shipping option, or a user entered description for manually added costs)

Lastly is a cost ex vat figure, for shipping this will be auto filled, & for additional cost this is entered by the user.

From this ex vat figure & the previously mentioned vat rate, we can calculate both the cost with vat and the at rate to be used on the invoice.
