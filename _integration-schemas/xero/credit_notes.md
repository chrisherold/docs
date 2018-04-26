---
tap: "xero"
version: "1.0"

name: "credit_notes"
doc-link: &api-doc https://developer.xero.com/documentation/api/credit-notes
singer-schema: https://github.com/singer-io/tap-xero/blob/master/tap_xero/schemas/credit_notes.json
description: |
  The `credit_notes` table contains info about credit notes. A credit note is similar to an invoice, except it reduces the amount you owe a supplier or the amount a customer owes you.

replication-method: "Incremental"

api-method:
  name: getCreditNotes
  doc-link: *api-doc

attributes:
  - name: "CreditNoteID"
    type: "string"
    primary-key: true
    description: "The credit note ID."

  - name: "UpdatedDateUTC"
    type: "date-time"
    replication-key: true
    description: "The date the credit note was last updated, in UTC."

  - name: "Type"
    type: "string"
    description: |
      The credit note type. Possible values are:

      - `ACCPAYCREDIT` - An Accounts Payable (supplier) credit note
      - `ACCRECCREDIT` - An Accounts Receivable (customer) credit note

  - name: "Contact"
    type: 
    description: ""

  - name: "Date"
    type: "date-time"
    description: "The date the credit note was issued."

  - name: "DueDate"
    type: "date-time"
    description: ""

  - name: "DueDateString"
    type: "date-time"
    description: ""

  - name: "Status"
    type: "string"
    description: |
      The status of the credit note. Possible values are:

      - `DRAFT`
      - `SUBMITTED` - Awaiting approval
      - `DELETED`
      - `AUTHORISED` - Approved and awaiting payment OR partially paid
      - `PAID` - Completely paid
      - `VOIDED`

  - name: "LineAmountTypes"
    type: "string"
    description: |
      The type of amounts that the line items in the credit note contain. Possible values are:

      - `Exclusive` - Line items are exclusive of tax
      - `Inclusive` - Line items are inclusive tax
      - `NoTax` - Line items have no tax

  - name: "LineItems"
    type: 
    description: ""

  - name: "SubTotal"
    type: "number"
    description: "The subtotal of the credit note, excluding taxes."

  - name: "AppliedAmount"
    type: "number"
    description: ""

  - name: "TotalTax"
    type: "number"
    description: "The total tax on the credit note."

  - name: "Total"
    type: "number"
    description: "The total of the credit note, calculated as `SubTotal + TotalTax`."

  - name: "CurrencyCode"
    type: "string"
    description: "The currency code used for the credit note."
    foreign-key: true

  - name: "FullyPaidOnDate"
    type: "date-time"
    description: "The date that the credit note was fully paid, in UTC."

  - name: "CreditNoteNumber"
    type: "string"
    description: |
      An identifier for the credit note. The value this field contains varies depending on the credit note `Type`:

      - `ACCPAYCREDIT` - A non-unique alpha-numeric code identifying the credit note. In the Xero UI, this displays as **Reference**.
      - `ACCRECCREDIT` - A unique alpha-numeric code identifying the credit note.

  - name: "Reference"
    type: "string"
    description: "**Applicable only to `Type: ACCRECCREDIT` credit notes**. An additional reference number."

  - name: "SentToContact"
    type: "boolean"
    description: "If `true`, the credit note has been sent to a contact via the Xero app."

  - name: "CurrencyRate"
    type: "number"
    description: "The currency rate for a multicurrency invoice. If no rate is specified, the [XE.com day rate](http://help.xero.com/#CurrencySettings$Rates) is used."

  - name: "RemainingCredit"
    type: "number"
    description: "The remaining credit balance on the credit note."

  - name: "Allocations"
    type: "array"
    description: ""

  - name: "BrandingThemeID"
    type: "string"
    description: "The ID of the branding theme applied to the credit note."
    foreign-key: true

  - name: "HasAttachments"
    type: "boolean"
    description: "If `true`, the credit note has an attachment."

  - name: "DateString"
    type: "date-time"
    description: ""

  # - name: "ID"
  #   type: 
  #   description: ""
---