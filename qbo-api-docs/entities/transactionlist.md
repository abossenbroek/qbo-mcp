# TransactionList

The TransactionList report provides a list of all transactions within a specified date range.

## Operations

### Query
Retrieve transaction list report data.

#### Request
```
GET /v3/company/{companyId}/reports/TransactionList
```

#### Parameters
- `start_date` (string, required): Start date for the report period (YYYY-MM-DD)
- `end_date` (string, required): End date for the report period (YYYY-MM-DD)
- `accounting_method` (string): Accounting method - Cash or Accrual (default: Accrual)
- `sort_by` (string): Sort by default, date, name, or amount
- `sort_order` (string): Sort order - ascend or descend
- `columns` (string): Comma-separated list of columns to include
- `transaction_type` (string): Filter by transaction type
- `source_account` (string): Filter by source account
- `account` (string): Filter by account
- `customer` (string): Filter by customer ID
- `vendor` (string): Filter by vendor ID
- `employee` (string): Filter by employee ID
- `class` (string): Filter by class ID
- `department` (string): Filter by department ID
- `payment_method` (string): Filter by payment method

#### Response
```json
{
  "Header": {
    "Time": "2025-01-15T10:30:00-08:00",
    "ReportName": "TransactionList",
    "DateMacro": "This Month",
    "ReportBasis": "Accrual",
    "StartPeriod": "2025-01-01",
    "EndPeriod": "2025-01-31",
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
        "ColTitle": "Date",
        "ColType": "Date",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "tx_date"
          }
        ]
      },
      {
        "ColTitle": "Transaction Type",
        "ColType": "String",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "txn_type"
          }
        ]
      },
      {
        "ColTitle": "Num",
        "ColType": "String",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "doc_num"
          }
        ]
      },
      {
        "ColTitle": "Name",
        "ColType": "String",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "name"
          }
        ]
      },
      {
        "ColTitle": "Memo/Description",
        "ColType": "String",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "memo"
          }
        ]
      },
      {
        "ColTitle": "Account",
        "ColType": "String",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "account_name"
          }
        ]
      },
      {
        "ColTitle": "Split",
        "ColType": "String",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "split"
          }
        ]
      },
      {
        "ColTitle": "Amount",
        "ColType": "Money",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "amount"
          }
        ]
      },
      {
        "ColTitle": "Balance",
        "ColType": "Money",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "balance"
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
            "value": "2025-01-05",
            "id": ""
          },
          {
            "value": "Invoice",
            "id": "96"
          },
          {
            "value": "1037"
          },
          {
            "value": "Amy's Bird Sanctuary",
            "id": "1"
          },
          {
            "value": "Rock Fountain installation"
          },
          {
            "value": "Accounts Receivable",
            "id": "84"
          },
          {
            "value": "Sales of Product Income"
          },
          {
            "value": "275.00"
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
            "value": "2025-01-07",
            "id": ""
          },
          {
            "value": "Payment",
            "id": "103"
          },
          {
            "value": "2145"
          },
          {
            "value": "Amy's Bird Sanctuary",
            "id": "1"
          },
          {
            "value": "Payment received - Thank you!"
          },
          {
            "value": "Undeposited Funds",
            "id": "4"
          },
          {
            "value": "Accounts Receivable"
          },
          {
            "value": "275.00"
          },
          {
            "value": "0.00"
          }
        ],
        "type": "Data"
      },
      {
        "ColData": [
          {
            "value": "2025-01-10",
            "id": ""
          },
          {
            "value": "Bill",
            "id": "25"
          },
          {
            "value": "203"
          },
          {
            "value": "Hicks Hardware",
            "id": "41"
          },
          {
            "value": "January supplies"
          },
          {
            "value": "Accounts Payable",
            "id": "33"
          },
          {
            "value": "-SPLIT-"
          },
          {
            "value": "-525.00"
          },
          {
            "value": "-525.00"
          }
        ],
        "type": "Data"
      },
      {
        "ColData": [
          {
            "value": "2025-01-12",
            "id": ""
          },
          {
            "value": "Check",
            "id": "31"
          },
          {
            "value": "1045"
          },
          {
            "value": "Hicks Hardware",
            "id": "41"
          },
          {
            "value": "Payment for Bill #203"
          },
          {
            "value": "Checking",
            "id": "35"
          },
          {
            "value": "Accounts Payable"
          },
          {
            "value": "-525.00"
          },
          {
            "value": "0.00"
          }
        ],
        "type": "Data"
      },
      {
        "ColData": [
          {
            "value": "2025-01-15",
            "id": ""
          },
          {
            "value": "Deposit",
            "id": "37"
          },
          {
            "value": ""
          },
          {
            "value": ""
          },
          {
            "value": "Deposit Undeposited Funds"
          },
          {
            "value": "Checking",
            "id": "35"
          },
          {
            "value": "Undeposited Funds"
          },
          {
            "value": "275.00"
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
            "value": "2025-01-20",
            "id": ""
          },
          {
            "value": "Journal Entry",
            "id": "55"
          },
          {
            "value": "JE-101"
          },
          {
            "value": ""
          },
          {
            "value": "Depreciation expense"
          },
          {
            "value": "Depreciation Expense",
            "id": "126"
          },
          {
            "value": "-SPLIT-"
          },
          {
            "value": "150.00"
          },
          {
            "value": "150.00"
          }
        ],
        "type": "Data"
      }
    ]
  }
}
```

## Transaction Types

Common transaction types include:
- **Invoice** - Customer invoices
- **Payment** - Customer payments
- **Sales Receipt** - Cash sales
- **Credit Memo** - Customer credits
- **Refund Receipt** - Customer refunds
- **Estimate** - Customer quotes
- **Bill** - Vendor bills
- **Bill Payment** - Payments to vendors
- **Check** - Check payments
- **Expense** - Cash/credit card expenses
- **Purchase Order** - Orders to vendors
- **Vendor Credit** - Credits from vendors
- **Credit Card Credit** - Credit card refunds
- **Journal Entry** - Manual journal entries
- **Deposit** - Bank deposits
- **Transfer** - Bank transfers
- **Time Activity** - Time tracking entries

## Column Options

Available columns:
- `tx_date` - Transaction date
- `txn_type` - Transaction type
- `doc_num` - Document number
- `name` - Customer/Vendor name
- `memo` - Memo/Description
- `account_name` - Account name
- `split` - Split account
- `amount` - Transaction amount
- `balance` - Running balance
- `create_by` - Created by user
- `last_mod_by` - Last modified by
- `create_date` - Creation date
- `last_mod_date` - Last modification date
- `class` - Class
- `dept` - Department
- `billable` - Billable status
- `inv_item` - Inventory item
- `qty` - Quantity
- `rate` - Rate/Price

## Filtering Options

### By Transaction Type
```
?transaction_type=Invoice,Payment
```

### By Account
```
?account=35
```

### By Customer
```
?customer=1
```

### By Date Range
```
?start_date=2025-01-01&end_date=2025-01-31
```

## Notes
- Shows all transactions affecting general ledger
- Balance column shows running balance for AR/AP
- Split shows -SPLIT- for multi-line transactions
- Can export to Excel for further analysis
- Useful for reconciliation and audit trails
- Supports custom column selection