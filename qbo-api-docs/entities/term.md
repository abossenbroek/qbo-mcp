# Term

The Term entity represents payment terms that define when payment is due for sales or purchases.

## Operations

### Create
Create new payment terms.

#### Request
```
POST /v3/company/{companyId}/term
```

#### Request Body
```json
{
  "Name": "Net 45",
  "DueDays": 45,
  "Type": "STANDARD",
  "Active": true
}
```

#### Response
```json
{
  "Term": {
    "Name": "Net 45",
    "Active": true,
    "Type": "STANDARD",
    "DueDays": 45,
    "domain": "QBO",
    "sparse": false,
    "Id": "8",
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
Retrieve payment terms by ID.

#### Request
```
GET /v3/company/{companyId}/term/{termId}
```

### Update
Update existing payment terms.

#### Request
```
POST /v3/company/{companyId}/term
```

Include the full term object with `Id` and updated `SyncToken`.

### Delete
Deactivate payment terms.

#### Request
```
POST /v3/company/{companyId}/term
```

Set `Active` to `false` with the `Id` and `SyncToken`.

### Query
Query payment terms with filters.

#### Request
```
GET /v3/company/{companyId}/query?query=select * from Term where Active = true
```

## Term Types

### Standard Terms
Net terms with fixed days:
```json
{
  "Name": "Net 30",
  "Type": "STANDARD",
  "DueDays": 30
}
```

### Date Driven Terms
Due on specific day of month:
```json
{
  "Name": "Due on 15th",
  "Type": "DATE_DRIVEN",
  "DayOfMonthDue": 15
}
```

### Discount Terms
Early payment discount:
```json
{
  "Name": "2/10 Net 30",
  "Type": "STANDARD",
  "DueDays": 30,
  "DiscountDays": 10,
  "DiscountPercent": 2.0
}
```

## Fields

- `Name` (required) - Term name
- `Active` - Whether terms are active
- `Type` - Term type (STANDARD or DATE_DRIVEN)
- `DueDays` - Days until due (for STANDARD type)
- `DayOfMonthDue` - Day of month due (for DATE_DRIVEN)
- `DiscountDays` - Days to qualify for discount
- `DiscountPercent` - Early payment discount percentage
- `DiscountDayOfMonth` - Day of month for discount

## Common Payment Terms

### Immediate Payment
```json
{
  "Name": "Due on receipt",
  "Type": "STANDARD",
  "DueDays": 0
}
```

### Net Terms
```json
{
  "Name": "Net 30",
  "Type": "STANDARD",
  "DueDays": 30
}
```

### End of Month
```json
{
  "Name": "Due EOM",
  "Type": "DATE_DRIVEN",
  "DayOfMonthDue": 31
}
```

### Early Payment Discount
```json
{
  "Name": "2/10 Net 30",
  "Type": "STANDARD",
  "DueDays": 30,
  "DiscountDays": 10,
  "DiscountPercent": 2.0
}
```

### Due on Specific Date
```json
{
  "Name": "Due 15th",
  "Type": "DATE_DRIVEN",
  "DayOfMonthDue": 15,
  "DueNextMonthDays": 20
}
```

## Usage in Transactions

### Invoice Terms
```json
{
  "Invoice": {
    "SalesTermRef": {
      "value": "3"
    }
  }
}
```

### Bill Terms
```json
{
  "Bill": {
    "SalesTermRef": {
      "value": "4"
    }
  }
}
```

### Customer Default Terms
```json
{
  "Customer": {
    "SalesTermRef": {
      "value": "3"
    }
  }
}
```

### Vendor Default Terms
```json
{
  "Vendor": {
    "TermRef": {
      "value": "4"
    }
  }
}
```

## Term Calculation Examples

### Standard Terms
- Invoice Date: 2025-01-15
- Terms: Net 30
- Due Date: 2025-02-14

### Date Driven Terms
- Invoice Date: 2025-01-20
- Terms: Due on 15th
- Due Date: 2025-02-15

### Discount Terms
- Invoice Date: 2025-01-15
- Terms: 2/10 Net 30
- Discount Due: 2025-01-25 (2% off)
- Full Due: 2025-02-14

## Notes
- Cannot delete terms, only deactivate
- Terms calculate due dates automatically
- Discount terms enable early payment incentives
- Date-driven terms useful for monthly billing
- Can set default terms on customers/vendors
- Terms affect aging reports