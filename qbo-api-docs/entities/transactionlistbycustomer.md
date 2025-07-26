# TransactionListByCustomer

The TransactionListByCustomer report provides a list of all transactions grouped by customer.

## Operations

### Query
Retrieve transaction list by customer report data.

#### Request
```
GET /v3/company/{companyId}/reports/TransactionListByCustomer
```

#### Parameters
- `start_date` (string, required): Start date for the report period (YYYY-MM-DD)
- `end_date` (string, required): End date for the report period (YYYY-MM-DD)
- `accounting_method` (string): Accounting method - Cash or Accrual (default: Accrual)
- `customer` (string): Filter by specific customer ID
- `transaction_type` (string): Filter by transaction type (Invoice, Payment, SalesReceipt, CreditMemo, RefundReceipt, Estimate, Statement)
- `ar_paid` (string): Filter by payment status - All, Paid, Unpaid
- `sort_by` (string): Sort by default, date, or amount
- `sort_order` (string): Sort order - ascend or descend

#### Response
```json
{
  "Header": {
    "Time": "2025-01-15T10:30:00-08:00",
    "ReportName": "TransactionListByCustomer",
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
              "value": "Amy's Bird Sanctuary",
              "id": "1"
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
                  "value": "Invoice",
                  "id": "96"
                },
                {
                  "value": "1037"
                },
                {
                  "value": "2025-02-04"
                },
                {
                  "value": "Rock Fountain installation"
                },
                {
                  "value": "Accounts Receivable"
                },
                {
                  "value": "Sales of Product Income"
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
                  "value": "2025-01-07"
                },
                {
                  "value": "Payment",
                  "id": "103"
                },
                {
                  "value": "2145"
                },
                {
                  "value": ""
                },
                {
                  "value": "Payment received - Thank you!"
                },
                {
                  "value": "Undeposited Funds"
                },
                {
                  "value": "Accounts Receivable"
                },
                {
                  "value": "-275.00"
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
                  "value": "Invoice",
                  "id": "97"
                },
                {
                  "value": "1038"
                },
                {
                  "value": "2025-02-14"
                },
                {
                  "value": "Monthly maintenance"
                },
                {
                  "value": "Accounts Receivable"
                },
                {
                  "value": "Landscaping Services"
                },
                {
                  "value": "450.00"
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
                  "value": "2025-01-20"
                },
                {
                  "value": "Sales Receipt",
                  "id": "134"
                },
                {
                  "value": "1015"
                },
                {
                  "value": ""
                },
                {
                  "value": "Garden supplies"
                },
                {
                  "value": "Checking"
                },
                {
                  "value": "-SPLIT-"
                },
                {
                  "value": "125.00"
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
              "value": "Total for Amy's Bird Sanctuary"
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
              "value": "575.00"
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
              "value": "Bill's Windsurf Shop",
              "id": "2"
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
                  "value": "Estimate",
                  "id": "89"
                },
                {
                  "value": "1030"
                },
                {
                  "value": ""
                },
                {
                  "value": "Design proposal"
                },
                {
                  "value": ""
                },
                {
                  "value": "Design income"
                },
                {
                  "value": "650.00"
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
                  "value": "2025-01-10"
                },
                {
                  "value": "Invoice",
                  "id": "98"
                },
                {
                  "value": "1039"
                },
                {
                  "value": "2025-02-09"
                },
                {
                  "value": "Design services - 50% deposit"
                },
                {
                  "value": "Accounts Receivable"
                },
                {
                  "value": "Design income"
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
                  "value": "2025-01-18"
                },
                {
                  "value": "Credit Memo",
                  "id": "101"
                },
                {
                  "value": "CM-100"
                },
                {
                  "value": ""
                },
                {
                  "value": "Design revision credit"
                },
                {
                  "value": "Accounts Receivable"
                },
                {
                  "value": "Design income"
                },
                {
                  "value": "-50.00"
                },
                {
                  "value": "-50.00"
                }
              ],
              "type": "Data"
            }
          ]
        },
        "Summary": {
          "ColData": [
            {
              "value": "Total for Bill's Windsurf Shop"
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
              "value": "925.00"
            },
            {
              "value": "275.00"
            }
          ]
        },
        "type": "Section"
      },
      {
        "Header": {
          "ColData": [
            {
              "value": "Cool Cars",
              "id": "3"
            }
          ]
        },
        "Rows": {
          "Row": [
            {
              "ColData": [
                {
                  "value": "2025-01-12"
                },
                {
                  "value": "Invoice",
                  "id": "99"
                },
                {
                  "value": "1040"
                },
                {
                  "value": "2025-01-26"
                },
                {
                  "value": "Parking lot landscaping"
                },
                {
                  "value": "Accounts Receivable"
                },
                {
                  "value": "-SPLIT-"
                },
                {
                  "value": "1850.00"
                },
                {
                  "value": "1850.00"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "2025-01-25"
                },
                {
                  "value": "Payment",
                  "id": "104"
                },
                {
                  "value": "2146"
                },
                {
                  "value": ""
                },
                {
                  "value": "Partial payment on invoice 1040"
                },
                {
                  "value": "Undeposited Funds"
                },
                {
                  "value": "Accounts Receivable"
                },
                {
                  "value": "-500.00"
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
              "value": "Total for Cool Cars"
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
              "value": "1350.00"
            },
            {
              "value": "1350.00"
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
              "value": "2850.00"
            },
            {
              "value": "2075.00"
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
- Transactions grouped by customer
- Sub-customers shown under parent customers
- Customer totals calculated automatically

### Transaction Types Included
- **Invoice** - Sales on credit (increases balance)
- **Payment** - Customer payments (decreases balance)
- **Sales Receipt** - Cash sales (no AR impact)
- **Credit Memo** - Credits to customer (decreases balance)
- **Refund Receipt** - Cash refunds to customer
- **Estimate** - Quotes (no AR impact)
- **Statement** - Customer statements

### Open Balance
- Shows current amount owed by customer
- Invoices increase balance
- Payments and credits decrease balance
- Sales receipts don't affect AR balance

## Common Use Cases

### Customer Account Review
- See all transactions with a customer
- Verify open balances
- Track payment history

### Collections Management
- Identify overdue invoices
- Review payment patterns
- Prioritize collection efforts

### Customer Statements
- Generate transaction history
- Prepare customer reconciliations
- Support billing inquiries

## Filtering Examples

### Single Customer
```
GET /v3/company/{companyId}/reports/TransactionListByCustomer?customer=1
```

### Unpaid Transactions Only
```
GET /v3/company/{companyId}/reports/TransactionListByCustomer?ar_paid=Unpaid
```

### Specific Transaction Types
```
GET /v3/company/{companyId}/reports/TransactionListByCustomer?transaction_type=Invoice,Payment
```

## Payment Status Options

- `All` - All transactions
- `Paid` - Fully paid transactions
- `Unpaid` - Open/partially paid transactions

## Notes
- Open balance reflects current AR status
- Estimates don't affect AR balance
- Credit memos can be applied to invoices
- Shows both AR and non-AR transactions
- Useful for customer account reconciliation
- Can include sub-customer transactions