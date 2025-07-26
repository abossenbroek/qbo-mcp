# TrialBalance

The TrialBalance report shows the balance of all accounts at a specific date to verify debits equal credits.

## Operations

### Query
Retrieve trial balance report data.

#### Request
```
GET /v3/company/{companyId}/reports/TrialBalance
```

#### Parameters
- `start_date` (string): Start date for the report period (YYYY-MM-DD)
- `end_date` (string): End date for the report period (YYYY-MM-DD)
- `accounting_method` (string): Accounting method - Cash or Accrual (default: Accrual)
- `summarize_column_by` (string): Summarize columns by Days, Weeks, Months, Quarters, Years, or Total

#### Response
```json
{
  "Header": {
    "Time": "2025-01-15T10:30:00-08:00",
    "ReportName": "TrialBalance",
    "StartPeriod": "2025-01-01",
    "EndPeriod": "2025-01-31",
    "Currency": "USD",
    "ReportBasis": "Accrual",
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
        "ColType": "Account",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "account"
          }
        ]
      },
      {
        "ColTitle": "Debit",
        "ColType": "Money",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "debit"
          }
        ]
      },
      {
        "ColTitle": "Credit",
        "ColType": "Money",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "credit"
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
            "value": "Checking",
            "id": "35"
          },
          {
            "value": "15420.00"
          },
          {
            "value": ""
          }
        ],
        "type": "Data",
        "group": "BankAccounts"
      },
      {
        "ColData": [
          {
            "value": "Savings",
            "id": "36"
          },
          {
            "value": "8500.00"
          },
          {
            "value": ""
          }
        ],
        "type": "Data",
        "group": "BankAccounts"
      },
      {
        "ColData": [
          {
            "value": "Accounts Receivable",
            "id": "84"
          },
          {
            "value": "5281.52"
          },
          {
            "value": ""
          }
        ],
        "type": "Data",
        "group": "AccountsReceivable"
      },
      {
        "ColData": [
          {
            "value": "Inventory Asset",
            "id": "81"
          },
          {
            "value": "3500.00"
          },
          {
            "value": ""
          }
        ],
        "type": "Data",
        "group": "OtherCurrentAssets"
      },
      {
        "ColData": [
          {
            "value": "Prepaid Expenses",
            "id": "3"
          },
          {
            "value": "1200.00"
          },
          {
            "value": ""
          }
        ],
        "type": "Data",
        "group": "OtherCurrentAssets"
      },
      {
        "ColData": [
          {
            "value": "Equipment",
            "id": "5"
          },
          {
            "value": "25000.00"
          },
          {
            "value": ""
          }
        ],
        "type": "Data",
        "group": "FixedAssets"
      },
      {
        "ColData": [
          {
            "value": "Accumulated Depreciation",
            "id": "6"
          },
          {
            "value": ""
          },
          {
            "value": "5000.00"
          }
        ],
        "type": "Data",
        "group": "FixedAssets"
      },
      {
        "ColData": [
          {
            "value": "Accounts Payable",
            "id": "33"
          },
          {
            "value": ""
          },
          {
            "value": "1847.67"
          }
        ],
        "type": "Data",
        "group": "AccountsPayable"
      },
      {
        "ColData": [
          {
            "value": "Credit Card",
            "id": "41"
          },
          {
            "value": ""
          },
          {
            "value": "564.32"
          }
        ],
        "type": "Data",
        "group": "CreditCards"
      },
      {
        "ColData": [
          {
            "value": "Sales Tax Payable",
            "id": "25"
          },
          {
            "value": ""
          },
          {
            "value": "425.00"
          }
        ],
        "type": "Data",
        "group": "OtherCurrentLiabilities"
      },
      {
        "ColData": [
          {
            "value": "Loan Payable",
            "id": "43"
          },
          {
            "value": ""
          },
          {
            "value": "10000.00"
          }
        ],
        "type": "Data",
        "group": "LongTermLiabilities"
      },
      {
        "ColData": [
          {
            "value": "Opening Balance Equity",
            "id": "34"
          },
          {
            "value": ""
          },
          {
            "value": "15000.00"
          }
        ],
        "type": "Data",
        "group": "Equity"
      },
      {
        "ColData": [
          {
            "value": "Retained Earnings",
            "id": "2"
          },
          {
            "value": ""
          },
          {
            "value": "8500.00"
          }
        ],
        "type": "Data",
        "group": "Equity"
      },
      {
        "ColData": [
          {
            "value": "Sales of Product Income",
            "id": "79"
          },
          {
            "value": ""
          },
          {
            "value": "14239.96"
          }
        ],
        "type": "Data",
        "group": "Income"
      },
      {
        "ColData": [
          {
            "value": "Services",
            "id": "1"
          },
          {
            "value": ""
          },
          {
            "value": "8307.50"
          }
        ],
        "type": "Data",
        "group": "Income"
      },
      {
        "ColData": [
          {
            "value": "Cost of Goods Sold",
            "id": "80"
          },
          {
            "value": "5171.06"
          },
          {
            "value": ""
          }
        ],
        "type": "Data",
        "group": "CostOfGoodsSold"
      },
      {
        "ColData": [
          {
            "value": "Advertising",
            "id": "7"
          },
          {
            "value": "274.86"
          },
          {
            "value": ""
          }
        ],
        "type": "Data",
        "group": "Expenses"
      },
      {
        "ColData": [
          {
            "value": "Automobile",
            "id": "8"
          },
          {
            "value": "346.82"
          },
          {
            "value": ""
          }
        ],
        "type": "Data",
        "group": "Expenses"
      },
      {
        "ColData": [
          {
            "value": "Bank Charges",
            "id": "9"
          },
          {
            "value": "85.00"
          },
          {
            "value": ""
          }
        ],
        "type": "Data",
        "group": "Expenses"
      },
      {
        "ColData": [
          {
            "value": "Rent or Lease",
            "id": "17"
          },
          {
            "value": "1800.00"
          },
          {
            "value": ""
          }
        ],
        "type": "Data",
        "group": "Expenses"
      },
      {
        "ColData": [
          {
            "value": "Utilities",
            "id": "19"
          },
          {
            "value": "339.92"
          },
          {
            "value": ""
          }
        ],
        "type": "Data",
        "group": "Expenses"
      },
      {
        "Summary": {
          "ColData": [
            {
              "value": "TOTAL"
            },
            {
              "value": "67884.45"
            },
            {
              "value": "67884.45"
            }
          ]
        },
        "type": "Section",
        "group": "Total"
      }
    ]
  }
}
```

