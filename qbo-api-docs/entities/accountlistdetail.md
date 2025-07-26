# Accountlistdetail

The information below provides a reference on how to access the account list detail report from the QuickBooks Online Report Service.

The account list detail report object

The table below lists all possible attributes that can be returned in the report response. Values are not localized unless indicated. Click here to download the latest XSD.

## Attributes

### Header

The report header.

### Rows

Top level container holding information for report rows.

### Columns

Top level container holding information for report columns or subcolumns.

## Sample Object

```json
{
  "Header": {
    "ReportName": "AccountList", 
    "Currency": "USD", 
    "Option": [
      {
        "Name": "NoReportData", 
        "Value": "false"
      }
    ], 
    "Time": "2016-03-08T11:56:36-08:00"
  }, 
  "Rows": {
    "Row": [
      {
        "ColData": [
          {
            "value": "Billable Expense Income"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Design income"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Discounts given"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Fees Billed"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Landscaping Services"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Landscaping Services:Job Materials"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Landscaping Services:Job Materials:Decks and Patios"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Landscaping Services:Job Materials:Fountains and Garden Lighting"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Landscaping Services:Job Materials:Plants and Soil"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Landscaping Services:Job Materials:Sprinklers and Drip Systems"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Landscaping Services:Labor"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Landscaping Services:Labor:Installation"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Landscaping Services:Labor:Maintenance and Repair"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Other Income"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Pest Control Services"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Refunds-Allowances"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Sales of Product Income"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Services"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Shipping Income"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Unapplied Cash Payment Income"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Uncategorized Income"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }
    ]
  }, 
  "Columns": {
    "Column": [
      {
        "ColType": "account_name", 
        "ColTitle": "Account"
      }, 
      {
        "ColType": "account_type", 
        "ColTitle": "Type"
      }
    ]
  }
}
```

## Query

### Query Parameters

- **date_macro** (Optional, String): Predefined report account create date range. Use if you want the report to cover a standard create report date range; otherwise, use start_createdate and end_createdate to cover an explicit report date range.
  - Supported Values: Today, Yesterday, This Week, Last Week, This Week-to-date, Last Week-to-date, Next Week, Next 4 Weeks, This Month, Last Month, This Month-to-date, Last Month-to-date, Next Month, This Fiscal Quarter, Last Fiscal Quarter, This Fiscal Quarter-to-date, Last Fiscal Quarter-to-date, Next Fiscal Quarter, This Fiscal Year, Last Fiscal Year, This Fiscal Year-to-date, Last Fiscal Year-to-date, Next Fiscal Year

- **start_date** (Optional, String): The start date and end date of the report, in the format YYYY-MM-DD. start_date must be less than end_date. Use if you want the report to cover an explicit date range; otherwise, use date_macro to cover a standard report date range.

- **columns** (Optional, String): Column types to be shown in the report.
  - Supported Values: account_name*, account_type*, detail_acc_type, create_date, create_by, detail_acc_type*, last_mod_date, last_mod_by, account_desc*, account_bal*

### Sample Request

```
GET /v3/company/<realmID>/reports/AccountList
```

### Sample Response

```json
{
  "Header": {
    "ReportName": "AccountList", 
    "Currency": "USD", 
    "Option": [
      {
        "Name": "NoReportData", 
        "Value": "false"
      }
    ], 
    "Time": "2016-03-08T11:56:36-08:00"
  }, 
  "Rows": {
    "Row": [
      {
        "ColData": [
          {
            "value": "Billable Expense Income"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Design income"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Discounts given"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Fees Billed"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Landscaping Services"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Landscaping Services:Job Materials"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Landscaping Services:Job Materials:Decks and Patios"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Landscaping Services:Job Materials:Fountains and Garden Lighting"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Landscaping Services:Job Materials:Plants and Soil"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Landscaping Services:Job Materials:Sprinklers and Drip Systems"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Landscaping Services:Labor"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Landscaping Services:Labor:Installation"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Landscaping Services:Labor:Maintenance and Repair"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Other Income"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Pest Control Services"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Refunds-Allowances"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Sales of Product Income"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Services"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Shipping Income"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Unapplied Cash Payment Income"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }, 
      {
        "ColData": [
          {
            "value": "Uncategorized Income"
          }, 
          {
            "value": "Income"
          }
        ], 
        "type": "Data"
      }
    ]
  }, 
  "Columns": {
    "Column": [
      {
        "ColType": "account_name", 
        "ColTitle": "Account"
      }, 
      {
        "ColType": "account_type", 
        "ColTitle": "Type"
      }
    ]
  }
}
```