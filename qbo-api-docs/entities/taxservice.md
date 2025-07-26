# TaxService

The TaxService entity provides tax calculation services and manages automated tax settings.

## Operations

### Create Tax Code
Create a tax code using the tax service.

#### Request
```
POST /v3/company/{companyId}/taxservice/taxcode
```

#### Request Body
```json
{
  "TaxCode": {
    "TaxRateDetails": [
      {
        "TaxRateName": "myNewTaxRateName",
        "RateValue": 8.5,
        "TaxAgencyId": "1",
        "TaxApplicableOn": "Sales"
      }
    ],
    "TaxCodeName": "myNewTaxCode"
  }
}
```

#### Response
```json
{
  "TaxCodeId": "20"
}
```

### Add Tax Rate to Existing Code
Add a tax rate to an existing tax code.

#### Request
```
POST /v3/company/{companyId}/taxservice/taxcode/{taxCodeId}
```

#### Request Body
```json
{
  "TaxRateDetails": [
    {
      "TaxRateName": "additionalTaxRate",
      "RateValue": 2.5,
      "TaxAgencyId": "2",
      "TaxApplicableOn": "Sales"
    }
  ]
}
```

## Tax Calculation

### Calculate Tax for Transaction
Calculate tax for a transaction before saving.

#### Request
```
POST /v3/company/{companyId}/taxservice/calculate
```

#### Request Body
```json
{
  "Transaction": {
    "TxnDate": "2025-01-15",
    "CustomerRef": {
      "value": "1"
    },
    "Line": [
      {
        "Amount": 100.00,
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
    ],
    "BillAddr": {
      "Line1": "123 Main St",
      "City": "Mountain View",
      "CountrySubDivisionCode": "CA",
      "PostalCode": "94043"
    }
  }
}
```

#### Response
```json
{
  "TaxDetails": {
    "TotalTax": 8.25,
    "TaxLine": [
      {
        "Amount": 8.25,
        "DetailType": "TaxLineDetail",
        "TaxLineDetail": {
          "TaxRateRef": {
            "value": "3"
          },
          "PercentBased": true,
          "TaxPercent": 8.25,
          "NetAmountTaxable": 100.00
        }
      }
    ]
  }
}
```

## Automated Sales Tax Configuration

### Get AST Configuration
Retrieve automated sales tax settings.

#### Request
```
GET /v3/company/{companyId}/taxservice/config
```

#### Response
```json
{
  "ASTEnabled": true,
  "EffectiveDate": "2025-01-01",
  "CompanyAddress": {
    "Line1": "123 Main St",
    "City": "Mountain View",
    "CountrySubDivisionCode": "CA",
    "PostalCode": "94043"
  },
  "SalesTaxSettings": {
    "TaxBasis": "Accrual",
    "TaxableSales": true,
    "TaxOnShipping": true,
    "TaxOnHandling": false
  }
}
```

### Update AST Configuration
Update automated sales tax settings.

#### Request
```
POST /v3/company/{companyId}/taxservice/config
```

#### Request Body
```json
{
  "ASTEnabled": true,
  "SalesTaxSettings": {
    "TaxOnShipping": true,
    "TaxOnHandling": true
  }
}
```

## Tax Jurisdictions

### Get Jurisdictions
Get tax jurisdictions for an address.

#### Request
```
POST /v3/company/{companyId}/taxservice/jurisdictions
```

#### Request Body
```json
{
  "Address": {
    "Line1": "123 Main St",
    "City": "Mountain View",
    "CountrySubDivisionCode": "CA",
    "PostalCode": "94043"
  }
}
```

#### Response
```json
{
  "Jurisdictions": [
    {
      "JurisdictionId": "23",
      "JurisdictionName": "CALIFORNIA",
      "JurisdictionType": "State",
      "Rate": 7.25
    },
    {
      "JurisdictionId": "43-073",
      "JurisdictionName": "SANTA CLARA",
      "JurisdictionType": "County",
      "Rate": 1.0
    }
  ],
  "TotalRate": 8.25
}
```

## Tax Exemptions

### Create Exemption
Create a tax exemption for a customer.

#### Request
```
POST /v3/company/{companyId}/taxservice/exemption
```

#### Request Body
```json
{
  "CustomerRef": {
    "value": "1"
  },
  "ExemptionNumber": "EX-12345",
  "ExemptionReason": "Resale",
  "EffectiveDate": "2025-01-01",
  "ExpirationDate": "2025-12-31"
}
```

## Tax Return Preparation

### Get Tax Summary
Get tax summary for return preparation.

#### Request
```
GET /v3/company/{companyId}/taxservice/taxsummary?start_date=2025-01-01&end_date=2025-01-31
```

#### Response
```json
{
  "TaxSummary": {
    "TotalSales": 50000.00,
    "TaxableSales": 45000.00,
    "NonTaxableSales": 5000.00,
    "TotalTaxCollected": 3712.50,
    "TaxByJurisdiction": [
      {
        "JurisdictionName": "California",
        "TaxCollected": 3262.50,
        "TaxableSales": 45000.00
      },
      {
        "JurisdictionName": "Santa Clara County",
        "TaxCollected": 450.00,
        "TaxableSales": 45000.00
      }
    ]
  }
}
```

## Notes
- Tax service integrates with tax providers
- Automated Sales Tax (AST) simplifies compliance
- Real-time tax calculation based on addresses
- Handles multi-jurisdiction tax scenarios
- Manages exemptions and special rules
- Essential for accurate tax compliance