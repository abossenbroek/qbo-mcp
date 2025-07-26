# ProfitAndLossDetail

The ProfitAndLossDetail report provides a detailed view of revenues and expenses with transaction-level information.

## Operations

### Query
Retrieve detailed profit and loss report data with transaction details.

#### Request
```
GET /v3/company/{companyId}/reports/ProfitAndLossDetail
```

#### Parameters
- `start_date` (string, required): Start date for the report period (YYYY-MM-DD)
- `end_date` (string, required): End date for the report period (YYYY-MM-DD)
- `accounting_method` (string): Accounting method - Cash or Accrual (default: Accrual)
- `sort_by` (string): Sort by default, name, or total
- `sort_order` (string): Sort order - ascend or descend
- `customer` (string): Filter by specific customer ID
- `vendor` (string): Filter by specific vendor ID
- `class` (string): Filter by specific class ID
- `department` (string): Filter by specific department ID
- `payment_method` (string): Filter by payment method

#### Response
```json
{
  "Header": {
    "Time": "2025-01-15T10:30:00-08:00",
    "ReportName": "ProfitAndLossDetail",
    "ReportBasis": "Accrual",
    "StartPeriod": "2025-01-01",
    "EndPeriod": "2025-01-31",
    "Currency": "USD",
    "Option": [
      {
        "Name": "AccountingStandard",
        "Value": "GAAP"
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
        "ColTitle": "Split",
        "ColType": "String",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "split_acc"
          }
        ]
      },
      {
        "ColTitle": "Amount",
        "ColType": "Money",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "subt_nat_amount"
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
            }
          ]
        },
        "Rows": {
          "Row": [
            {
              "Header": {
                "ColData": [
                  {
                    "value": "Sales of Product Income",
                    "id": "79"
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
                        "value": "Amy's Bird Sanctuary",
                        "id": "1"
                      },
                      {
                        "value": "Rock Fountain"
                      },
                      {
                        "value": "Accounts Receivable",
                        "id": "84"
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
                        "value": "2025-01-07"
                      },
                      {
                        "value": "Sales Receipt",
                        "id": "134"
                      },
                      {
                        "value": "1038"
                      },
                      {
                        "value": "Cool Cars",
                        "id": "3"
                      },
                      {
                        "value": "Pump"
                      },
                      {
                        "value": "Checking",
                        "id": "35"
                      },
                      {
                        "value": "15.00"
                      }
                    ],
                    "type": "Data"
                  }
                ]
              },
              "Summary": {
                "ColData": [
                  {
                    "value": "Total for Sales of Product Income"
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
                    "value": "290.00"
                  }
                ]
              },
              "type": "Section"
            },
            {
              "Header": {
                "ColData": [
                  {
                    "value": "Services",
                    "id": "1"
                  }
                ]
              },
              "Rows": {
                "Row": [
                  {
                    "ColData": [
                      {
                        "value": "2025-01-09"
                      },
                      {
                        "value": "Invoice",
                        "id": "100"
                      },
                      {
                        "value": "1039"
                      },
                      {
                        "value": "Bill's Windsurf Shop",
                        "id": "2"
                      },
                      {
                        "value": "Custom Design"
                      },
                      {
                        "value": "Accounts Receivable",
                        "id": "84"
                      },
                      {
                        "value": "337.50"
                      }
                    ],
                    "type": "Data"
                  }
                ]
              },
              "Summary": {
                "ColData": [
                  {
                    "value": "Total for Services"
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
                    "value": "337.50"
                  }
                ]
              },
              "type": "Section"
            }
          ]
        },
        "Summary": {
          "ColData": [
            {
              "value": "Total Income"
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
              "value": "627.50"
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
            }
          ]
        },
        "Rows": {
          "Row": [
            {
              "Header": {
                "ColData": [
                  {
                    "value": "Cost of Goods Sold",
                    "id": "80"
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
                        "value": "Amy's Bird Sanctuary",
                        "id": "1"
                      },
                      {
                        "value": "Rock Fountain"
                      },
                      {
                        "value": "Accounts Receivable",
                        "id": "84"
                      },
                      {
                        "value": "125.00"
                      }
                    ],
                    "type": "Data"
                  }
                ]
              },
              "Summary": {
                "ColData": [
                  {
                    "value": "Total for Cost of Goods Sold"
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
                    "value": "125.00"
                  }
                ]
              },
              "type": "Section"
            }
          ]
        },
        "Summary": {
          "ColData": [
            {
              "value": "Total Cost of Goods Sold"
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
              "value": "125.00"
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
              "value": "502.50"
            }
          ]
        },
        "type": "Section",
        "group": "GrossProfit"
      }
    ]
  }
}
```

## Report Structure

### Transaction Details
Each row contains:
- `Date` - Transaction date
- `Transaction Type` - Type of transaction (Invoice, Sales Receipt, Bill, etc.)
- `Num` - Document number
- `Name` - Customer or vendor name
- `Memo/Description` - Transaction description
- `Split` - Account used for the other side of the transaction
- `Amount` - Transaction amount

### Report Sections
- **Income**: All revenue transactions grouped by income account
- **Cost of Goods Sold**: Direct cost transactions
- **Gross Profit**: Calculated as Income minus COGS
- **Expenses**: All expense transactions grouped by expense account
- **Net Income**: Final calculation

## Notes
- Provides transaction-level detail for each account
- Includes all transactions that affect the P&L within the date range
- Can be filtered by various dimensions
- Useful for drilling down into summary P&L numbers
- Transaction IDs are included for API reference