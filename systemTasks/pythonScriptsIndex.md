# Python Scripts

There are a couple of areas of the system where we use some Python scripts in order to perform tasks that were not ideal to do just through Ninox and Integromat due to speed/ excessive use of integromat operations

Along with these 2 scripts which are always working, there have been a number of scripts used throughout the system to do a number of things, including:

- Manipulating data
  - Customer data for catalogues
  - Data to be imported to Ninox during the initial migration
  - Cleaning exported unleashed data when the account was closed
  - Cleaning old backorderd data from Unleashed
- Deleting old small packet PDF's which were saved on Ninox
- An older version of the stock control system
- Previous printing solutions
- And others...

The 2 scripts that run regularly today are:

- [Printing helper](pythonScripts/printHelper.md)
- [dupesChecker](pythonScripts/dupesChecker.md)
