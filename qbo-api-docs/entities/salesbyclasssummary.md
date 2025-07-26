# SalesByClassSummary

The SalesByClassSummary report provides a summary of sales organized by class.

## Operations

### Query
Retrieve sales by class summary report data.

#### Request
```
GET /v3/company/{companyId}/reports/SalesByClassSummary
```

#### Parameters
- `start_date` (string, required): Start date for the report period (YYYY-MM-DD)
- `end_date` (string, required): End date for the report period (YYYY-MM-DD)
- `accounting_method` (string): Accounting method - Cash or Accrual (default: Accrual)
- `summarize_column_by` (string): Summarize columns by Days, Weeks, Months, Quarters, Years, or Total
- `class` (string): Filter by specific class ID

#### Response
```json
{
  "Header": {
    "Time": "2025-01-15T10:30:00-08:00",
    "ReportName": "SalesByClassSummary",
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
        "ColData": [
          {
            "value": "Design income",
            "id": "82"
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
                  "value": "Design",
                  "id": "2"
                },
                {
                  "value": "2350.00"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "Video",
                  "id": "3"
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
                  "value": "Not Specified"
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
              "value": "Total Design income"
            },
            {
              "value": "4100.00"
            }
          ]
        },
        "type": "Section",
        "group": "Account"
      },
      {
        "ColData": [
          {
            "value": "Landscaping Services",
            "id": "45"
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
                  "value": "Installation",
                  "id": "1"
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
                  "value": "Maintenance",
                  "id": "4"
                },
                {
                  "value": "2150.00"
                }
              ],
              "type": "Data"
            }
          ]
        },
        "Summary": {
          "ColData": [
            {
              "value": "Total Landscaping Services"
            },
            {
              "value": "5650.00"
            }
          ]
        },
        "type": "Section",
        "group": "Account"
      },
      {
        "ColData": [
          {
            "value": "Sales of Product Income",
            "id": "79"
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
                  "value": "Installation",
                  "id": "1"
                },
                {
                  "value": "1275.00"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "Not Specified"
                },
                {
                  "value": "750.00"
                }
              ],
              "type": "Data"
            }
          ]
        },
        "Summary": {
          "ColData": [
            {
              "value": "Total Sales of Product Income"
            },
            {
              "value": "2025.00"
            }
          ]
        },
        "type": "Section",
        "group": "Account"
      },
      {
        "Summary": {
          "ColData": [
            {
              "value": "TOTAL"
            },
            {
              "value": "11775.00"
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
- Primary grouping: Income accounts
- Secondary grouping: Classes within each account
- Shows "Not Specified" for transactions without class assignment

### Columns
- Account/Class names
- Total sales amount for the period
- Can be summarized by time periods

## Common Use Cases

### Department Analysis
When classes represent departments:
- Compare revenue by department
- Identify top-performing departments
- Track departmental growth

### Location Analysis
When classes represent locations:
- Compare sales by location
- Identify geographic trends
- Plan inventory by location

### Product Line Analysis
When classes represent product lines:
- Track sales by product category
- Identify best-selling lines
- Plan marketing efforts

## Notes
- Only includes income accounts
- Requires class tracking to be enabled
- "Not Specified" indicates transactions without class assignment
- Can be filtered to specific classes
- Supports both cash and accrual accounting methods
- Useful for segment reporting and analysis