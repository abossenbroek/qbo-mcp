# TaxPayment

The TaxPayment entity represents a payment made to a tax agency for collected taxes.

## Operations

### Create
Create a new tax payment.

#### Request
```
POST /v3/company/{companyId}/taxpayment
```

#### Request Body
```json
{
  "TaxAgencyRef": {
    "value": "1"
  },
  "PaymentDate": "2025-01-15",
  "PaymentAccountRef": {
    "value": "35"
  },
  "Amount": 1250.00,
  "Description": "Q4 2024 Sales Tax Payment",
  "PaymentMethod": "Check",
  "PaymentRefNum": "1234",
  "PrivateNote": "Sales tax for October through December 2024"
}
```

#### Response
```json
{
  "TaxPayment": {
    "Id": "12",
    "SyncToken": "0",
    "TaxAgencyRef": {
      "value": "1",
      "name": "Board of Equalization"
    },
    "PaymentDate": "2025-01-15",
    "PaymentAccountRef": {
      "value": "35",
      "name": "Checking"
    },
    "Amount": 1250.00,
    "Description": "Q4 2024 Sales Tax Payment",
    "PaymentMethod": "Check",
    "PaymentRefNum": "1234",
    "PrivateNote": "Sales tax for October through December 2024",
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
Retrieve a tax payment by ID.

#### Request
```
GET /v3/company/{companyId}/taxpayment/{taxPaymentId}
```

### Update
Update an existing tax payment.

#### Request
```
POST /v3/company/{companyId}/taxpayment
```

Include the full tax payment object with `Id` and updated `SyncToken`.

### Delete
Delete a tax payment.

#### Request
```
POST /v3/company/{companyId}/taxpayment?operation=delete
```

#### Request Body
```json
{
  "Id": "12",
  "SyncToken": "0"
}
```

### Query
Query tax payments with filters.

#### Request
```
GET /v3/company/{companyId}/query?query=select * from TaxPayment where PaymentDate > '2025-01-01'
```

## Fields

- `TaxAgencyRef` (required) - Reference to the tax agency
- `PaymentDate` (required) - Date of payment
- `PaymentAccountRef` (required) - Bank account used for payment
- `Amount` (required) - Payment amount
- `Description` - Payment description
- `PaymentMethod` - Payment method (Check, EFT, etc.)
- `PaymentRefNum` - Check or reference number
- `PrivateNote` - Internal note

## Payment Methods

- `Check` - Check payment
- `Cash` - Cash payment
- `CreditCard` - Credit card payment
- `EFT` - Electronic funds transfer
- `Other` - Other payment method

## Tax Payment Workflow

### 1. Review Tax Liability
Check tax liability report:
```
GET /v3/company/{companyId}/reports/TaxSummary
```

### 2. Create Tax Payment
Record payment to tax agency:
```json
{
  "TaxAgencyRef": {
    "value": "1"
  },
  "Amount": 1250.00,
  "PaymentDate": "2025-01-15"
}
```

### 3. Link to Tax Return
For filed returns:
```json
{
  "TaxReturnRef": {
    "value": "TR-2024-Q4"
  }
}
```

## Common Scenarios

### Quarterly Sales Tax Payment
```json
{
  "TaxAgencyRef": {
    "value": "1"
  },
  "PaymentDate": "2025-01-15",
  "PaymentAccountRef": {
    "value": "35"
  },
  "Amount": 3500.00,
  "Description": "Q4 2024 Sales Tax",
  "PaymentMethod": "EFT",
  "PaymentRefNum": "EFT-20250115"
}
```

### Payroll Tax Payment
```json
{
  "TaxAgencyRef": {
    "value": "2"
  },
  "PaymentDate": "2025-01-15",
  "PaymentAccountRef": {
    "value": "35"
  },
  "Amount": 5200.00,
  "Description": "Federal Payroll Tax Deposit",
  "PaymentMethod": "EFT"
}
```

### VAT Payment
```json
{
  "TaxAgencyRef": {
    "value": "3"
  },
  "PaymentDate": "2025-01-31",
  "PaymentAccountRef": {
    "value": "35"
  },
  "Amount": 8750.00,
  "Description": "VAT Payment - January 2025",
  "PaymentMethod": "Check",
  "PaymentRefNum": "5678"
}
```

## Reports Integration

Tax payments affect:
- Tax liability reports
- Cash flow statements
- Tax summary reports
- Agency-specific reports

## Notes
- Reduces tax liability balance
- Affects specified bank account
- Can be linked to tax returns
- Supports multiple payment methods
- Important for tax compliance tracking
- May require supporting documentation