# BillPayment

A BillPayment object represents the financial transaction of payment of bills that the business owner receives from a vendor for goods or services purchased from the vendor.

## The billpayment object

### Attributes

| Attribute | Type | Description |
|-----------|------|-------------|
| **Id** | String | **Required for update**, read only, system defined, filterable, sortable. Unique Identifier for an Intuit entity (object). Sort order is ASC by default. |
| **VendorRef** | ReferenceType | **Required**, filterable, sortable. Reference to the vendor for this transaction. Query the Vendor name list resource to determine the appropriate Vendor object for this reference. Use Vendor.Id and Vendor.Name from that object for VendorRef.value and VendorRef.name, respectively. |
| **Line** | Line[0..n] | **Required**. Individual line items representing zero or more Bill, VendorCredit, and JournalEntry objects linked to this BillPayment object. Use Line.LinkedTxn.TxnId as the ID in a separate Bill, VendorCredit, or JournalEntry read request to retrieve details of the linked object. |
| **TotalAmt** | BigDecimal | **Required**, filterable, sortable. Indicates the total amount associated with this payment. This includes the total of all the payments from the payment line details. If TotalAmt is greater than the total on the lines being paid, the overpayment is treated as a credit and exposed as such on the QuickBooks UI. It cannot be negative. |
| **PayType** | BillPaymentTypeEnum | **Required**. The payment type. Valid values include: Check, CreditCard |
| **SyncToken** | String | **Required for update**, read only, system defined. Version number of the object. It is used to lock an object for use by one app at a time. As soon as an application modifies an object, its SyncToken is incremented. Attempts to modify an object specifying an older SyncToken fails. Only the latest version of the object is maintained by QuickBooks Online. |
| **CurrencyRef** | CurrencyRefType | **Conditionally required**. Reference to the currency in which all amounts on the associated transaction are expressed. This must be defined if multicurrency is enabled for the company. Multicurrency is enabled for the company if Preferences.MultiCurrencyEnabled is set to true. Required if multicurrency is enabled for the company. |
| **DocNumber** | String | Optional, max 21 chars, filterable, sortable. Reference number for the transaction. If not explicitly provided at create time, a custom value can be provided. If no value is supplied, the resulting DocNumber is null. Throws an error when duplicate DocNumber is sent in the request. |
| **PrivateNote** | String | Optional, max 4000 chars. User entered, organization-private note about the transaction. This note does not appear on the invoice to the customer. This field maps to the Memo field on the form. |
| **TxnDate** | Date | Optional, filterable, sortable. The date entered by the user when this transaction occurred. For posting transactions, this is the posting date that affects the financial statements. If the date is not supplied, the current date on the server is used. |
| **ExchangeRate** | Decimal | Optional. The number of home currency units it takes to equal one unit of currency specified by CurrencyRef. Applicable if multicurrency is enabled for the company. |
| **DepartmentRef** | ReferenceType | Optional. A reference to a Department object specifying the location of the transaction, as defined using location tracking in QuickBooks Online. |
| **CheckPayment** | CheckPayment | **Conditionally required**. Information about a check payment for the transaction. Used when PayType is Check. |
| **CreditCardPayment** | CreditCardPayment | **Conditionally required**. Information about a credit card payment for the transaction. Used when PayType is CreditCard. |
| **APAccountRef** | ReferenceType | Optional, filterable, sortable. Specifies to which AP account the bill is credited. Query the Account name list resource to determine the appropriate Account object for this reference. |
| **MetaData** | ModificationMetaData | Optional. Descriptive information about the object. The MetaData values are set by Data Services and are read only for all applications. |
| **TxnSource** | String | Optional. Used internally to specify originating source of a credit card transaction. |
| **ProcessBillPayment** | Boolean | Optional. Indicates that the payment should be processed by merchant account service. QBO will process the payment and actually issue a transaction to the merchant account service to initiate the funds transfer. |

## Operations

### Create a billpayment

Creates a new BillPayment object to record payment of bills from vendors.

**Required fields:**
- VendorRef
- Line (with linked transactions)
- TotalAmt
- PayType
- Either CheckPayment or CreditCardPayment details based on PayType

### Query a billpayment

Returns the results of the query for BillPayment objects.

### Read a billpayment

Retrieves the details of a BillPayment that has been previously created.

### Update a billpayment

Updates an existing BillPayment object. The request body must include all writable fields of the existing object as returned in a read response. Writable fields omitted from the request body are set to NULL.

**Required fields:**
- Id
- SyncToken
- All other required fields from create operation

### Delete a billpayment

Deletes an existing BillPayment object.

**Required fields:**
- Id
- SyncToken

Note: You must unlink any linked transactions before deleting a BillPayment.