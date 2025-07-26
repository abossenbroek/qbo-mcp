# TaxRate

The TaxRate entity represents individual tax rates that can be used in tax codes.

## Operations

### Create
Create a new tax rate (non-US companies only).

#### Request
```
POST /v3/company/{companyId}/taxrate
```

#### Request Body
```json
{
  "Name": "State Sales Tax",
  "Description": "California State Sales Tax",
  "RateValue": 7.25,
  "AgencyRef": {
    "value": "1"
  },
  "TaxReturnLineRef": {
    "value": "1"
  },
  "EffectiveDate": "2025-01-01",
  "Active": true,
  "SpecialTaxType": "NONE"
}
```

#### Response
```json
{
  "TaxRate": {
    "Name": "State Sales Tax",
    "Description": "California State Sales Tax",
    "RateValue": 7.25,
    "AgencyRef": {
      "value": "1",
      "name": "California State Board of Equalization"
    },
    "TaxReturnLineRef": {
      "value": "1"
    },
    "EffectiveDate": "2025-01-01",
    "Active": true,
    "SpecialTaxType": "NONE",
    "DisplayType": "ReadOnly",
    "domain": "QBO",
    "sparse": false,
    "Id": "5",
    "SyncToken": "0",
    "MetaData": {
      "CreateTime": "2025-01-15T10:00:00-08:00",
      "LastUpdatedTime": "2025-01-15T10:00:00-08:00"
    }
  },
  "time": "2025-01-15T10:00:00.000-08:00"
}
```

### Read
Retrieve a tax rate by ID.

#### Request
```
GET /v3/company/{companyId}/taxrate/{taxRateId}
```

### Update
Update an existing tax rate.

#### Request
```
POST /v3/company/{companyId}/taxrate
```

Include the full tax rate object with `Id` and updated `SyncToken`.

### Query
Query tax rates with filters.

#### Request
```
GET /v3/company/{companyId}/query?query=select * from TaxRate where Active = true
```

## Fields

- `Name` (required) - Tax rate name
- `RateValue` (required) - Tax percentage rate
- `AgencyRef` (required) - Tax agency reference
- `Description` - Description of the tax rate
- `Active` - Whether the rate is active
- `EffectiveDate` - Date rate becomes effective
- `EndDate` - Date rate expires
- `SpecialTaxType` - Special tax type designation
- `DisplayType` - Display type for UI
- `TaxReturnLineRef` - Tax return line mapping

## Special Tax Types

- `NONE` - Standard tax rate
- `ZERO_RATE` - Zero-rated items
- `EXEMPT` - Tax exempt
- `REVERSECHARGE` - Reverse charge VAT
- `NOTAPPLICABLE` - Tax not applicable
- `ADJUSTMENT` - Tax adjustment rate

## Tax Rate Examples

### Sales Tax Rate
```json
{
  "Name": "CA Sales Tax",
  "RateValue": 7.25,
  "AgencyRef": {
    "value": "1"
  },
  "Description": "California state sales tax",
  "SpecialTaxType": "NONE"
}
```

### VAT Rate
```json
{
  "Name": "Standard VAT",
  "RateValue": 20.0,
  "AgencyRef": {
    "value": "2"
  },
  "Description": "Standard VAT rate",
  "SpecialTaxType": "NONE"
}
```

### Zero Rate
```json
{
  "Name": "Zero Rate",
  "RateValue": 0.0,
  "AgencyRef": {
    "value": "1"
  },
  "Description": "Zero-rated supplies",
  "SpecialTaxType": "ZERO_RATE"
}
```

### Reverse Charge
```json
{
  "Name": "Reverse Charge",
  "RateValue": 0.0,
  "AgencyRef": {
    "value": "2"
  },
  "Description": "Reverse charge VAT",
  "SpecialTaxType": "REVERSECHARGE"
}
```

## Usage in Tax Codes

Tax rates are referenced in tax codes:
```json
{
  "TaxCode": {
    "SalesTaxRateList": {
      "TaxRateDetail": [
        {
          "TaxRateRef": {
            "value": "5"
          },
          "TaxTypeApplicable": "TaxOnAmount"
        }
      ]
    }
  }
}
```

## Effective Dating

Handle rate changes:
```json
{
  "Name": "State Tax 2025",
  "RateValue": 7.5,
  "EffectiveDate": "2025-01-01",
  "EndDate": "2025-12-31"
}
```

## Agency Assignment

Each rate must be assigned to an agency:
```json
{
  "AgencyRef": {
    "value": "1"
  }
}
```

## Notes
- US companies use automated tax rates
- Non-US companies can create custom rates
- Rates can have effective date ranges
- Special types handle exempt/zero scenarios
- Linked to tax agencies for reporting
- Used within tax codes for calculations