# TransactionListByVendor

The TransactionListByVendor report provides a list of all transactions grouped by vendor.

## Operations

### Query
Retrieve transaction list by vendor report data.

#### Request
```
GET /v3/company/{companyId}/reports/TransactionListByVendor
```

#### Parameters
- `start_date` (string, required): Start date for the report period (YYYY-MM-DD)
- `end_date` (string, required): End date for the report period (YYYY-MM-DD)
- `accounting_method` (string): Accounting method - Cash or Accrual (default: Accrual)
- `vendor` (string): Filter by specific vendor ID
- `transaction_type` (string): Filter by transaction type (Bill, BillPayment, Check, CreditCardCredit, Expense, PurchaseOrder, VendorCredit)
- `sort_by` (string): Sort by default, date, or amount
- `sort_order` (string): Sort order - ascend or descend

#### Response
```json
{
  "Header": {
    "Time": "2025-01-15T10:30:00-08:00",
    "ReportName": "TransactionListByVendor",
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
        "ColTitle": "Due Date",
        "ColType": "Date",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "due_date"
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
            "Value": "account"
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
        "ColTitle": "Open Balance",
        "ColType": "Money",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "open_balance"
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
              "value": "Bob's Burger Joint",
              "id": "44"
            }
          ]
        },
        "Rows": {
          "Row": [
            {
              "ColData": [
                {
                  "value": "2025-01-05"
                },
                {
                  "value": "Bill",
                  "id": "152"
                },
                {
                  "value": "2005"
                },
                {
                  "value": "2025-02-04"
                },
                {
                  "value": "Food supplies"
                },
                {
                  "value": "Accounts Payable"
                },
                {
                  "value": "Food Costs"
                },
                {
                  "value": "250.00"
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
                  "value": "2025-01-10"
                },
                {
                  "value": "Expense",
                  "id": "144"
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": "Lunch meeting"
                },
                {
                  "value": "Checking"
                },
                {
                  "value": "Meals and Entertainment"
                },
                {
                  "value": "52.50"
                },
                {
                  "value": ""
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
              "value": ""
            },
            {
              "value": "302.50"
            },
            {
              "value": "250.00"
            }
          ]
        },
        "type": "Section"
      },
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
                  "value": "2025-01-03"
                },
                {
                  "value": "Purchase Order",
                  "id": "154"
                },
                {
                  "value": "1004"
                },
                {
                  "value": ""
                },
                {
                  "value": "Hardware supplies order"
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": "525.00"
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
                  "value": "2025-01-10"
                },
                {
                  "value": "Bill",
                  "id": "156"
                },
                {
                  "value": "203"
                },
                {
                  "value": "2025-02-09"
                },
                {
                  "value": "January supplies"
                },
                {
                  "value": "Accounts Payable"
                },
                {
                  "value": "-SPLIT-"
                },
                {
                  "value": "525.00"
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
                  "value": "2025-01-12"
                },
                {
                  "value": "Bill Payment (Check)",
                  "id": "157"
                },
                {
                  "value": "1045"
                },
                {
                  "value": ""
                },
                {
                  "value": "Payment for Bill #203"
                },
                {
                  "value": "Checking"
                },
                {
                  "value": "Accounts Payable"
                },
                {
                  "value": "-525.00"
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
                  "value": "2025-01-15"
                },
                {
                  "value": "Vendor Credit",
                  "id": "158"
                },
                {
                  "value": "VC-100"
                },
                {
                  "value": ""
                },
                {
                  "value": "Returned defective items"
                },
                {
                  "value": "Accounts Payable"
                },
                {
                  "value": "Supplies"
                },
                {
                  "value": "-75.00"
                },
                {
                  "value": "-75.00"
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
                  "value": "Bill",
                  "id": "159"
                },
                {
                  "value": "567"
                },
                {
                  "value": "2025-01-22"
                },
                {
                  "value": "Lumber for project"
                },
                {
                  "value": "Accounts Payable"
                },
                {
                  "value": "Job Materials"
                },
                {
                  "value": "1250.00"
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
                  "value": "2025-01-20"
                },
                {
                  "value": "Check",
                  "id": "160"
                },
                {
                  "value": "1046"
                },
                {
                  "value": ""
                },
                {
                  "value": "COD lumber purchase"
                },
                {
                  "value": "Checking"
                },
                {
                  "value": "Job Materials"
                },
                {
                  "value": "325.00"
                },
                {
                  "value": ""
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
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": "1575.00"
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
              "value": ""
            },
            {
              "value": "2327.50"
            },
            {
              "value": "1925.00"
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

### Grouping
- Transactions grouped by vendor
- Each vendor section shows all related transactions
- Vendor totals calculated automatically

### Transaction Types Included
- **Bill** - Vendor bills (increases balance)
- **Bill Payment** - Payments on bills (decreases balance)
- **Check** - Direct check payments
- **Expense** - Cash/credit card expenses
- **Purchase Order** - Outstanding orders
- **Vendor Credit** - Credits from vendors (decreases balance)
- **Credit Card Credit** - Credit card refunds

### Open Balance
- Shows current amount owed to vendor
- Bills and expenses increase balance
- Payments and credits decrease balance
- Purchase orders shown for reference (may not affect balance)

## Common Use Cases

### Vendor Account Reconciliation
- Review all transactions with a vendor
- Verify open balances match vendor statements
- Identify missing bills or payments

### Payment Planning
- See all outstanding bills by vendor
- Prioritize payments based on due dates
- Track purchase orders not yet billed

### Vendor Analysis
- Total purchases from each vendor
- Identify top vendors by spend
- Review payment history

## Filtering Examples

### Single Vendor
```
GET /v3/company/{companyId}/reports/TransactionListByVendor?vendor=41
```

### Specific Transaction Types
```
GET /v3/company/{companyId}/reports/TransactionListByVendor?transaction_type=Bill,BillPayment
```

### Date Range
```
GET /v3/company/{companyId}/reports/TransactionListByVendor?start_date=2025-01-01&end_date=2025-01-31
```

## Notes
- Open balance calculated based on report date
- Purchase orders may show open balance if linked to bills
- Vendor credits reduce amount owed
- Split shows -SPLIT- for multi-line transactions
- Useful for vendor statement reconciliation
- Can export for detailed analysis