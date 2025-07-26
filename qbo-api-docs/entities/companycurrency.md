# CompanyCurrency

The CompanyCurrency resource represents the currencies that have been set up for use by a company in QuickBooks Online when multicurrency is enabled.

## The companycurrency object

### Attributes

| Attribute | Type | Description |
|-----------|------|-------------|
| **Id** | String | Read only, system defined. Unique identifier for this object. |
| **Code** | String | **Required**. Three letter ISO 4217 currency code (e.g., USD, EUR, GBP). |
| **Name** | String | Optional. Full name of the currency (e.g., United States Dollar, Euro, British Pound). |
| **Active** | Boolean | Optional. Whether or not the currency is currently enabled for use by the company. Default value is true. |
| **SyncToken** | String | **Required for update**. Version number of the object. It is used to lock an object for use by one app at a time. |
| **MetaData** | ModificationMetaData | Optional. Descriptive information about the object. The MetaData values are set by Data Services and are read only for all applications. |

## Operations

### Create a companycurrency

Creates a new CompanyCurrency object. This adds a currency to the list of currencies available for use in the company.

**Required fields:**
- Code (must be a valid ISO 4217 currency code)

**Prerequisites:**
- Multicurrency must be enabled for the company (Preferences.MultiCurrencyEnabled = true)
- The currency code must not already exist in the company

### Query a companycurrency

Returns the results of the query for CompanyCurrency objects.

**Example query:**
```
SELECT * FROM CompanyCurrency WHERE Active = true
```

### Read a companycurrency

Retrieves the details of a CompanyCurrency that has been previously created.

### Update a companycurrency

Updates an existing CompanyCurrency object. You can only update the Active status of a currency.

**Required fields:**
- Id
- SyncToken
- Code

**Note:** You cannot change the currency code after creation. You can only activate or deactivate currencies.

## Important Notes

1. **Home Currency**: The company's home currency is set during company creation and cannot be changed.
2. **Currency Usage**: Once a currency is used in transactions, it cannot be deleted, only deactivated.
3. **Exchange Rates**: Exchange rates are managed separately and are not part of the CompanyCurrency object.
4. **ISO Standards**: Only valid ISO 4217 currency codes are accepted.

## Common Currency Codes

- USD - United States Dollar
- EUR - Euro
- GBP - British Pound
- CAD - Canadian Dollar
- AUD - Australian Dollar
- JPY - Japanese Yen
- CHF - Swiss Franc
- CNY - Chinese Yuan
- INR - Indian Rupee
- MXN - Mexican Peso