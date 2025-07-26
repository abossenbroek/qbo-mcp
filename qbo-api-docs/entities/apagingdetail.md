# Apagingdetail

The information below provides a reference on how to access the AP Aging Detail report from the QuickBooks Online Report Service.

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
    "ReportName": "AgedPayableDetail",
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
    "Time": "2016-03-08T14:34:28-08:00"
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
                  "id": "32",
                  "value": "Cal Telephone"
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
                  "id": "48",
                  "value": "PG&E"
                },
                {
                  "value": "2015-06-24"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "id": "51",
                  "value": "Tim Philip Masonry"
                },
                {
                  "value": "2015-06-24"
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
        "ColType": "vend_name",
        "ColTitle": "Vendor"
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

### shipvia
- **Optional**: String
- Filter by the shipping method as stored in Invoice.ShipMethodRef.Name.
- Supported Values: Any shipping method as sent in the Invoice.ShipMethodRef.Name attribute at Invoice create- or update-time.

### term
- **Optional**: String
- Filters report contents based on term or terms supplied.
- Supported Values: One or more comma separated term IDs as returned in the attribute, Term.Id of the Term object response code.

### end_duedate
- **Optional**: String
- The range of dates over which receivables are due, in the format YYYY-MM-DD. start_duedate must be less than end_duedate. If not specified, all data is returned.

### accounting_method
- **Optional**: String
- The accounting method used in the report. 
- Supported Values: Cash, Accrual

### start_duedate
- **Optional**: String
- The range of dates over which receivables are due, in the format YYYY-MM-DD. start_duedate must be less than end_duedate. If not specified, all data is returned.

### custom1
- **Optional**: String
- Filter by the specified custom field as defined by the CustomField attribute in transaction entities where supported.
- Supported Values: Name of custom field.

### custom2
- **Optional**: String
- Filter by the specified custom field as defined by the CustomField attribute in transaction entities where supported.
- Supported Values: Name of custom field.

### custom3
- **Optional**: String
- Filter by the specified custom field as defined by the CustomField attribute in transaction entities where supported.
- Supported Values: Name of custom field.

### report_date
- **Optional**: String
- Start date to use for the report, in the format YYYY-MM-DD.

### num_periods
- **Optional**: Integer
- The number of periods to be shown in the report.
- Supported Values: A numeric value.

### vendor
- **Optional**: String
- Filters report contents to include information for specified vendors.
- Supported Values: One or more comma separated vendor IDs as returned in the attribute, Vendor.Id, of the Vendor object response code.

### past_due
- **Optional**: Integer
- Filters report contents based on minimum days past due.
- Supported Values: Integer number of days.

### aging_period
- **Optional**: Decimal
- The number of days in the aging period.
- Supported Values: A numeric value.

### columns
- **Optional**: String
- Column types to be shown in the report.