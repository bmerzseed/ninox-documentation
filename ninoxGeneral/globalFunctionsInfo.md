# Global Functions

Global functions can be accessed on Ninox via the main options area of the database (i.e. by clicking the database name in the popout sidebar), then clicking options, and finally global functions

They work similarly to normal functions (i.e. are defined in the same way)

```
function fnName(arg1: type, arg2: type, …) do
    let val := 1
    val
end;
```

Values are returned by writing the value to be returned on its own (i.e. above val would be returned -> 1 would be returned)

In order to take a record as an argument, the type should be the table name in single quotations
i.e. fn(order: ‘Sales Orders’) would take a sales order record as an argument, which would be accessible using 'order' within the code block

One slight quirk I have not figured out with global functions involves ‘do as server’
There were no problems using ‘do as server’ when making http requests within a global function, but otherwise, wherever I placed it execution seemed to be getting missed, for this reason do as server is only used for http requests within global functions within this database.

A list of global functions used within the database can be found below

- [getAllowance(productType: text)](globalFunctions/getAllowance.md)
- [getNextManualOrderCode()](globalFunctions/getNextManualOrderCode.md)
- [getNextBatchNumber()](globalFunctions/getNextBatchNumber.md)
- [isDecimal(num: number)](globalFunctions/isDecimal.md)
- [getNextPurchaseOrderCode()](globalFunctions/getNextPurchaseOrderCode.md)
- [createXeroInvoice(si: 'Shipments & Invoices')](globalFunctions/createXeroInvoice.md)
- [sendAllXeroInvs()](globalFunctions/sendAllXeroInvs.md)
- [getCustXeroID(c: Customer)](globalFunctions/getCustXeroID.md)
- [displayRecordButtons(print: boolean, manip: boolean, nav: boolean)](globalFunctions/displayRecordButtons.md)
- [hideCreateRecordOnPopup()](globalFunctions/hideCreateRecordOnPopup.md)
- [getSalesCount(formMonth: number, prods: 'Saleable Products')](globalFunctions/getSalesCount.md)
