# Bill

A Bill object is an AP transaction representing a request-for-payment from a third party for goods/services rendered, received, or both.

## The bill object

### Attributes

| Attribute | Type | Description |
|-----------|------|-------------|
| **Id** | String | **Required for update**, read only, system defined, filterable, sortable. Unique identifier for this object. Sort order is ASC by default. |
| **VendorRef** | ReferenceType | **Required**, filterable, sortable. Reference to the vendor for this transaction. Query the Vendor name list resource to determine the appropriate Vendor object for this reference. Use Vendor.Id and Vendor.Name from that object for VendorRef.value and VendorRef.name, respectively. |
| **Line** | Line[0..n] | **Required**. Individual line items of a transaction. Valid Line types include: ItemBasedExpenseLine and AccountBasedExpenseLine |
| **SyncToken** | String | **Required for update**, read only, system defined. Version number of the object. It is used to lock an object for use by one app at a time. As soon as an application modifies an object, its SyncToken is incremented. Attempts to modify an object specifying an older SyncToken fails. Only the latest version of the object is maintained by QuickBooks Online. |
| **CurrencyRef** | CurrencyRefType | **Conditionally required**. Reference to the currency in which all amounts on the associated transaction are expressed. This must be defined if multicurrency is enabled for the company. Multicurrency is enabled for the company if Preferences.MultiCurrencyEnabled is set to true. Required if multicurrency is enabled for the company. |
| **GlobalTaxCalculation** | GlobalTaxCalculationEnum | **Conditionally required**. Method in which tax is applied. Allowed values are: TaxExcluded, TaxInclusive, and NotApplicable. Not applicable to US companies; required for non-US companies. |
| **TxnDate** | Date | Optional, filterable, sortable. The date entered by the user when this transaction occurred. For posting transactions, this is the posting date that affects the financial statements. If the date is not supplied, the current date on the server is used. Sort order is ASC by default. |
| **APAccountRef** | ReferenceType | Optional, filterable, sortable. Specifies to which AP account the bill is credited. Query the Account name list resource to determine the appropriate Account object for this reference. Use Account.Id and Account.Name from that object for APAccountRef.value and APAccountRef.name, respectively. The specified account must have Account.Classification set to Liability and Account.AccountSubType set to AccountsPayable. |
| **SalesTermRef** | ReferenceType | Optional, filterable, sortable. Reference to the Term associated with the transaction. Query the Term name list resource to determine the appropriate Term object for this reference. Use Term.Id and Term.Name from that object for SalesTermRef.value and SalesTermRef.name, respectively. |
| **LinkedTxn** | LinkedTxn[0..n] | Optional. Zero or more transactions linked to this Bill object. The LinkedTxn.TxnType can be set to PurchaseOrder, BillPaymentCheck or if using Minor Version 55 and above ReimburseCharge. Use LinkedTxn.TxnId as the ID of the transaction. |
| **TotalAmt** | BigDecimal | Optional, read only, filterable, sortable. Indicates the total amount of the transaction. This includes the total of all the charges, allowances, and taxes. Calculated by QuickBooks business logic; any value you supply is over-written by QuickBooks. |
| **TransactionLocationType** | String | Optional, minorVersion: 4. The account location. Valid values include: WithinFrance, FranceOverseas, OutsideFranceWithEU, OutsideEU. For France locales only. |
| **DueDate** | Date | Optional, filterable, sortable. Date when the payment of the transaction is due. If date is not provided, the number of days specified in SalesTermRef added the transaction date will be used. |
| **MetaData** | ModificationMetaData | Optional. Descriptive information about the object. The MetaData values are set by Data Services and are read only for all applications. |
| **DocNumber** | String | Optional, max 21 chars, filterable, sortable. Reference number for the transaction. If not explicitly provided at create time, a custom value can be provided. If no value is supplied, the resulting DocNumber is null. Throws an error when duplicate DocNumber is sent in the request. |
| **PrivateNote** | String | Optional, max 4000 chars. User entered, organization-private note about the transaction. This note does not appear on the invoice to the customer. This field maps to the Memo field on the Invoice form. |
| **TxnTaxDetail** | TxnTaxDetail | Optional. This data type provides information for taxes charged on the transaction as a whole. It captures the details of all taxes calculated for the transaction based on the tax codes referenced by the transaction. |
| **ExchangeRate** | Decimal | Optional. The number of home currency units it takes to equal one unit of currency specified by CurrencyRef. Applicable if multicurrency is enabled for the company. |
| **DepartmentRef** | ReferenceType | Optional. A reference to a Department object specifying the location of the transaction, as defined using location tracking in QuickBooks Online. |
| **IncludeInAnnualTPAR** | Boolean | Optional, minorVersion: 40. Include the supplier in the annual TPAR. TPAR stands for Taxable Payments Annual Report. |
| **HomeBalance** | Decimal | Read only, minorVersion: 3. Convenience field containing the amount in Balance expressed in terms of the home currency. Calculated by QuickBooks business logic. |
| **RecurDataRef** | ReferenceType | Read only, minorVersion: 52. A reference to the Recurring Transaction. It captures what recurring transaction template the Bill was created from. |
| **Balance** | Decimal | Read only, filterable. The balance reflecting any payments made against the transaction. Initially set to the value of TotalAmt. A Balance of 0 indicates the bill is fully paid. |

## Operations

### Create a bill

**Request Body**

The minimum elements to create a bill are:
- **VendorRef** (Required): Reference to the vendor for this transaction
- **Line** (Required): The minimum line item required for the request
- **CurrencyRef** (Conditionally required): Reference to the currency if multicurrency is enabled

### Delete a bill

This operation deletes the bill object specified in the request body. Include a minimum of Bill.Id and Bill.SyncToken in the request body. You must unlink any linked transactions associated with the bill object before deleting it.

**Request Body**
- **SyncToken** (Required): Version number of the object
- **Id** (Required): Unique identifier for this object

### Query a bill

Returns the results of the query.

### Read a bill

Retrieves the details of a bill that has been previously created.

### Full update a bill

Use this operation to update any of the writable fields of an existing bill object. The request body must include all writable fields of the existing object as returned in a read response. Writable fields omitted from the request body are set to NULL. The ID of the object to update is specified in the request body.

## Sample Bill Object

```json
{
  "Bill": {
    "SyncToken": "2",
    "domain": "QBO",
    "APAccountRef": {
      "name": "Accounts Payable (A/P)",
      "value": "33"
    },
    "VendorRef": {
      "name": "Norton Lumber and Building Materials",
      "value": "46"
    },
    "TxnDate": "2014-11-06",
    "TotalAmt": 103.55,
    "CurrencyRef": {
      "name": "United States Dollar",
      "value": "USD"
    },
    "LinkedTxn": [
      {
        "TxnId": "118",
        "TxnType": "BillPaymentCheck"
      }
    ]
  }
}
```