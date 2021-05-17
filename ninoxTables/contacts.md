# Contacts

The ‘contacts’ table is a child of the ‘customer’ table.

This contacts table is only used for customers with the ‘business’ field set to ‘yes’, otherwise contacts are stored on the customer record itself. This contacts table is designed to allow businesses to have multiple contacts.

It contains fields for the contacts name, email, mobile, phone & website, with additional ‘yes/no’ fields for the types of communication the contact should be used for (though as of 15/1/2021, these fields are not being used anywhere directly)
