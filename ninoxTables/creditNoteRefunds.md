# Credit note refunds

The credit note refunds table is part of the credit note functionality, records of this table are a child of [credit notes](creditNotes.md) (1 credit note to many credit note refunds).

The table itself is very simple, and works similarly to the way [payments](payments.md) relate to [orders](salesOrders.md)

The table stores information about how the refund was completed e.g.

- Shopify
- Cheque
- Bank Transfer
- Stripe
- Cash

and the refund amount.

Refunds for a particular credit note can be added/ viewed via the `refunds` option on `show view`

Refunds are used in formula fields on the credit note - e.g.

- amount refunded
- amount to refund
