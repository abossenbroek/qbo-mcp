# TransactionListWithSplits

The TransactionListWithSplits report provides detailed transaction information including all split lines.

## Operations

### Query
Retrieve transaction list with splits report data.

#### Request
```
GET /v3/company/{companyId}/reports/TransactionListWithSplits
```

#### Parameters
- `start_date` (string, required): Start date for the report period (YYYY-MM-DD)
- `end_date` (string, required): End date for the report period (YYYY-MM-DD)
- `accounting_method` (string): Accounting method - Cash or Accrual (default: Accrual)
- `account` (string): Filter by specific account ID
- `customer` (string): Filter by customer ID
- `vendor` (string): Filter by vendor ID
- `class` (string): Filter by class ID
- `department` (string): Filter by department ID
- `sort_by` (string): Sort by default, date, name, or amount

#### Response
```json
{
  "Header": {
    "Time": "2025-01-15T10:30:00-08:00",
    "ReportName": "TransactionListWithSplits",
    "ReportBasis": "Accrual",
    "StartPeriod": "2025-01-01",
    "EndPeriod": "2025-01-31",
    "Currency": "USD"
  },
  "Columns": {
    "Column": [
      {
        "ColTitle": "Date",
        "ColType": "Date"
      },
      {
        "ColTitle": "Transaction Type",
        "ColType": "String"
      },
      {
        "ColTitle": "Num",
        "ColType": "String"
      },
      {
        "ColTitle": "Name",
        "ColType": "String"
      },
      {
        "ColTitle": "Memo/Description",
        "ColType": "String"
      },
      {
        "ColTitle": "Account",
        "ColType": "String"
      },
      {
        "ColTitle": "Class",
        "ColType": "String"
      },
      {
        "ColTitle": "Department",
        "ColType": "String"
      },
      {
        "ColTitle": "Debit",
        "ColType": "Money"
      },
      {
        "ColTitle": "Credit",
        "ColType": "Money"
      }
    ]
  },
  "Rows": {
    "Row": [
      {
        "Header": {
          "ColData": [
            {
              "value": "2025-01-05"
            },
            {
              "value": "Invoice"
            },
            {
              "value": "1037"
            },
            {
              "value": "Amy's Bird Sanctuary"
            },
            {
              "value": "Rock Fountain installation"
            },
            {
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": "302.50"
            },
            {
              "value": ""
            }
          ]
        },
        "Rows": {
          "Row": [
            {
              "ColData": [
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": "Rock Fountain"
                },
                {
                  "value": "Sales of Product Income"
                },
                {
                  "value": "Installation"
                },
                {
                  "value": "Garden Center"
                },
                {
                  "value": ""
                },
                {
                  "value": "275.00"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": "CA Sales Tax"
                },
                {
                  "value": "Sales Tax Payable"
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": "27.50"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": "Accounts Receivable"
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": "302.50"
                },
                {
                  "value": ""
                }
              ],
              "type": "Data"
            }
          ]
        },
        "type": "Section"
      },
      {
        "Header": {
          "ColData": [
            {
              "value": "2025-01-10"
            },
            {
              "value": "Bill"
            },
            {
              "value": "203"
            },
            {
              "value": "Hicks Hardware"
            },
            {
              "value": "January supplies"
            },
            {
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": "525.00"
            }
          ]
        },
        "Rows": {
          "Row": [
            {
              "ColData": [
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": "Office supplies"
                },
                {
                  "value": "Office Supplies"
                },
                {
                  "value": ""
                },
                {
                  "value": "Main Office"
                },
                {
                  "value": "125.00"
                },
                {
                  "value": ""
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": "Tools"
                },
                {
                  "value": "Tools and Equipment"
                },
                {
                  "value": "Installation"
                },
                {
                  "value": "Garden Center"
                },
                {
                  "value": "400.00"
                },
                {
                  "value": ""
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": "Accounts Payable"
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": "525.00"
                }
              ],
              "type": "Data"
            }
          ]
        },
        "type": "Section"
      },
      {
        "Header": {
          "ColData": [
            {
              "value": "2025-01-15"
            },
            {
              "value": "Journal Entry"
            },
            {
              "value": "JE-101"
            },
            {
              "value": ""
            },
            {
              "value": "Monthly depreciation"
            },
            {
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": "500.00"
            },
            {
              "value": "500.00"
            }
          ]
        },
        "Rows": {
          "Row": [
            {
              "ColData": [
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": "Equipment depreciation"
                },
                {
                  "value": "Depreciation Expense"
                },
                {
                  "value": ""
                },
                {
                  "value": "Garden Center"
                },
                {
                  "value": "300.00"
                },
                {
                  "value": ""
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": "Vehicle depreciation"
                },
                {
                  "value": "Depreciation Expense"
                },
                {
                  "value": ""
                },
                {
                  "value": "West Branch"
                },
                {
                  "value": "200.00"
                },
                {
                  "value": ""
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": "Equipment"
                },
                {
                  "value": "Accumulated Depreciation"
                },
                {
                  "value": ""
                },
                {
                  "value": "Garden Center"
                },
                {
                  "value": ""
                },
                {
                  "value": "300.00"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": "Vehicles"
                },
                {
                  "value": "Accumulated Depreciation"
                },
                {
                  "value": ""
                },
                {
                  "value": "West Branch"
                },
                {
                  "value": ""
                },
                {
                  "value": "200.00"
                }
              ],
              "type": "Data"
            }
          ]
        },
        "type": "Section"
      }
    ]
  }
}
```

## Report Features

### Split Details
- Shows every line item within transactions
- Includes account distributions
- Displays class and department assignments
- Shows both debit and credit amounts

### Transaction Header
- Date, type, number, and name
- Total debits and credits
- Overall transaction description

### Split Lines
- Individual line descriptions
- Account assignments
- Class and department tracking
- Line-level amounts

## Common Use Cases

### Account Analysis
- See all transactions affecting an account
- Review account distributions
- Verify proper coding

### Class/Department Tracking
- Analyze transactions by dimension
- Ensure proper allocation
- Review cost center activity

### Audit Trail
- Full transaction detail
- Complete account distributions
- Supporting documentation

### Journal Entry Review
- See all journal entry lines
- Verify balanced entries
- Review adjustments

## Filtering Examples

### By Account
```
GET /v3/company/{companyId}/reports/TransactionListWithSplits?account=35
```

### By Class
```
GET /v3/company/{companyId}/reports/TransactionListWithSplits?class=1
```

### By Date Range and Customer
```
GET /v3/company/{companyId}/reports/TransactionListWithSplits?start_date=2025-01-01&end_date=2025-01-31&customer=1
```

## Notes
- Shows complete double-entry detail
- Debits and credits always balance
- Includes all tracking dimensions
- More detailed than standard transaction list
- Useful for detailed analysis and audits
- Can be large for high-volume periods