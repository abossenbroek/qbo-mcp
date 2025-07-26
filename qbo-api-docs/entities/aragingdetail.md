# Aragingdetail

The information below provides a reference on how to access the AR Aging Detail report from the QuickBooks Online Report Service.

## Attributes

### Header

The report header.

### Rows

Top level container holding information for report rows.

### Columns

Top level container holding information for report columns or subcolumns.

## Sample Response

```json
{
  "Header": {
    "ReportName": "AgedReceivableDetail",
    "Currency": "USD",
    "EndPeriod": "2015-06-30",
    "Option": [
      {
        "Name": "report_date",
        "Value": "2015-06-30"
      },
      {
        "Name": "NoReportData",
        "Value": "false"
      }
    ],
    "Time": "2016-03-09T10:16:56-08:00"
  },
  "Rows": {
    "Row": [
      {
        "Header": {
          "ColData": [
            {
              "value": "31 - 60 days past due"
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
                  "id": "8",
                  "value": "Freeman Sporting Goods:0969 Ocean View Road"
                },
                {
                  "value": "2015-05-24"
                }
              ],
              "type": "Data"
            }
          ]
        },
        "type": "Section"
      },
      {
        "Header": {
          "ColData": [
            {
              "value": "Total for 31 - 60 days past due"
            },
            {
              "value": ""
            }
          ]
        },
        "Rows": {},
        "type": "Section"
      },
      {
        "Header": {
          "ColData": [
            {
              "value": "1 - 30 days past due"
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
                  "id": "20",
                  "value": "Red Rock Diner"
                },
                {
                  "value": "2015-05-31"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "id": "1",
                  "value": "Amy's Bird Sanctuary"
                },
                {
                  "value": "2015-06-16"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "id": "16",
                  "value": "Kookies by Kathy"
                },
                {
                  "value": "2015-06-20"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "id": "2",
                  "value": "Bill's Windsurf Shop"
                },
                {
                  "value": "2015-06-21"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "id": "9",
                  "value": "Freeman Sporting Goods:55 Twin Lane"
                },
                {
                  "value": "2015-06-21"
                }
              ],
              "type": "Data"
            }
          ]
        },
        "type": "Section"
      },
      {
        "Header": {
          "ColData": [
            {
              "value": "Total for 1 - 30 days past due"
            },
            {
              "value": ""
            }
          ]
        },
        "type": "Section"
      }
    ]
  },
  "Columns": {
    "Column": [
      {
        "ColType": "cust_name",
        "ColTitle": "Client"
      },
      {
        "ColType": "due_date",
        "ColTitle": "Due Date"
      }
    ]
  }
}
```

## Query Parameters

Query parameters available for the AR Aging Detail report:

- **report_date**: The date as of which the report is run. Format: YYYY-MM-DD
- **aging_period**: The number of days in each aging period (default is 30)
- **num_periods**: Number of aging periods to show
- **customer**: Filter by specific customer ID(s)
- **past_due**: Include only invoices that are past due
- **accounting_method**: Cash or Accrual
- **columns**: Specify which columns to include in the report