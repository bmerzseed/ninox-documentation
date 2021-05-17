# getSalesCount(formMonth: number, prods: ‘Saleable Products’)

This function takes a month (1-12 as a number), and a saleable products record as arguments. It then returns the number of that product sold the previous time that month occured.

examples

- if it is currently April 2021, and April is called, data from April 2020 would be shown
- if it is currently April 2021, and March is called, data from March 2021 would be shown
- if it is currently April 2021, and May is called, data from May 2020 would be shown.

As this Ninox system only started being used halfway through December 2020, we cannot solely use calculated sales data.

When accessing 2020 data from January to November, we use the data which is stored in number fields in the ‘past sales’ record of each product, which is a subtable of products.

2020 data for December is slightly more complicated, as half the sales figures were imported from the old system, and half are calculated based on data from the new system.

Because of this, the function works by adding the historic figures to an outVal formula (if it is necessary to), and then adding the calculated figure on top of this (whether the calculated figure is greater than 0 or not)

We calculate sales figures by summing the line quantity of ‘order items’ made on the year/ month specified.

We finally return outVal.
