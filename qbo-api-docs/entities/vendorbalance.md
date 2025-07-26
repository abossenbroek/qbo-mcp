# VendorBalance

The VendorBalance report provides a summary of balances owed to vendors.

## Operations

### Query
Retrieve vendor balance report data.

#### Request
```
GET /v3/company/{companyId}/reports/VendorBalance
```

#### Parameters
- `report_date` (string): As-of date for balances (YYYY-MM-DD)
- `accounting_method` (string): Accounting method - Cash or Accrual (default: Accrual)
- `sort_by` (string): Sort by name or total
- `sort_order` (string): Sort order - ascend or descend
- `vendor` (string): Filter by specific vendor ID

#### Response
```json
{
  "Header": {
    "Time": "2025-01-15T10:30:00-08:00",
    "ReportName": "VendorBalance",
    "DateMacro": "Today",
    "ReportDate": "2025-01-15",
    "ReportBasis": "Accrual",
    "Currency": "USD",
    "Option": [
      {
        "Name": "NoReportData",
        "Value": "false"
      }
    ]
  },
  "Columns": {
    "Column": [
      {
        "ColTitle": "",
        "ColType": "Vendor",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "vendor"
          }
        ]
      },
      {
        "ColTitle": "Total",
        "ColType": "Money",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "total"
          }
        ]
      }
    ]
  },
  "Rows": {
    "Row": [
      {
        "ColData": [
          {
            "value": "Bob's Burger Joint",
            "id": "44"
          },
          {
            "value": "250.00"
          }
        ],
        "type": "Data"
      },
      {
        "ColData": [
          {
            "value": "Hicks Hardware",
            "id": "41"
          },
          {
            "value": "450.00"
          }
        ],
        "type": "Data"
      },
      {
        "ColData": [
          {
            "value": "Norton Lumber and Building Materials",
            "id": "42"
          },
          {
            "value": "1250.00"
          }
        ],
        "type": "Data"
      },
      {
        "ColData": [
          {
            "value": "Robertson & Associates",
            "id": "43"
          },
          {
            "value": "375.00"
          }
        ],
        "type": "Data"
      },
      {
        "ColData": [
          {
            "value": "Tania's Nursery",
            "id": "45"
          },
          {
            "value": "825.00"
          }
        ],
        "type": "Data"
      },
      {
        "Summary": {
          "ColData": [
            {
              "value": "TOTAL"
            },
            {
              "value": "3150.00"
            }
          ]
        },
        "type": "Section",
        "group": "GrandTotal"
      }
    ]
  }
}
```

## Report Features

### Balance Summary
- Shows current balance for each vendor
- Only includes vendors with non-zero balances
- As-of date determines balance calculation

### Sorting Options
- By vendor name (alphabetical)
- By balance amount (highest to lowest)

## Common Use Cases

### Cash Flow Planning
- See total amount owed to vendors
- Prioritize payments
- Plan cash requirements

### Vendor Management
- Identify largest vendor balances
- Monitor vendor relationships
- Track payment obligations

### Period-End Review
- Verify AP balance
- Review vendor liabilities
- Prepare for payments

## Related Reports

### Aged Payables
For aging analysis:
```
GET /v3/company/{companyId}/reports/AgedPayables
```

### Vendor Balance Detail
For transaction details:
```
GET /v3/company/{companyId}/reports/VendorBalanceDetail
```

## As-Of Date Examples

### Current Date
```
GET /v3/company/{companyId}/reports/VendorBalance?report_date=2025-01-15
```

### Prior Month End
```
GET /v3/company/{companyId}/reports/VendorBalance?report_date=2024-12-31
```

### Specific Vendor
```
GET /v3/company/{companyId}/reports/VendorBalance?vendor=41
```

## Balance Calculation

Includes:
- Unpaid bills
- Partial payments
- Vendor credits (reduce balance)
- Credit card charges (if vendor)

Excludes:
- Paid bills
- Unapplied vendor credits
- Purchase orders (until billed)

## Notes
- Shows point-in-time balances
- Zero balance vendors excluded
- Credits show as negative amounts
- Total matches AP on balance sheet
- Useful for payment planning
- Can filter by specific vendor