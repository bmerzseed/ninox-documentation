# Grower

The growers table is used to store information about who grew a particular seedlot

It has a relationship with [suppliers](supplier.md)

- only supplier to many growers
- composition relationship

and also a relationship with [seedlots](seedlots.md)

- one grower to many seedlots

There are additional relationships with areas of the purchase order functionality, as this is not functional, these will not be elaborated on.

As the purchase order functionality is not complete, right now it serves as a simple data store about the grower of a particular seedlot.
