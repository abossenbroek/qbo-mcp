# SalesByCustomer

The SalesByCustomer report provides a summary of sales organized by customer.

## Operations

### Query
Retrieve sales by customer report data.

#### Request
```
GET /v3/company/{companyId}/reports/SalesByCustomer
```

#### Parameters
- `start_date` (string, required): Start date for the report period (YYYY-MM-DD)
- `end_date` (string, required): End date for the report period (YYYY-MM-DD)
- `accounting_method` (string): Accounting method - Cash or Accrual (default: Accrual)
- `summarize_column_by` (string): Summarize columns by Days, Weeks, Months, Quarters, Years, Customers, or Total
- `customer` (string): Filter by specific customer ID
- `sort_by` (string): Sort by default or total
- `sort_order` (string): Sort order - ascend or descend

#### Response
```json
{
  "Header": {
    "Time": "2025-01-15T10:30:00-08:00",
    "ReportName": "SalesByCustomer",
    "ReportBasis": "Accrual",
    "StartPeriod": "2025-01-01",
    "EndPeriod": "2025-01-31",
    "SummarizeColumnsBy": "Total",
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
        "ColType": "Customer",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "customer"
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
            "value": "Amy's Bird Sanctuary",
            "id": "1"
          },
          {
            "value": "5785.00"
          }
        ],
        "type": "Data"
      },
      {
        "ColData": [
          {
            "value": "Bill's Windsurf Shop",
            "id": "2"
          },
          {
            "value": "4520.00"
          }
        ],
        "type": "Data"
      },
      {
        "ColData": [
          {
            "value": "Cool Cars",
            "id": "3"
          },
          {
            "value": "3814.00"
          }
        ],
        "type": "Data"
      },
      {
        "ColData": [
          {
            "value": "Diego Rodriguez",
            "id": "4"
          },
          {
            "value": "2395.00"
          }
        ],
        "type": "Data"
      },
      {
        "ColData": [
          {
            "value": "Freeman Sporting Goods:0969 Ocean View Road",
            "id": "5"
          },
          {
            "value": "1817.50"
          }
        ],
        "type": "Data"
      },
      {
        "ColData": [
          {
            "value": "Freeman Sporting Goods:55 Twin Lane",
            "id": "6"
          },
          {
            "value": "1266.00"
          }
        ],
        "type": "Data"
      },
      {
        "ColData": [
          {
            "value": "Geeta Kalapatapu",
            "id": "7"
          },
          {
            "value": "1602.00"
          }
        ],
        "type": "Data"
      },
      {
        "ColData": [
          {
            "value": "Jeff's Jalopies",
            "id": "8"
          },
          {
            "value": "946.00"
          }
        ],
        "type": "Data"
      },
      {
        "ColData": [
          {
            "value": "John Melton",
            "id": "9"
          },
          {
            "value": "737.50"
          }
        ],
        "type": "Data"
      },
      {
        "ColData": [
          {
            "value": "Kate Whelan",
            "id": "10"
          },
          {
            "value": "554.75"
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
              "value": "23437.75"
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

### Customer Information
- Customer name (including sub-customers with colon separator)
- Customer ID for API reference
- Total sales amount for the period

### Sub-customers
- Displayed as "Parent:Sub-customer"
- Each sub-customer listed separately
- Can be filtered by parent or sub-customer

## Detailed Customer Sales Report

For detailed transaction information, add detail parameter:

#### Request
```
GET /v3/company/{companyId}/reports/SalesByCustomer?detail_level=detail
```

This returns individual transactions:
```json
{
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
                  "value": "Invoice"
                },
                {
                  "value": "1037"
                },
                {
                  "value": "Rock Fountain"
                },
                {
                  "value": "275.00"
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
              "value": "5785.00"
            }
          ]
        }
      }
    ]
  }
}
```

## Common Use Cases

### Customer Ranking
- Identify top customers by sales volume
- Calculate customer concentration risk
- Plan customer retention strategies

### Sales Analysis
- Track customer purchase patterns
- Identify growth opportunities
- Monitor customer engagement

### Commission Calculations
- Calculate sales rep commissions by customer
- Track territory performance
- Measure customer acquisition success

## Notes
- Includes all income transactions (invoices, sales receipts)
- Excludes credit memos and refunds from totals
- Sub-customers shown with parent:child notation
- Can be sorted by customer name or total sales
- Supports date range filtering
- Detail level option shows individual transactions