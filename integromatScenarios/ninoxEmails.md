# Send Emails Via Ninox

This scenario is used to send Invoices to customers via the [Email Form](../ninoxTables/emailForm.md) in Ninox

Originally, we were using the sendEmail() function within Ninox, but there were a couple of issues with this

- It does not save a copy of the E-Mail when it is sent
- There is no way of knowing if an E-Mail bounces back.

The scenario itself is simple.

It accepts data via webhook, for example:

```json
{
    "to": "davidprice@seedcooperative.org.uk",                                      `the address to send the invoice to`
    "subject": "Sales Invoices for Sales Order: #15798 from Seed Co-operative",     `the subject of the email`
    "body": ".....",                                                                `HTML based e-mail body`
    "id": 123                                                                       `the id of the email form record within Ninox to download the invoice pdf from`
}
```

Once it has accepted the data, it downloads the file from that invoice

It then sends an email to the given to address (from seedshop@seedcooperative.org.uk), bcc'ing in seedshop@seedcooperative.org.uk, using the given subject/ body/ attachment.

If either of these 2 steps fail, an email alert will be sent to the Seed Shop email account

Additionally, there is a rule on the seed shop email to move the copies of these emails to the 'Sent from Ninox' email folder.
