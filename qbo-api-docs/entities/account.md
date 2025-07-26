# Account

Accounts are what businesses use to track transactions. Accounts can track money coming in (income or revenue) and going out (expenses). They can also track the value of things (assets), like vehicles and equipment. There are five basic account types: asset, liability, income, expense, and equity. Accounts are part of the chart of accounts, the unique list of accounts each business puts together to do their accounting. Accountants often call accounts "ledgers". Learn more about accounts and the chart of accounts. The account object is what you'll use to do actions with the end-users accounts. Note: If you need to delete an account, set the Active attribute to false in an object update request. This makes it inactive. The account itself isn't permanently deleted, but is hidden for display purposes.

## Attributes

### Id

- **Type**: String
- **Required**: Required for update
- **Metadata**: Required for update, read only, system defined

Unique identifier for this object.
Sort order is ASC by default.

### Name

- **Type**: String
- **Required**: Required
- **Metadata**: Required, max character: max 100 characters

User recognizable name for the Account.
Account.Name attribute must not contain double quotes (") or colon (:).

### SyncToken

- **Type**: String
- **Required**: Required for update
- **Metadata**: Required for update, read only, system defined

Version number of the object. It is used to lock an object for use by one app at a time. As soon as an application modifies an object, its SyncToken is incremented. Attempts to modify an object specifying an older SyncToken fails. Only the latest version of the object is maintained by QuickBooks Online.

### AcctNum

- **Type**: String
- **Required**: Conditionally required
- **Metadata**: Conditionally required

User-defined account number to help the user in identifying the account within the chart-of-accounts and in deciding what should be posted to the account. The Account.AcctNum attribute must not contain colon (:).Name must be unique.For French Locales:Length must be between 6 and 20 charactersMust start with the account number from the master category list.Name limited to alpha-numeric characters.
 Max length for Account.AcctNum:AU & CA: 20 characters.US, UK & IN: 7 characters

### CurrencyRef

- **Type**: CurrencyRef
- **Metadata**: Optional, read only

Reference to the currency in which this account holds amounts.

### ParentRef

- **Type**: ReferenceType
- **Metadata**: Optional

Specifies the Parent AccountId if this represents a SubAccount.

### Description

- **Type**: String
- **Metadata**: Optional, max character: maximum of 100 chars

User entered description for the account, which may include user entered information to guide bookkeepers/accountants in deciding what journal entries to post to the account.

### Active

- **Type**: Boolean
- **Metadata**: Optional

Whether or not active inactive accounts may be hidden from most display purposes and may not be posted to.

### MetaData

- **Type**: ModificationMetaData
- **Metadata**: Optional

Descriptive information about the object. The MetaData values are set by Data Services and are read only for all applications.

### SubAccount

- **Type**: Boolean
- **Metadata**: read only, system defined

Specifies whether this object represents a parent (false) or subaccount (true). Please note that accounts of these types - OpeningBalanceEquity, UndepositedFunds, RetainedEarnings, CashReceiptIncome, CashExpenditureExpense, ExchangeGainOrLoss cannot have a sub account and cannot be a sub account of another account.

### Classification

- **Type**: String
- **Metadata**: read only, system defined

The classification of an account. Not supported for non-posting accounts.
 Valid values include: Asset, Equity, Expense, Liability, Revenue

### FullyQualifiedName

- **Type**: String
- **Metadata**: read only, system defined

Fully qualified name of the object; derived from Name and ParentRef. The fully qualified name prepends the topmost parent, followed by each subaccount separated by colons and takes the form of
Parent:Account1:SubAccount1:SubAccount2. System generated. Limited to 5 levels.

### TxnLocationType

- **Type**: String
- **Metadata**: minorVersion: 5

The account location. Valid values include:
WithinFrance
FranceOverseas
OutsideFranceWithEU
OutsideEU

For France locales, only.

### AccountType

- **Type**: AccountTypeEnum

A detailed account classification that specifies the use of this account. The type is based on the Classification.

### CurrentBalanceWithSubAccounts

- **Type**: Decimal
- **Metadata**: read only

Specifies the cumulative balance amount for the current Account and all its sub-accounts.

### AccountAlias

- **Type**: String
- **Metadata**: minorVersion: 5

A user friendly name for the account. It must be unique across all account categories. For France locales, only.
For example, if an account is created under category 211 with AccountAlias of Terrains, then the system does not allow creation of an account with same AccountAlias of Terrains for any other category except 211. In other words, 211001 and 215001 accounts cannot have same AccountAlias because both belong to different account category.
For France locales, only.

### TaxCodeRef

- **Type**: ReferenceType
- **Metadata**: minorVersion: 3

Reference to the default tax code used by this account. Tax codes are referenced by the TaxCode.Id in the TaxCode object. Available when endpoint is invoked with the minorversion=3 query parameter. For global locales, only.

### AccountSubType

- **Type**: String

The account sub-type classification and is based on the AccountType value.

### CurrentBalance

- **Type**: Decimal
- **Metadata**: read only

Specifies the balance amount for the current Account. Valid for Balance Sheet accounts.

## Sample Object

```json
{
  "Account": {
    "FullyQualifiedName": 
      "MyJobs", 
    "domain": "QBO", 
    "Name": "MyJobs", 
    "Classification": "Asset", 
    "AccountSubType": 
      "AccountsReceivable", 
    "CurrencyRef": {
      "name": "United States Dollar", 
      "value": "USD"
    }, 
    "CurrentBalanceWithSubAccounts": 0, 
    "sparse": false, 
    "MetaData": {
      "CreateTime": "2014-12-31T09:29:05-08:00", 
      "LastUpdatedTime": "2014-12-31T09:29:05-08:00"
    }, 
    "AccountType": "Accounts Receivable", 
    "CurrentBalance": 0, 
    "Active": true, 
    "SyncToken": "0", 
    "Id": "94", 
    "SubAccount": false
  }, 
  "time": "2014-12-31T09:29:05.717-08:00"
}
```

## Create an Account

Name must be unique.
The Account.Name attribute must not contain double quotes (") or colon (:).
The Account.AcctNum attribute must not contain a colon (:).

### Request Body

The minimum elements to create an Account object are listed here.

**ATTRIBUTES**

- **Name** (Required, max 100 characters): User recognizable name for the Account. Account.Name attribute must not contain double quotes (") or colon (:).
- **AcctNum** (Conditionally required): User-defined account number to help the user in identifying the account within the chart-of-accounts and in deciding what should be posted to the account. The Account.AcctNum attribute must not contain colon (:). For France locales: Name must be unique. Length must be between 6 and 20 characters. Must start with the account number from the master category list. Name limited to alpha-numeric characters. Required for France locales.
- **TaxCodeRef** (Conditionally required, minorVersion: 3): Reference to the default tax code used by this account. Tax codes are referenced by the TaxCode.Id in the TaxCode object. Available when endpoint is invoked with the minorversion=3 query parameter. For global locales, only. Required for France locales.
- **AccountType** (Conditionally required): A detailed account classification that specifies the use of this account. The type is based on the Classification. Required if AccountSubType is not specified.
- **AccountSubType** (Conditionally required): The account sub-type classification and is based on the AccountType value. Required if AccountType is not specified.

### Returns

Returns the newly created Account object.

### Request URL

```
POST /v3/company/<realmID>/account
Content type: application/json
Production Base URL: https://quickbooks.api.intuit.com
Sandbox Base URL: https://sandbox-quickbooks.api.intuit.com
```

### Request Body Example

```json
{
  "Name": "MyJobs_test", 
  "AccountType": "Accounts Receivable"
}
```

### Response Example

```json
{
  "Account": {
    "FullyQualifiedName": "MyJobs", 
    "domain": "QBO", 
    "Name": "MyJobs", 
    "Classification": "Asset", 
    "AccountSubType": "AccountsReceivable", 
    "CurrencyRef": {
      "name": "United States Dollar", 
      "value": "USD"
    }, 
    "CurrentBalanceWithSubAccounts": 0, 
    "sparse": false, 
    "MetaData": {
      "CreateTime": "2014-12-31T09:29:05-08:00", 
      "LastUpdatedTime": "2014-12-31T09:29:05-08:00"
    }, 
    "AccountType": "Accounts Receivable", 
    "CurrentBalance": 0, 
    "Active": true, 
    "SyncToken": "0", 
    "Id": "94", 
    "SubAccount": false
  }, 
  "time": "2014-12-31T09:29:05.717-08:00"
}
```

## Query an Account

### Returns

Returns the results of the query.

### Request URL

```
GET /v3/company/<realmID>/query?query=<selectStatement>
Content type: text/plain
Production Base URL: https://quickbooks.api.intuit.com
Sandbox Base URL: https://sandbox-quickbooks.api.intuit.com
```

### Sample Query

```sql
select * from Account where Metadata.CreateTime > '2014-12-31'
```

### Response Example

```json
{
  "QueryResponse": {
    "startPosition": 1, 
    "Account": [
      {
        "FullyQualifiedName": "Canadian Accounts Receivable", 
        "domain": "QBO", 
        "Name": "Canadian Accounts Receivable", 
        "Classification": "Asset", 
        "AccountSubType": "AccountsReceivable", 
        "CurrencyRef": {
          "name": "United States Dollar", 
          "value": "USD"
        }, 
        "CurrentBalanceWithSubAccounts": 0, 
        "sparse": false, 
        "MetaData": {
          "CreateTime": "2015-06-23T09:38:18-07:00", 
          "LastUpdatedTime": "2015-06-23T09:38:18-07:00"
        }, 
        "AccountType": "Accounts Receivable", 
        "CurrentBalance": 0, 
        "Active": true, 
        "SyncToken": "0", 
        "Id": "92", 
        "SubAccount": false
      }
    ], 
    "maxResults": 3
  }, 
  "time": "2015-07-13T12:35:57.651-07:00"
}
```

## Read an Account

Retrieves the details of an Account object that has been previously created.

### Returns

Returns the Account object.

### Request URL

```
GET /v3/company/<realmID>/account/<accountId>
Production Base URL: https://quickbooks.api.intuit.com
Sandbox Base URL: https://sandbox-quickbooks.api.intuit.com
```

### Response Example

```json
{
  "Account": {
    "FullyQualifiedName": "Accounts Payable (A/P)", 
    "domain": "QBO", 
    "Name": "Accounts Payable (A/P)", 
    "Classification": "Liability", 
    "AccountSubType": "AccountsPayable", 
    "CurrentBalanceWithSubAccounts": -1091.23, 
    "sparse": false, 
    "MetaData": {
      "CreateTime": "2014-09-12T10:12:02-07:00", 
      "LastUpdatedTime": "2015-06-30T15:09:07-07:00"
    }, 
    "AccountType": "Accounts Payable", 
    "CurrentBalance": -1091.23, 
    "Active": true, 
    "SyncToken": "0", 
    "Id": "33", 
    "SubAccount": false
  }, 
  "time": "2015-07-13T12:50:36.72-07:00"
}
```

## Full Update an Account

Use this operation to update any of the writable fields of an existing account object. The request body must include all writable fields of the existing object as returned in a read response. Writable fields omitted from the request body are set to NULL. The ID of the object to update is specified in the request body.

### Request Body

All writable attributes from the Account object are required in the request body for a full update.

### Returns

The account response body.

### Request URL

```
POST /v3/company/<realmID>/account
Content type: application/json
Production Base URL: https://quickbooks.api.intuit.com
Sandbox Base URL: https://sandbox-quickbooks.api.intuit.com
```

### Request Body Example

```json
{
  "FullyQualifiedName": "Accounts Payable (A/P)", 
  "domain": "QBO", 
  "SubAccount": false, 
  "Description": "Description added during update.", 
  "Classification": "Liability", 
  "AccountSubType": "AccountsPayable", 
  "CurrentBalanceWithSubAccounts": -1091.23, 
  "sparse": false, 
  "MetaData": {
    "CreateTime": "2014-09-12T10:12:02-07:00", 
    "LastUpdatedTime": "2015-06-30T15:09:07-07:00"
  }, 
  "AccountType": "Accounts Payable", 
  "CurrentBalance": -1091.23, 
  "Active": true, 
  "SyncToken": "0", 
  "Id": "33", 
  "Name": "Accounts Payable (A/P)"
}
```

### Response Example

```json
{
  "Account": {
    "FullyQualifiedName": "Accounts Payable (A/P)", 
    "domain": "QBO", 
    "SubAccount": false, 
    "Description": "Description added during update.", 
    "Classification": "Liability", 
    "AccountSubType": "AccountsPayable", 
    "CurrentBalanceWithSubAccounts": -1091.23, 
    "sparse": false, 
    "MetaData": {
      "CreateTime": "2014-09-12T10:12:02-07:00", 
      "LastUpdatedTime": "2015-07-13T15:35:13-07:00"
    }, 
    "AccountType": "Accounts Payable", 
    "CurrentBalance": -1091.23, 
    "Active": true, 
    "SyncToken": "1", 
    "Id": "33", 
    "Name": "Accounts Payable (A/P)"
  }, 
  "time": "2015-07-13T15:31:25.618-07:00"
}
```
