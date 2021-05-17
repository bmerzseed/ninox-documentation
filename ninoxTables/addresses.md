# Billing/ Delivery Addresses

The billing and delivery address tables are functionally almost identical.

The main difference is that the delivery address table has a button ‘billing address same as delivery address’, this will create a billing address record and duplicate the information entered in the fields of the delivery address record across to it.

Addresses are linked to [orders](salesOrders.md) (one address can have many orders). When creating a new order within Ninox, the user has a choice of using existing addresses, or creating new addresses (by pressing the ‘+’ icon on the address fields’

When an order is imported from Shopify (via the [Shopify Orders to Ninox](../integromatScenarios/shopifyOrdersToNinox.md) scenario), Integromat will first check if a corresponding billing/ shipping addresses already exists, if so, it will link these to the order, if not, new address records will be created with the provided information and will be linked to the order.

Addresses can also be viewed from a [customer](customer.md) record, though there is no direct link from the customer to either address table, it will show any addresses linked to orders which are linked to that customer.

Both the delivery address and the shipment address are displayed on invoices. This is set up such that first, we check if there is an ‘\* ADDRESS NAME’, if so, we display this as the name on the invoice. If not, we check if there exists either a ‘\* FIRST NAME’ or ‘\* LAST NAME’, if yes, we concatenate these two fields & use this value. Should all of these fields be empty, we display ‘NO NAME ENTERED’ on the invoice, alerting whoever is picking/ dispatching that these fields are missing and must be entered.
