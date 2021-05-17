# getAllowance(productType: text)

This function takes in a productType as text (i.e. “small packet” or “bulk label”)

Depending on the value inputted, it either returns 1.05 (for a small packet) or 1.01 (for a bulk label)

This function was originally used in the ‘max able to makeup from seedlots’ fields, but when trying to add stock update functionality, the formula broke due to circular references, so those fields now calculate the allowance directly, rather than referencing the function.

It is currently still used in the assembly dashboard
