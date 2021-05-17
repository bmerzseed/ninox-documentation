# Customer

The customers table is used to store information about a given customer.

It is linked to orders via a one to many relationship (1 customer to many orders), and also to contacts by a one to many composition relationship (1 customer to many contacts).

Primarily we only use this contacts relationship for customers classified as ‘businesses’ (via the ‘BUSINESS ?’ Boolean field). Non business customers instead have a few contacts fields to use on the customer record itself (phone/ mobile/ email)

Customers also have a customer type, this is always (1/ gardener) for non businesses. For businesses it can also be (2/ commercial, 3/ retailer or 4/ seed company). This customer type is use to determine whether or not a customer is eligible for ‘wholesale prices’ on small packets. If the customer type is 3/ retailer, they will be, and when adding order items to an order, these prices will automatically be used.

The customers record also has a ‘show view’ field, this is used to show information about the four different categories (contact details, billing addresses, delivery addresses, orders), working via ‘display ifs’ on the corresponding fields.

First, we have ‘contact details’. This shows either the 3 contact fields or the contacts relationship table depending on whether the customer is classified as a business or not.

Next, delivery addresses and billing addresses. These both work identically (but are obviously different tables).

Due to the format of the data when we were doing the initial migration to Ninox, addresses are not directly linked to customers. Instead, addresses are linked to the Order records (1 address to many orders), in this view, we then display all of the addresses where their linked order was made by the current customer.

The selection of addresses works in a similar way, meaning a single address will only ever be linked to orders made by a single customer (unless admin mode is used to remove in place constraints)
Lastly in show view, we show the orders linked to this customer.

Below show view, we have shopify customer ids/ shopify customer emails. These are automatically added for customers created via the shopify integration.
