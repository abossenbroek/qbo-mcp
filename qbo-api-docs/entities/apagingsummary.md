# Apagingsummary

The information below provides a reference on how to access the AP Aging summary report from the QuickBooks Online Report Service.

## Attributes

### Header

The report header.

### Rows

Top level container holding information for Aged Receivables report rows.

### Columns

Top level container holding information for report columns or subcolumns.

## Sample Object

```json
{
  "Header": {
    "ReportName": "AgedPayables",
    "Option": [
      {
        "Name": "report_date",
        "Value": "2016-03-08"
      },
      {
        "Name": "NoReportData",
        "Value": "false"
      }
    ],
    "DateMacro": "today",
    "StartPeriod": "2016-03-08",
    "Currency": "USD",
    "EndPeriod": "2016-03-08",
    "Time": "2016-03-08T16:11:49-08:00"
  },
  "Rows": {
    "Row": [
      {
        "ColData": [
          {
            "id": "56",
            "value": "Bob's Burger Joint"
          },
          {
            "value": ""
          },
          {
            "value": ""
          },
          {
            "value": "-46.00"
          },
          {
            "value": ""
          },
          {
            "value": ""
          },
          {
            "value": "-46.00"
          }
        ]
      },
      {
        "ColData": [
          {
            "id": "31",
            "value": "Brosnahan Insurance Agency"
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
            "value": "241.23"
          },
          {
            "value": "241.23"
          }
        ]
      },
      {
        "ColData": [
          {
            "id": "36",
            "value": "Diego's Road Warrior Bodyshop"
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
            "value": "755.00"
          },
          {
            "value": "755.00"
          }
        ]
      },
      {
        "ColData": [
          {
            "id": "46",
            "value": "Norton Lumber and Building Materials"
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
            "value": "205.00"
          },
          {
            "value": "205.00"
          }
        ]
      },
      {
        "ColData": [
          {
            "id": "48",
            "value": "PG&E"
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
            "value": "86.44"
          },
          {
            "value": "86.44"
          }
        ]
      },
      {
        "group": "GrandTotal",
        "type": "Section",
        "Summary": {
          "ColData": [
            {
              "value": "TOTAL"
            },
            {
              "value": "0.00"
            },
            {
              "value": "0.00"
            },
            {
              "value": "-46.00"
            },
            {
              "value": "0.00"
            },
            {
              "value": "1287.67"
            },
            {
              "value": "1241.67"
            }
          ]
        }
      }
    ]
  },
  "Columns": {
    "Column": [
      {
        "ColType": "Vendor",
        "ColTitle": ""
      },
      {
        "ColType": "Money",
        "ColTitle": "Current"
      },
      {
        "ColType": "Money",
        "ColTitle": "1 - 30"
      },
      {
        "ColType": "Money",
        "ColTitle": "31 - 60"
      },
      {
        "ColType": "Money",
        "ColTitle": "61 - 90"
      },
      {
        "ColType": "Money",
        "ColTitle": "91 and over"
      },
      {
        "ColType": "Money",
        "ColTitle": "Total"
      }
    ]
  }
}
```

## Query Parameters

### Query parameters for AP Aging Summary Report

- **report_date**: The date as of which the report is run. Format: YYYY-MM-DD
- **aging_period**: The number of days in each aging period (default is 30)
- **past_due**: Include only invoices that are past due
- **accounting_method**: Cash or Accrual
- **num_periods**: Number of aging periods to show
- **vendor**: Filter by specific vendor ID(s)
- **columns**: Specify which columns to include in the report