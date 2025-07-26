# TaxAgency

The TaxAgency entity represents a tax authority to which taxes are paid.

## Operations

### Create
Create a new tax agency.

#### Request
```
POST /v3/company/{companyId}/taxagency
```

#### Request Body
```json
{
  "DisplayName": "California State Board of Equalization",
  "TaxRegistrationNumber": "123-45-6789",
  "TaxAgencyConfig": {
    "TaxTypeApplicableTo": "Sales",
    "TaxFormNum": "BOE-401-A",
    "ReportingPeriod": "Monthly"
  }
}
```

#### Response
```json
{
  "TaxAgency": {
    "Id": "1",
    "SyncToken": "0",
    "DisplayName": "California State Board of Equalization",
    "TaxRegistrationNumber": "123-45-6789",
    "TaxAgencyConfig": {
      "TaxTypeApplicableTo": "Sales",
      "TaxFormNum": "BOE-401-A",
      "ReportingPeriod": "Monthly"
    },
    "Active": true,
    "domain": "QBO",
    "sparse": false,
    "MetaData": {
      "CreateTime": "2025-01-15T10:00:00-08:00",
      "LastUpdatedTime": "2025-01-15T10:00:00-08:00"
    }
  },
  "time": "2025-01-15T10:00:00.000-08:00"
}
```

### Read
Retrieve a tax agency by ID.

#### Request
```
GET /v3/company/{companyId}/taxagency/{taxAgencyId}
```

### Update
Update an existing tax agency.

#### Request
```
POST /v3/company/{companyId}/taxagency
```

Include the full tax agency object with `Id` and updated `SyncToken`.

### Query
Query tax agencies with filters.

#### Request
```
GET /v3/company/{companyId}/query?query=select * from TaxAgency where Active = true
```

## Fields

- `DisplayName` (required) - Agency name
- `TaxRegistrationNumber` - Your registration number with the agency
- `TaxAgencyConfig` - Configuration settings
- `Active` - Whether the agency is active
- `LastFileDate` - Last tax return filing date
- `TaxTrackedOnPurchases` - Track tax on purchases
- `TaxTrackedOnSales` - Track tax on sales

## TaxAgencyConfig Structure

```json
{
  "TaxAgencyConfig": {
    "TaxTypeApplicableTo": "Sales",
    "TaxFormNum": "BOE-401-A",
    "ReportingPeriod": "Monthly",
    "FilingDueDate": "15",
    "PaymentDueDate": "15"
  }
}
```

### TaxTypeApplicableTo Options
- `Sales` - Sales tax agency
- `Purchase` - Purchase/VAT tax agency
- `Payroll` - Payroll tax agency
- `Other` - Other tax types

### ReportingPeriod Options
- `Monthly`
- `Quarterly`
- `Annually`

## Common Tax Agencies

### State Sales Tax
```json
{
  "DisplayName": "California State Board of Equalization",
  "TaxRegistrationNumber": "123-45-6789",
  "TaxAgencyConfig": {
    "TaxTypeApplicableTo": "Sales",
    "TaxFormNum": "BOE-401-A",
    "ReportingPeriod": "Quarterly"
  }
}
```

### Federal Tax
```json
{
  "DisplayName": "Internal Revenue Service",
  "TaxRegistrationNumber": "12-3456789",
  "TaxAgencyConfig": {
    "TaxTypeApplicableTo": "Payroll",
    "TaxFormNum": "941",
    "ReportingPeriod": "Quarterly"
  }
}
```

### VAT Authority
```json
{
  "DisplayName": "HM Revenue & Customs",
  "TaxRegistrationNumber": "GB123456789",
  "TaxAgencyConfig": {
    "TaxTypeApplicableTo": "Purchase",
    "TaxFormNum": "VAT100",
    "ReportingPeriod": "Quarterly"
  }
}
```

## Agency Contact Information

```json
{
  "ContactInfo": {
    "ContactName": "Tax Department",
    "Phone": {
      "FreeFormNumber": "1-800-123-4567"
    },
    "Email": {
      "Address": "taxes@agency.gov"
    },
    "WebAddr": {
      "URI": "https://www.taxagency.gov"
    }
  }
}
```

## Filing Information

Track filing details:
```json
{
  "LastFileDate": "2024-12-31",
  "NextFilingDueDate": "2025-01-31",
  "FilingFrequency": "Quarterly",
  "PaymentMethod": "EFT"
}
```

## Linking to Transactions

Tax agencies are referenced in:
- Tax rates
- Tax codes
- Tax payments
- Tax liability reports

## Notes
- Essential for tax compliance tracking
- Links tax rates to collecting authority
- Tracks filing deadlines and frequency
- Stores registration numbers
- Can include contact information
- Used in tax reports and payments