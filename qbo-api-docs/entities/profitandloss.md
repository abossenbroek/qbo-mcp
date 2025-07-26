# ProfitAndLoss

The ProfitAndLoss report (Income Statement) summarizes revenues and expenses for a specific period.

## Operations

### Query
Retrieve profit and loss report data.

#### Request
```
GET /v3/company/{companyId}/reports/ProfitAndLoss
```

#### Parameters
- `start_date` (string, required): Start date for the report period (YYYY-MM-DD)
- `end_date` (string, required): End date for the report period (YYYY-MM-DD)
- `accounting_method` (string): Accounting method - Cash or Accrual (default: Accrual)
- `summarize_column_by` (string): Summarize columns by Days, Weeks, Months, Quarters, Years, Customers, Vendors, Classes, Departments, Employees, ProductsAndServices
- `customer` (string): Filter by specific customer ID
- `vendor` (string): Filter by specific vendor ID
- `class` (string): Filter by specific class ID
- `department` (string): Filter by specific department ID
- `item` (string): Filter by specific item ID

#### Response
```json
{
  "Header": {
    "Time": "2025-01-15T10:30:00-08:00",
    "ReportName": "ProfitAndLoss",
    "ReportBasis": "Accrual",
    "StartPeriod": "2025-01-01",
    "EndPeriod": "2025-01-31",
    "SummarizeColumnsBy": "Total",
    "Currency": "USD",
    "Option": [
      {
        "Name": "AccountingStandard",
        "Value": "GAAP"
      },
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
        "ColType": "Account",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "account"
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
        "Header": {
          "ColData": [
            {
              "value": "Income"
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
                  "value": "Sales of Product Income",
                  "id": "79"
                },
                {
                  "value": "4239.96"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "Services",
                  "id": "1"
                },
                {
                  "value": "3307.50"
                }
              ],
              "type": "Data"
            }
          ]
        },
        "Summary": {
          "ColData": [
            {
              "value": "Total Income"
            },
            {
              "value": "7547.46"
            }
          ]
        },
        "type": "Section",
        "group": "Income"
      },
      {
        "Header": {
          "ColData": [
            {
              "value": "Cost of Goods Sold"
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
                  "value": "Cost of Goods Sold",
                  "id": "80"
                },
                {
                  "value": "2171.06"
                }
              ],
              "type": "Data"
            }
          ]
        },
        "Summary": {
          "ColData": [
            {
              "value": "Total Cost of Goods Sold"
            },
            {
              "value": "2171.06"
            }
          ]
        },
        "type": "Section",
        "group": "COGS"
      },
      {
        "Header": {
          "ColData": [
            {
              "value": "Gross Profit"
            },
            {
              "value": "5376.40"
            }
          ]
        },
        "type": "Section",
        "group": "GrossProfit"
      },
      {
        "Header": {
          "ColData": [
            {
              "value": "Expenses"
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
                  "value": "Advertising",
                  "id": "7"
                },
                {
                  "value": "74.86"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "Automobile",
                  "id": "8"
                },
                {
                  "value": "346.82"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "Bank Charges",
                  "id": "9"
                },
                {
                  "value": "15.00"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "Legal & Professional Fees",
                  "id": "12"
                },
                {
                  "value": "75.00"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "Rent or Lease",
                  "id": "17"
                },
                {
                  "value": "900.00"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "Travel",
                  "id": "18"
                },
                {
                  "value": "228.09"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "Utilities",
                  "id": "19"
                },
                {
                  "value": "239.92"
                }
              ],
              "type": "Data"
            }
          ]
        },
        "Summary": {
          "ColData": [
            {
              "value": "Total Expenses"
            },
            {
              "value": "1879.69"
            }
          ]
        },
        "type": "Section",
        "group": "Expenses"
      },
      {
        "Header": {
          "ColData": [
            {
              "value": "Net Operating Income"
            },
            {
              "value": "3496.71"
            }
          ]
        },
        "type": "Section",
        "group": "NetOperatingIncome"
      },
      {
        "Header": {
          "ColData": [
            {
              "value": "Net Income"
            },
            {
              "value": "3496.71"
            }
          ]
        },
        "type": "Section",
        "group": "NetIncome"
      }
    ]
  }
}
```

## Report Structure

### Income Section
Shows all revenue accounts including:
- Sales of products
- Service income
- Other income

### Cost of Goods Sold (COGS)
Direct costs associated with producing goods sold:
- Material costs
- Direct labor
- Manufacturing overhead

### Gross Profit
Calculated as: Income - COGS

### Expenses Section
Operating expenses including:
- Advertising
- Automobile expenses
- Bank charges
- Insurance
- Legal & Professional fees
- Office expenses
- Rent or lease
- Repairs & Maintenance
- Travel
- Utilities
- Wages
- Other expenses

### Net Income
Final profit/loss calculated as: Gross Profit - Total Expenses

## Notes
- Default accounting method is Accrual
- Can be filtered by various dimensions (customer, vendor, class, department)
- Supports column summarization for trend analysis
- All amounts are in the company's home currency
- Zero balance accounts may be excluded by default