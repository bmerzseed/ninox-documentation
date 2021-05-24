# Stock

The stock table is used as part of the stock control functionality.

It is the main parent record of the other areas of control control, with [saleable products](saleableProds.md), [stock control triggers](stockGroupTriggers.md), and [stock groups](stockGroups.md) all being children.

The table itself has less moving parts than the others.

It primarily serves as a link between them, as a storage for the next stock group to check, as a view of sale states, and as a way of manually updating all groups via button press (`update stock` button).
