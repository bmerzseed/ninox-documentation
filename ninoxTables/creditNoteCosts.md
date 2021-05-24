# Credit note costs

Credit note costs is a fairly simple table.

It only has 2 data fields (both relationships)

First is a link to a single [credit note](creditNotes.md) record

- there are many credit note costs to a single credit note cost

And also a link to an [additional costs](additionalCosts.md) record

- there are many credit note costs to a single additional costs
- in reality, the functionality is setup such that it should only ever be a 1-1 relationship

The table itself is used for crediting additional costs (primarily shipping) as part of a credit note.

It has a number of formulas visible to see how much will be added to the credit note, and also which are used when sending credit notes to Xero

The value of credit note costs will be added to the total value of the credit note/ amount to refund on the credit note.

When credit notes are sent through to Xero (via the [Create Credit Notes in Xero from Ninox 1.0](../integromatScenarios/createCNXero.md) scenario).

- Shipping costs will show up as 1 line on the credit notes
- All other additional costs will show up as a seperate line on the credit notes.
