# TaxCode

The TaxCode entity represents tax codes used to specify tax treatment for transactions.

## Operations

### Create
Create a new tax code (non-US companies only).

#### Request
```
POST /v3/company/{companyId}/taxcode
```

#### Request Body
```json
{
  "Name": "GST 10%",
  "Description": "Goods and Services Tax at 10%",
  "Active": true,
  "Taxable": true,
  "TaxGroup": false,
  "SalesTaxRateList": {
    "TaxRateDetail": [
      {
        "TaxRateRef": {
          "value": "4"
        },
        "TaxTypeApplicable": "TaxOnAmount",
        "TaxOrder": 0
      }
    ]
  },
  "PurchaseTaxRateList": {
    "TaxRateDetail": [
      {
        "TaxRateRef": {
          "value": "5"
        },
        "TaxTypeApplicable": "TaxOnAmount",
        "TaxOrder": 0
      }
    ]
  }
}
```

#### Response
```json
{
  "TaxCode": {
    "Name": "GST 10%",
    "Description": "Goods and Services Tax at 10%",
    "Active": true,
    "Taxable": true,
    "TaxGroup": false,
    "SalesTaxRateList": {
      "TaxRateDetail": [
        {
          "TaxRateRef": {
            "value": "4",
            "name": "GST"
          },
          "TaxTypeApplicable": "TaxOnAmount",
          "TaxOrder": 0
        }
      ]
    },
    "PurchaseTaxRateList": {
      "TaxRateDetail": [
        {
          "TaxRateRef": {
            "value": "5",
            "name": "GST on purchases"
          },
          "TaxTypeApplicable": "TaxOnAmount",
          "TaxOrder": 0
        }
      ]
    },
    "domain": "QBO",
    "sparse": false,
    "Id": "7",
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
Retrieve a tax code by ID.

#### Request
```
GET /v3/company/{companyId}/taxcode/{taxCodeId}
```

### Update
Update an existing tax code.

#### Request
```
POST /v3/company/{companyId}/taxcode
```

Include the full tax code object with `Id` and updated `SyncToken`.

### Query
Query tax codes with filters.

#### Request
```
GET /v3/company/{companyId}/query?query=select * from TaxCode where Active = true
```

## Tax Code Types

### Standard Tax Code
Single tax rate:
```json
{
  "Name": "Standard Rate",
  "Taxable": true,
  "TaxGroup": false,
  "SalesTaxRateList": {
    "TaxRateDetail": [
      {
        "TaxRateRef": {
          "value": "3"
        }
      }
    ]
  }
}
```

### Tax Group
Multiple tax rates combined:
```json
{
  "Name": "State + County Tax",
  "Taxable": true,
  "TaxGroup": true,
  "SalesTaxRateList": {
    "TaxRateDetail": [
      {
        "TaxRateRef": {
          "value": "3"
        },
        "TaxTypeApplicable": "TaxOnAmount",
        "TaxOrder": 0
      },
      {
        "TaxRateRef": {
          "value": "4"
        },
        "TaxTypeApplicable": "TaxOnAmount",
        "TaxOrder": 1
      }
    ]
  }
}
```

### Non-Taxable Code
```json
{
  "Name": "NON",
  "Description": "Non-Taxable Sales",
  "Taxable": false,
  "Active": true
}
```

## Special Tax Codes (US)

### TAX
- Default taxable code
- Automatically calculates based on location
- Used with Automated Sales Tax

### NON
- Non-taxable transactions
- No tax calculated
- For exempt items/customers

## Fields

- `Name` (required) - Tax code name
- `Description` - Description of the tax code
- `Active` - Whether the tax code is active
- `Taxable` - Whether this code applies tax
- `TaxGroup` - Whether this is a group of tax rates
- `SalesTaxRateList` - Tax rates for sales
- `PurchaseTaxRateList` - Tax rates for purchases
- `TaxCodeRef` - Reference for linked tax codes

## TaxRateDetail Structure
```json
{
  "TaxRateDetail": [
    {
      "TaxRateRef": {
        "value": "3"
      },
      "TaxTypeApplicable": "TaxOnAmount",
      "TaxOrder": 0
    }
  ]
}
```

### TaxTypeApplicable Options
- `TaxOnAmount` - Tax calculated on amount
- `TaxOnAmountPlusTax` - Tax on tax (compound)
- `TaxOnTax` - Tax calculated on other taxes

## Usage Examples

### On Invoice Line
```json
{
  "Line": [
    {
      "DetailType": "SalesItemLineDetail",
      "SalesItemLineDetail": {
        "ItemRef": {
          "value": "1"
        },
        "TaxCodeRef": {
          "value": "TAX"
        }
      }
    }
  ]
}
```

### On Customer
Set default tax code:
```json
{
  "DefaultTaxCodeRef": {
    "value": "3"
  }
}
```

### On Item
Set default tax code:
```json
{
  "SalesTaxCodeRef": {
    "value": "TAX"
  },
  "PurchaseTaxCodeRef": {
    "value": "TAX"
  }
}
```

## Notes
- US companies have limited tax code options (TAX/NON)
- Non-US companies can create custom tax codes
- Tax groups combine multiple tax rates
- Tax order determines calculation sequence
- Linked to tax rates for actual percentages
- Essential for accurate tax calculation