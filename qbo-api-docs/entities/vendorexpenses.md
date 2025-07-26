# VendorExpenses

The VendorExpenses report provides a detailed breakdown of expenses by vendor.

## Operations

### Query
Retrieve vendor expenses report data.

#### Request
```
GET /v3/company/{companyId}/reports/VendorExpenses
```

#### Parameters
- `start_date` (string, required): Start date for the report period (YYYY-MM-DD)
- `end_date` (string, required): End date for the report period (YYYY-MM-DD)
- `accounting_method` (string): Accounting method - Cash or Accrual (default: Accrual)
- `vendor` (string): Filter by specific vendor ID
- `summarize_column_by` (string): Summarize columns by Days, Weeks, Months, Quarters, Years, Vendors, or Total
- `expense_account` (string): Filter by expense account
- `sort_by` (string): Sort by default or total
- `sort_order` (string): Sort order - ascend or descend

#### Response
```json
{
  "Header": {
    "Time": "2025-01-15T10:30:00-08:00",
    "ReportName": "VendorExpenses",
    "ReportBasis": "Accrual",
    "StartPeriod": "2025-01-01",
    "EndPeriod": "2025-01-31",
    "SummarizeColumnsBy": "Total",
    "Currency": "USD"
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
            "value": ""
          }
        ],
        "Rows": {
          "Row": [
            {
              "ColData": [
                {
                  "value": "Meals and Entertainment",
                  "id": "13"
                },
                {
                  "value": "152.50"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "Travel Meals",
                  "id": "86"
                },
                {
                  "value": "325.00"
                }
              ],
              "type": "Data"
            }
          ]
        },
        "Summary": {
          "ColData": [
            {
              "value": "Total for Bob's Burger Joint"
            },
            {
              "value": "477.50"
            }
          ]
        },
        "type": "Section"
      },
      {
        "ColData": [
          {
            "value": "Hicks Hardware",
            "id": "41"
          },
          {
            "value": ""
          }
        ],
        "Rows": {
          "Row": [
            {
              "ColData": [
                {
                  "value": "Job Materials",
                  "id": "64"
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
                  "value": "Office Supplies",
                  "id": "23"
                },
                {
                  "value": "125.00"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "Tools and Equipment",
                  "id": "87"
                },
                {
                  "value": "850.00"
                }
              ],
              "type": "Data"
            }
          ]
        },
        "Summary": {
          "ColData": [
            {
              "value": "Total for Hicks Hardware"
            },
            {
              "value": "2225.00"
            }
          ]
        },
        "type": "Section"
      },
      {
        "ColData": [
          {
            "value": "Norton Lumber and Building Materials",
            "id": "42"
          },
          {
            "value": ""
          }
        ],
        "Rows": {
          "Row": [
            {
              "ColData": [
                {
                  "value": "Job Materials",
                  "id": "64"
                },
                {
                  "value": "3500.00"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "Cost of Goods Sold",
                  "id": "80"
                },
                {
                  "value": "1850.00"
                }
              ],
              "type": "Data"
            }
          ]
        },
        "Summary": {
          "ColData": [
            {
              "value": "Total for Norton Lumber and Building Materials"
            },
            {
              "value": "5350.00"
            }
          ]
        },
        "type": "Section"
      },
      {
        "ColData": [
          {
            "value": "Robertson & Associates",
            "id": "43"
          },
          {
            "value": ""
          }
        ],
        "Rows": {
          "Row": [
            {
              "ColData": [
                {
                  "value": "Legal & Professional Fees",
                  "id": "12"
                },
                {
                  "value": "750.00"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "Accounting",
                  "id": "85"
                },
                {
                  "value": "500.00"
                }
              ],
              "type": "Data"
            }
          ]
        },
        "Summary": {
          "ColData": [
            {
              "value": "Total for Robertson & Associates"
            },
            {
              "value": "1250.00"
            }
          ]
        },
        "type": "Section"
      },
      {
        "Summary": {
          "ColData": [
            {
              "value": "TOTAL"
            },
            {
              "value": "9302.50"
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

## Report Structure

### Vendor Grouping
- Primary level: Vendors
- Secondary level: Expense accounts
- Shows breakdown of spending by category

### Expense Categories
Common expense accounts include:
- Cost of Goods Sold
- Job Materials
- Office Supplies
- Professional Fees
- Travel & Entertainment
- Utilities
- Rent
- Insurance

## Common Use Cases

### Vendor Analysis
- Total spending per vendor
- Expense category breakdown
- Identify major suppliers

### Cost Control
- Monitor vendor spending
- Compare periods
- Identify cost savings opportunities

### 1099 Preparation
- Track payments to contractors
- Verify 1099 amounts
- Support tax filing

### Budget Comparison
- Compare actual to budget
- Analyze spending patterns
- Plan future purchases

## Filtering Examples

### Single Vendor
```
GET /v3/company/{companyId}/reports/VendorExpenses?vendor=41
```

### By Expense Account
```
GET /v3/company/{companyId}/reports/VendorExpenses?expense_account=64
```

### Monthly Comparison
```
GET /v3/company/{companyId}/reports/VendorExpenses?summarize_column_by=Months
```

## Time Period Analysis

### Year-to-Date
```
GET /v3/company/{companyId}/reports/VendorExpenses?start_date=2025-01-01&end_date=2025-12-31
```

### Prior Year Comparison
```
GET /v3/company/{companyId}/reports/VendorExpenses?start_date=2024-01-01&end_date=2024-12-31
```

## Transaction Types Included
- Bills (when paid in cash basis)
- Checks
- Expenses
- Credit card charges
- Bill payments (cash basis)
- Vendor credits (reduce expenses)

## Notes
- Shows expense account breakdown
- Useful for vendor negotiations
- Helps identify spending patterns
- Can track by time period
- Supports 1099 reporting
- Basis affects timing of recognition