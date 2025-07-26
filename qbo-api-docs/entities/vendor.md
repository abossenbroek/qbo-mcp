# Vendor

The Vendor entity represents suppliers from whom you purchase goods or services.

## Operations

### Create
Create a new vendor.

#### Request
```
POST /v3/company/{companyId}/vendor
```

#### Request Body
```json
{
  "DisplayName": "ABC Supplies Inc.",
  "CompanyName": "ABC Supplies Incorporated",
  "GivenName": "John",
  "FamilyName": "Smith",
  "PrintOnCheckName": "ABC Supplies Inc.",
  "Active": true,
  "PrimaryPhone": {
    "FreeFormNumber": "(555) 123-4567"
  },
  "PrimaryEmailAddr": {
    "Address": "vendor@abcsupplies.com"
  },
  "WebAddr": {
    "URI": "http://www.abcsupplies.com"
  },
  "BillAddr": {
    "Line1": "123 Main Street",
    "City": "Mountain View",
    "CountrySubDivisionCode": "CA",
    "PostalCode": "94043"
  },
  "TermRef": {
    "value": "3"
  },
  "Balance": 0,
  "Vendor1099": true,
  "TaxIdentifier": "12-3456789"
}
```

#### Response
```json
{
  "Vendor": {
    "DisplayName": "ABC Supplies Inc.",
    "CompanyName": "ABC Supplies Incorporated",
    "GivenName": "John",
    "FamilyName": "Smith",
    "PrintOnCheckName": "ABC Supplies Inc.",
    "Active": true,
    "PrimaryPhone": {
      "FreeFormNumber": "(555) 123-4567"
    },
    "PrimaryEmailAddr": {
      "Address": "vendor@abcsupplies.com"
    },
    "WebAddr": {
      "URI": "http://www.abcsupplies.com"
    },
    "BillAddr": {
      "Id": "123",
      "Line1": "123 Main Street",
      "City": "Mountain View",
      "CountrySubDivisionCode": "CA",
      "PostalCode": "94043"
    },
    "TermRef": {
      "value": "3",
      "name": "Net 30"
    },
    "Balance": 0,
    "Vendor1099": true,
    "TaxIdentifier": "12-3456789",
    "AcctNum": "V-1001",
    "domain": "QBO",
    "sparse": false,
    "Id": "67",
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
Retrieve a vendor by ID.

#### Request
```
GET /v3/company/{companyId}/vendor/{vendorId}
```

### Update
Update an existing vendor.

#### Request
```
POST /v3/company/{companyId}/vendor
```

Include the full vendor object with `Id` and updated `SyncToken`.

### Query
Query vendors with filters.

#### Request
```
GET /v3/company/{companyId}/query?query=select * from Vendor where Active = true
```

## Fields

### Basic Information
- `DisplayName` (required) - Display name (must be unique)
- `CompanyName` - Legal company name
- `GivenName` - Contact first name
- `MiddleName` - Contact middle name
- `FamilyName` - Contact last name
- `Suffix` - Name suffix
- `Title` - Contact title
- `PrintOnCheckName` - Name to print on checks
- `Active` - Active status

### Contact Information
- `PrimaryPhone` - Primary phone number
- `AlternatePhone` - Alternate phone
- `Mobile` - Mobile phone
- `Fax` - Fax number
- `PrimaryEmailAddr` - Primary email
- `WebAddr` - Website URL

### Addresses
- `BillAddr` - Billing address
- `ShipAddr` - Shipping address
- `OtherAddr` - Other address

### Financial Information
- `Balance` - Current balance (read-only)
- `TermRef` - Default payment terms
- `OpenBalanceDate` - Opening balance date
- `CreditLimit` - Credit limit
- `AcctNum` - Account number
- `Vendor1099` - 1099 vendor flag
- `TaxIdentifier` - Tax ID/SSN
- `CurrencyRef` - Currency for multi-currency

### Custom Fields
- `BillRate` - Default hourly bill rate
- `Notes` - Internal notes

## 1099 Vendor Setup
```json
{
  "Vendor1099": true,
  "TaxIdentifier": "12-3456789",
  "CompanyName": "ABC Supplies Incorporated",
  "BillAddr": {
    "Line1": "123 Main Street",
    "City": "Mountain View",
    "CountrySubDivisionCode": "CA",
    "PostalCode": "94043"
  }
}
```

## Contact Information Structure
```json
{
  "PrimaryPhone": {
    "FreeFormNumber": "(555) 123-4567"
  },
  "Mobile": {
    "FreeFormNumber": "(555) 987-6543"
  },
  "PrimaryEmailAddr": {
    "Address": "vendor@example.com"
  }
}
```

## Address Structure
```json
{
  "BillAddr": {
    "Line1": "123 Main Street",
    "Line2": "Suite 100",
    "Line3": "Building A",
    "Line4": "Office 42",
    "Line5": "Attn: Accounts Payable",
    "City": "Mountain View",
    "Country": "USA",
    "CountrySubDivisionCode": "CA",
    "PostalCode": "94043"
  }
}
```

## Common Queries

### Active Vendors
```
select * from Vendor where Active = true
```

### Vendors with Balance
```
select * from Vendor where Balance > '0'
```

### 1099 Vendors
```
select * from Vendor where Vendor1099 = true
```

### Search by Name
```
select * from Vendor where DisplayName like '%supplies%'
```

## Vendor Types

### Regular Vendor
Standard supplier for goods/services.

### Contractor (1099)
Independent contractors requiring 1099 forms:
```json
{
  "Vendor1099": true,
  "TaxIdentifier": "123-45-6789"
}
```

### Employee as Vendor
For employee reimbursements:
```json
{
  "DisplayName": "John Smith (Employee)",
  "IsEmployee": true
}
```

## Notes
- DisplayName must be unique
- Balance is read-only, calculated from transactions
- Vendor1099 flag required for 1099 reporting
- Can set default payment terms
- Supports multiple addresses
- Can track credit limits
- Used in bills, expenses, and purchase orders