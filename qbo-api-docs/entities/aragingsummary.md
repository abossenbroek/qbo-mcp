# ARAgingSummary

The information below provides a reference on how to access the AR Aging Summary report from the QuickBooks Online Report Service.

## The AR Aging Summary report object

The table below lists all possible attributes that can be returned in the report response. Values are not localized unless indicated. [Click here](https://developer.intuit.com/app/developer/qbo/docs/learn/explore-the-quickbooks-online-api/minor-versions) to download the latest XSD.

### Attributes

- **Header** - The report header.
- **Rows** - Top level container holding information for Aged Receivables report rows.
- **Columns** - Top level container holding information for report columns or subcolumns.

### Sample Object

```json
{
  "Header": {
    "Customer": "4", 
    "ReportName": "AgedReceivables", 
    "Option": [
      {
        "Name": "report_date", 
        "Value": "2015-12-31"
      }, 
      {
        "Name": "NoReportData", 
        "Value": "false"
      }
    ], 
    "DateMacro": "last calendar year", 
    "StartPeriod": "2015-01-01", 
    "Currency": "USD", 
    "EndPeriod": "2015-12-31", 
    "Time": "2016-03-09T09:09:52-08:00"
  }, 
  "Rows": {
    "Row": [
      {
        "ColData": [
          {
            "id": "4", 
            "value": "Jane Litigious"
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
            "value": "37.50"
          }, 
          {
            "value": "37.50"
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
              "value": "0.00"
            }, 
            {
              "value": "0.00"
            }, 
            {
              "value": "37.50"
            }, 
            {
              "value": "37.50"
            }
          ]
        }
      }
    ]
  }, 
  "Columns": {
    "Column": [
      {
        "ColType": "Customer", 
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

## Query a report

### Query Parameters

Customize the information returned in the report by specifying query parameters with the query. Listed below are query parameters available for this report.

#### Parameters

- **customer** (Optional, String) - Filters report contents to include information for specified customers. Supported Values: One or more comma separated customer IDs as returned in the attribute, Customer.Id, of the Customer object response code.

- **qzurl** (Optional, String) - Specifies whether Quick Zoom URL information should be generated for rows in the report. Quick Zoom URL is a hyperlink to another report containing further details about the particular column of data. Supported Values: true, false

- **date_macro** (Optional, String) - Predefined date range. Use if you want the report to cover a standard report date range; otherwise, use the start_date and end_date to cover an explicit report date range. Supported Values: Today, Yesterday, This Week, Last Week, This Week-to-date, Last Week-to-date, Next Week, Next 4 Weeks, This Month, Last Month, This Month-to-date, Last Month-to-date, Next Month, This Fiscal Quarter, Last Fiscal Quarter, This Fiscal Quarter-to-date, Last Fiscal Quarter-to-date, Next Fiscal Quarter, This Fiscal Year, Last Fiscal Year, This Fiscal Year-to-date, Last Fiscal Year-to-date, Next Fiscal Year

- **aging_method** (Optional, String) - The date upon which aging is determined. Supported Values: Report_Date, Current

- **report_date** (Optional, String) - Start date to use for the report, in the format YYYY-MM-DD.

- **sort_order** (Optional, String) - The sort order. Supported Values: ascend, descend

- **department** (Optional, String) - Filters report contents to include information for specified departments if so configured in the company file. Supported Values: One or more comma separated department IDs as returned in the attribute, Department.Id of the Department object response code.

### Sample Query

This query returns last fiscal year aged receivables for customer, Jane Litigious (customer=4).

### Request URL

```
GET /v3/company/<realmID>/reports/AgedReceivables?<name>=<value>[&...]
Accept type: application/json
Production Base URL: https://quickbooks.api.intuit.com
Sandbox Base URL: https://sandbox-quickbooks.api.intuit.com
```

### Sample Query

```
BaseURL/v3/company/1386066315/reports/AgedReceivables?customer=4&date_macro=Last Fiscal Year
```

### Returns

Returns the report object.

## API Reference

- **Endpoint**: `/v3/company/<realmID>/reports/AgedReceivables`
- **Method**: GET
- **Content-Type**: application/json
- **Response**: AR Aging Summary report object