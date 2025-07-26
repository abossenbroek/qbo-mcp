# SalesByDepartment

The SalesByDepartment report provides a summary of sales organized by department (location).

## Operations

### Query
Retrieve sales by department report data.

#### Request
```
GET /v3/company/{companyId}/reports/SalesByDepartment
```

#### Parameters
- `start_date` (string, required): Start date for the report period (YYYY-MM-DD)
- `end_date` (string, required): End date for the report period (YYYY-MM-DD)
- `accounting_method` (string): Accounting method - Cash or Accrual (default: Accrual)
- `summarize_column_by` (string): Summarize columns by Days, Weeks, Months, Quarters, Years, Departments, or Total
- `department` (string): Filter by specific department ID

#### Response
```json
{
  "Header": {
    "Time": "2025-01-15T10:30:00-08:00",
    "ReportName": "SalesByDepartment",
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
                  "value": "Garden Center",
                  "id": "1"
                },
                {
                  "value": "2850.00"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "West Branch",
                  "id": "2"
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
              "value": "4600.00"
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
                  "value": "Garden Center",
                  "id": "1"
                },
                {
                  "value": "4500.00"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "East Branch",
                  "id": "3"
                },
                {
                  "value": "2150.00"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "West Branch",
                  "id": "2"
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
              "value": "Total Landscaping Services"
            },
            {
              "value": "8500.00"
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
                  "value": "Garden Center",
                  "id": "1"
                },
                {
                  "value": "3275.00"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "East Branch",
                  "id": "3"
                },
                {
                  "value": "1750.00"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "West Branch",
                  "id": "2"
                },
                {
                  "value": "1125.00"
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
                  "value": "425.00"
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
              "value": "6575.00"
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
              "value": "19675.00"
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
- Secondary grouping: Departments within each account
- Shows "Not Specified" for transactions without department assignment

### Department Hierarchy
- Supports sub-departments
- Sub-departments shown as "Parent:Sub-department"
- Each level tracked separately

## Department Summary View

For a summary by department only:

#### Request
```
GET /v3/company/{companyId}/reports/SalesByDepartment?group_by=Department
```

Returns:
```json
{
  "Rows": {
    "Row": [
      {
        "ColData": [
          {
            "value": "Garden Center",
            "id": "1"
          },
          {
            "value": "10625.00"
          }
        ],
        "type": "Data"
      },
      {
        "ColData": [
          {
            "value": "East Branch",
            "id": "3"
          },
          {
            "value": "3900.00"
          }
        ],
        "type": "Data"
      },
      {
        "ColData": [
          {
            "value": "West Branch",
            "id": "2"
          },
          {
            "value": "4225.00"
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
            "value": "925.00"
          }
        ],
        "type": "Data"
      }
    ]
  }
}
```

## Common Use Cases

### Location Performance
- Compare sales across physical locations
- Identify top-performing branches
- Plan inventory distribution

### Department Analysis
- Track departmental revenue
- Allocate resources based on performance
- Set department-specific goals

### Regional Reporting
- Analyze geographic performance
- Plan expansion strategies
- Monitor regional trends

## Notes
- Requires department/location tracking enabled
- "Not Specified" indicates transactions without department
- Can filter to specific departments
- Supports hierarchical department structures
- Useful for multi-location businesses
- Can be combined with other dimensions (class, customer)