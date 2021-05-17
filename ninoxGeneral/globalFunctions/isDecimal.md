# isDecimal(num: number)

As far as I could find in the Ninox documentation, there was no direct way to check if a number was a decimal.

We need to check for decimals in the case of quantities (e.g. order item line quantities), to ensure half packets are not being added to orders.

This function works by checking if the rounded number is equal to the number.

It would likely also work using the modulus operator, i.e. num%1 = 1