## Report Structure

### Account Groups
- **Assets**
  - Bank Accounts
  - Accounts Receivable
  - Other Current Assets
  - Fixed Assets
- **Liabilities**
  - Accounts Payable
  - Credit Cards
  - Other Current Liabilities
  - Long Term Liabilities
- **Equity**
  - Owner's Equity
  - Retained Earnings
- **Income**
  - Sales Income
  - Service Income
  - Other Income
- **Expenses**
  - Cost of Goods Sold
  - Operating Expenses
  - Other Expenses

### Balance Types
- **Debit Balances** (Normal for):
  - Assets
  - Expenses
  - Dividends/Draws
- **Credit Balances** (Normal for):
  - Liabilities
  - Equity
  - Income

## Key Features

### Balance Verification
- Total debits must equal total credits
- Identifies out-of-balance conditions
- Essential for period-end closing

### Account Details
- Shows every account with activity
- Current period balance
- Proper debit/credit classification

## Common Use Cases

### Month-End Close
- Verify books are in balance
- Review account balances
- Identify unusual balances

### Audit Preparation
- Provide account balances
- Support financial statements
- Verify accounting equation

### Error Detection
- Find out-of-balance conditions
- Identify accounts with wrong balance type
- Spot data entry errors

## Related Reports

### With Beginning Balances
Include opening balances:
```
GET /v3/company/{companyId}/reports/TrialBalance?show_beginning_balance=true
```

### By Period
Show multiple periods:
```
GET /v3/company/{companyId}/reports/TrialBalance?summarize_column_by=Months
```

## Notes
- Fundamental accounting report
- Must always balance (debits = credits)
- Shows all accounts with balances
- Basis for financial statements
- Used for audit and review
- Critical for period-end procedures