# Sales order items

Sales order items are children of [sales orders](salesOrders.md)

- this is a composition relationship
- there are many sales order items to a single sales order

They are also linked to a [saleable product](saleableProds.md)

- there are many sales order items to a single saleable product
- this relationship is used to link to to the product the sales order item is for

Next are a series of information fields

- order item line quantity
  - number of that item on this line of the order
- line item discount
  - generally this will be 0
  - either set when adding items to the order
  - or can be set after the fact
    - there is an update trigger on this field to automatically update the line price/ line VAT if it is changed later
- line item price (exc discount)
  - this is set when the item is created
  - if a discount is later added, the value in the exc discount field is used to calculate the new inc discount amount
- line item price (inc discount)
  - generally the same as the exc discount amount
  - if a discount is set, this will be a percentage of the exc discount figure
  - this is the value used on the invoice/ invoice calculations
- line item VAT (exc discount)
  - this is set when the item is created
  - if a discount is later added, the value in the exc discount field is used to calculate the new inc discount amount
- line item VAT (inc discount)
  - generally the same as the exc discount amount
  - if a discount is set, this will be a percentage of the exc discount figure
  - this is the value used on the invoice/ invoice calculations

After these are a number of formula fields:

- unit cost
  -
