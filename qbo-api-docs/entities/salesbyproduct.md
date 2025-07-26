# SalesByProduct

The SalesByProduct report provides a summary of sales organized by products and services.

## Operations

### Query
Retrieve sales by product/service report data.

#### Request
```
GET /v3/company/{companyId}/reports/SalesByProduct
```

#### Parameters
- `start_date` (string, required): Start date for the report period (YYYY-MM-DD)
- `end_date` (string, required): End date for the report period (YYYY-MM-DD)
- `accounting_method` (string): Accounting method - Cash or Accrual (default: Accrual)
- `summarize_column_by` (string): Summarize columns by Days, Weeks, Months, Quarters, Years, ProductsAndServices, or Total
- `item` (string): Filter by specific item ID
- `sort_by` (string): Sort by default, qty_sold, or total
- `sort_order` (string): Sort order - ascend or descend

#### Response
```json
{
  "Header": {
    "Time": "2025-01-15T10:30:00-08:00",
    "ReportName": "SalesByProduct",
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
        "ColType": "Item",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "item"
          }
        ]
      },
      {
        "ColTitle": "Quantity",
        "ColType": "Integer",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "qty_sold"
          }
        ]
      },
      {
        "ColTitle": "Amount",
        "ColType": "Money",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "sales_amount"
          }
        ]
      },
      {
        "ColTitle": "% of Sales",
        "ColType": "Percent",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "pct_of_sales"
          }
        ]
      },
      {
        "ColTitle": "Avg Price",
        "ColType": "Money",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "avg_price"
          }
        ]
      },
      {
        "ColTitle": "COGS",
        "ColType": "Money",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "cogs_amount"
          }
        ]
      },
      {
        "ColTitle": "Gross Margin",
        "ColType": "Money",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "gross_margin"
          }
        ]
      },
      {
        "ColTitle": "Gross Margin %",
        "ColType": "Percent",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "gross_margin_pct"
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
            "value": "Concrete",
            "id": "3"
          },
          {
            "value": "0"
          },
          {
            "value": "0.00"
          },
          {
            "value": "0.0%"
          },
          {
            "value": ""
          },
          {
            "value": "0.00"
          },
          {
            "value": "0.00"
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
                  "value": "Concrete Slab",
                  "id": "4"
                },
                {
                  "value": "10"
                },
                {
                  "value": "2500.00"
                },
                {
                  "value": "8.5%"
                },
                {
                  "value": "250.00"
                },
                {
                  "value": "500.00"
                },
                {
                  "value": "2000.00"
                },
                {
                  "value": "80.0%"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "Concrete Installation",
                  "id": "5"
                },
                {
                  "value": "15"
                },
                {
                  "value": "3750.00"
                },
                {
                  "value": "12.7%"
                },
                {
                  "value": "250.00"
                },
                {
                  "value": "0.00"
                },
                {
                  "value": "3750.00"
                },
                {
                  "value": "100.0%"
                }
              ],
              "type": "Data"
            }
          ]
        },
        "Summary": {
          "ColData": [
            {
              "value": "Total Concrete"
            },
            {
              "value": "25"
            },
            {
              "value": "6250.00"
            },
            {
              "value": "21.2%"
            },
            {
              "value": "250.00"
            },
            {
              "value": "500.00"
            },
            {
              "value": "5750.00"
            },
            {
              "value": "92.0%"
            }
          ]
        },
        "type": "Section",
        "group": "ProductCategory"
      },
      {
        "ColData": [
          {
            "value": "Design",
            "id": "2"
          },
          {
            "value": "45"
          },
          {
            "value": "4500.00"
          },
          {
            "value": "15.3%"
          },
          {
            "value": "100.00"
          },
          {
            "value": "0.00"
          },
          {
            "value": "4500.00"
          },
          {
            "value": "100.0%"
          }
        ],
        "type": "Data"
      },
      {
        "ColData": [
          {
            "value": "Fountain",
            "id": "6"
          },
          {
            "value": "0"
          },
          {
            "value": "0.00"
          },
          {
            "value": "0.0%"
          },
          {
            "value": ""
          },
          {
            "value": "0.00"
          },
          {
            "value": "0.00"
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
                  "value": "Fountain Pump",
                  "id": "7"
                },
                {
                  "value": "25"
                },
                {
                  "value": "625.00"
                },
                {
                  "value": "2.1%"
                },
                {
                  "value": "25.00"
                },
                {
                  "value": "250.00"
                },
                {
                  "value": "375.00"
                },
                {
                  "value": "60.0%"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "Rock Fountain",
                  "id": "8"
                },
                {
                  "value": "15"
                },
                {
                  "value": "4125.00"
                },
                {
                  "value": "14.0%"
                },
                {
                  "value": "275.00"
                },
                {
                  "value": "1875.00"
                },
                {
                  "value": "2250.00"
                },
                {
                  "value": "54.5%"
                }
              ],
              "type": "Data"
            }
          ]
        },
        "Summary": {
          "ColData": [
            {
              "value": "Total Fountain"
            },
            {
              "value": "40"
            },
            {
              "value": "4750.00"
            },
            {
              "value": "16.1%"
            },
            {
              "value": "118.75"
            },
            {
              "value": "2125.00"
            },
            {
              "value": "2625.00"
            },
            {
              "value": "55.3%"
            }
          ]
        },
        "type": "Section",
        "group": "ProductCategory"
      },
      {
        "ColData": [
          {
            "value": "Installation",
            "id": "9"
          },
          {
            "value": "75"
          },
          {
            "value": "7500.00"
          },
          {
            "value": "25.4%"
          },
          {
            "value": "100.00"
          },
          {
            "value": "0.00"
          },
          {
            "value": "7500.00"
          },
          {
            "value": "100.0%"
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
            "value": "65"
          },
          {
            "value": "6500.00"
          },
          {
            "value": "22.0%"
          },
          {
            "value": "100.00"
          },
          {
            "value": "0.00"
          },
          {
            "value": "6500.00"
          },
          {
            "value": "100.0%"
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
              "value": "250"
            },
            {
              "value": "29500.00"
            },
            {
              "value": "100.0%"
            },
            {
              "value": ""
            },
            {
              "value": "2625.00"
            },
            {
              "value": "26875.00"
            },
            {
              "value": "91.1%"
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

## Report Metrics

### Key Columns
- **Quantity**: Units sold
- **Amount**: Total sales revenue
- **% of Sales**: Percentage of total sales
- **Avg Price**: Average selling price
- **COGS**: Cost of goods sold
- **Gross Margin**: Sales minus COGS
- **Gross Margin %**: Margin as percentage

### Product Hierarchy
- Parent items show aggregated data
- Sub-items show individual product details
- Categories automatically calculated

## Analysis Options

### By Time Period
```
GET /v3/company/{companyId}/reports/SalesByProduct?summarize_column_by=Months
```

Shows monthly columns for trend analysis.

### Top Products Only
```
GET /v3/company/{companyId}/reports/SalesByProduct?top_n=10
```

Returns only top 10 products by sales.

## Common Use Cases

### Inventory Planning
- Identify fast-moving items
- Plan reorder quantities
- Optimize stock levels

### Pricing Analysis
- Compare average selling prices
- Identify pricing opportunities
- Monitor price trends

### Profitability Analysis
- Calculate gross margins by product
- Identify most profitable items
- Focus on high-margin products

### Sales Mix Analysis
- Understand product contribution
- Plan product promotions
- Optimize product portfolio

## Notes
- Includes both products and services
- Shows hierarchy for bundled items
- COGS only available for inventory items
- Services typically show 100% margin
- Can filter by specific items or categories
- Supports multiple summarization options