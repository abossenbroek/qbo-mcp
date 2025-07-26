# ExchangeRate

## Attributes

### SyncToken
- **Required for update**: Yes
- **Read only**: Yes
- **System defined**: Yes
- **Type**: String
- **Description**: Version number of the object. It is used to lock an object for use by one app at a time. As soon as an application modifies an object, its SyncToken is incremented. Attempts to modify an object specifying an older SyncToken fails. Only the latest version of the object is maintained by QuickBooks Online.

### AsOfDate
- **Required for update**: Yes
- **Type**: Boolean
- **Filterable**: Yes
- **Description**: Date on which this exchange rate was set.

### SourceCurrencyCode
- **Required for update**: Yes
- **Max character**: Exactly 3 chars
- **Type**: String
- **Filterable**: Yes
- **Description**: The source currency from which the exchange rate is specified, and usually. Specify as a three letter string representing the ISO 4217 code for the currency. For example, USD, AUD, EUR, and so on. For example, in the equation 65 INR = 1 USD, INR is the source currency.

### Rate
- **Required for update**: Yes
- **Type**: Decimal
- **Description**: The exchange rate between SourceCurrencyCode and TargetCurrencyCode on the AsOfDate date.

### CustomField
- **Optional**: Yes
- **Type**: CustomField
- **Description**: One of, up to three custom fields for the transaction. Available for custom fields so configured for the company. Check Preferences.SalesFormsPrefs.CustomField and Preferences.VendorAndPurchasesPrefs.POCustomField for custom fields currently configured. Click here to learn about managing custom fields.
- Show child attributes

### TargetCurrencyCode
- **Optional**: Yes
- **Max character**: Exactly 3 chars
- **Type**: String
- **Description**: The target currency against which the exchange rate is specified. Specify as a three letter string representing the ISO 4217 code for the currency. For example, USD, AUD, EUR, and so on. For example, in the equation 65 INR = 1 USD, USA is the target currency.

### MetaData
- **Optional**: Yes
- **Type**: ModificationMetaData
- **Filterable**: Yes
- **Sortable**: Yes
- **Description**: Descriptive information about the object. The MetaData values are set by Data Services and are read only for all applications.
- Show child attributes

---
*Source: https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/exchangerate*