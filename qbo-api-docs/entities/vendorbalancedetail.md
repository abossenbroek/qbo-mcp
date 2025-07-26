# VendorBalanceDetail

The VendorBalanceDetail report provides detailed transaction information for vendor balances.

## Operations

### Query
Retrieve vendor balance detail report data.

#### Request
```
GET /v3/company/{companyId}/reports/VendorBalanceDetail
```

#### Parameters
- `report_date` (string): As-of date for balances (YYYY-MM-DD)
- `accounting_method` (string): Accounting method - Cash or Accrual (default: Accrual)
- `vendor` (string): Filter by specific vendor ID
- `sort_by` (string): Sort by date or vendor
- `sort_order` (string): Sort order - ascend or descend
- `columns` (string): Comma-separated list of columns to include

#### Response
```json
{
  "Header": {
    "Time": "2025-01-15T10:30:00-08:00",
    "ReportName": "VendorBalanceDetail",
    "DateMacro": "Today",
    "ReportDate": "2025-01-15",
    "ReportBasis": "Accrual",
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
        "ColTitle": "Due Date",
        "ColType": "Date"
      },
      {
        "ColTitle": "Amount",
        "ColType": "Money"
      },
      {
        "ColTitle": "Open Balance",
        "ColType": "Money"
      },
      {
        "ColTitle": "Balance",
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
              "value": "Hicks Hardware",
              "id": "41"
            }
          ]
        },
        "Rows": {
          "Row": [
            {
              "ColData": [
                {
                  "value": "2024-12-15"
                },
                {
                  "value": "Bill"
                },
                {
                  "value": "195"
                },
                {
                  "value": "2025-01-14"
                },
                {
                  "value": "325.00"
                },
                {
                  "value": "325.00"
                },
                {
                  "value": "325.00"
                }
              ],
              "type": "Data"
            },
            {
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
                  "value": "2025-02-09"
                },
                {
                  "value": "525.00"
                },
                {
                  "value": "525.00"
                },
                {
                  "value": "850.00"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "2025-01-12"
                },
                {
                  "value": "Bill Payment (Check)"
                },
                {
                  "value": "1045"
                },
                {
                  "value": ""
                },
                {
                  "value": "-325.00"
                },
                {
                  "value": ""
                },
                {
                  "value": "525.00"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "2025-01-15"
                },
                {
                  "value": "Vendor Credit"
                },
                {
                  "value": "VC-100"
                },
                {
                  "value": ""
                },
                {
                  "value": "-75.00"
                },
                {
                  "value": "-75.00"
                },
                {
                  "value": "450.00"
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
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": "450.00"
            },
            {
              "value": "450.00"
            },
            {
              "value": ""
            }
          ]
        },
        "type": "Section"
      },
      {
        "Header": {
          "ColData": [
            {
              "value": "Norton Lumber and Building Materials",
              "id": "42"
            }
          ]
        },
        "Rows": {
          "Row": [
            {
              "ColData": [
                {
                  "value": "2025-01-08"
                },
                {
                  "value": "Bill"
                },
                {
                  "value": "567"
                },
                {
                  "value": "2025-01-22"
                },
                {
                  "value": "1250.00"
                },
                {
                  "value": "1250.00"
                },
                {
                  "value": "1250.00"
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
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": "1250.00"
            },
            {
              "value": "1250.00"
            },
            {
              "value": ""
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
              "value": "1700.00"
            },
            {
              "value": ""
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

### Transaction Details
Shows for each vendor:
- Bill transactions (increase balance)
- Bill payments (decrease balance)
- Vendor credits (decrease balance)
- Running balance calculation

### Column Definitions
- **Date** - Transaction date
- **Transaction Type** - Type of transaction
- **Num** - Document number
- **Due Date** - Payment due date
- **Amount** - Transaction amount
- **Open Balance** - Unpaid portion
- **Balance** - Running balance

## Transaction Types

### Bills
- Increase vendor balance
- Show due dates
- Track open amounts

### Bill Payments
- Decrease vendor balance
- Show payment method
- Apply to specific bills

### Vendor Credits
- Decrease vendor balance
- Can be applied to bills
- Show as negative amounts

## Common Use Cases

### Vendor Reconciliation
- Match vendor statements
- Verify all transactions recorded
- Identify discrepancies

### Payment Planning
- Review due dates
- See payment history
- Plan upcoming payments

### Audit Support
- Detailed transaction trail
- Support vendor balances
- Document relationships

## Filtering Examples

### Single Vendor Detail
```
GET /v3/company/{companyId}/reports/VendorBalanceDetail?vendor=41
```

### As of Prior Month
```
GET /v3/company/{companyId}/reports/VendorBalanceDetail?report_date=2024-12-31
```

### Custom Columns
```
GET /v3/company/{companyId}/reports/VendorBalanceDetail?columns=date,txn_type,num,amount,open_balance
```

## Balance Calculation

Running balance shows:
1. Starting balance (if any)
2. Add bills
3. Subtract payments
4. Subtract credits
5. Ending balance

Open balance shows:
- Unpaid portion of bills
- Unapplied credits

## Notes
- More detailed than summary report
- Shows transaction-level detail
- Running balance for each vendor
- Useful for reconciliation
- Can be filtered by date range
- Includes all AP transactions