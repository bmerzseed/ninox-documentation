# Shipping Costs

Shipping costs is a table with no direct relationships to other tables.

It has 5 fields:

- Shipping Description

- Cost Inc Vat

- Cost Ex Vat

- Lower bound weight (g)

- Upper bound weight (g)

It is used when determining the shipping type/ cost for manually added [orders](salesOrders.md) (i.e. SO-xxxx orders).

There are two formula fields on the ‘add shipping’ option of ‘\*OPTIONS TO ADD TO ORDER’.

One is ‘shipping description’, and the other is the ‘shipping cost’, these are calculated based on the weight of the order and the upper/ lower bound limits of different shipping options. Upon clicking the ‘add shipping’ button of this form, a new [additional cost](additionalCosts.md) record will be created and attached to the order, it’s description / cost amount fields will be populated with the values from the ‘add shipping’ form you’ve just filled in.

If shipping has been applied (either manually or through shopify import), the shipping description will indicate this, and shipping cost on this ‘add shipping’ form will be 0, the button to add the shipping will also not work.

If you want to reapply the shipping (say after adding additional items to the order), as of 15/1/2021, there is no single function to do this, the easiest way is to select the shipping cost record (by clicking ‘order items’ on ‘show view’ and looking at the second view), and deleting it, you’ll then be able to re-add the shipping manually

When generating shipments/ picklists, any additional costs (e.g. shipping costs) that are not yet on a pick list will be assigned to that shipment. Generally this means shipping is only applied to the first shipment of an order, and later shipments (i.e. for backordered orders) will not have further shipping costs applied.
