# CustomerIncome

The information below provides a reference on how to access the Customer Income report from the QuickBooks Online Report Service.

## The customer income report object

The table below lists all possible attributes that can be returned in the report response. Values are not localized unless indicated. Click here to download the latest XSD.

### ATTRIBUTES

**Header**
The report header.
Show child attributes 

**Rows**
Top level container holding information for report rows.
Show child attributes 

**Columns**
Top level container holding information for report columns or subcolumns.
Show child attributes 

### SAMPLE OBJECT

```json
{
  "Header": {
    "Customer": "1", 
    "ReportName": 
      "CustomerIncome", 
    "Option": [
      {
        "Name": "NoReportData", 
        "Value": "false"
      }
    ], 
    "DateMacro": "this calendar 
      year-to-date", 
    "ReportBasis": "Accrual", 
    "StartPeriod": "2016-01-01", 
      
    "Currency": "USD", 
    "EndPeriod": "2016-03-10", 
    "Time": "2016-03-10T09:28:05
      -08:00"
  }, 
  "Rows": {
    "Row": [
      {
        "ColData": [
          {
            "id": "1", 
            "value": "Amy's Bird 
              Sanctuary"
          }, 
          {
            "value": "247.66"
          }, 
          {
            "value": "-96.31"
          }, 
          {
            "value": "151.35"
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
              "value": "247.66"
            }, 
            {
              "value": "-96.31"
            }, 
            {
              "value": "151.35"
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
        "ColTitle": "Income"
      }, 
      {
        "ColType": "Money", 
        "ColTitle": "Expenses"
      }, 
      {
        "ColType": "Money", 
        "ColTitle": "Net Income"
      }
    ]
  }
}
```

## Query a report

### Query Parameters

Customize the information returned in the report by specifying query parameters with the query. Listed below are query parameters available for this report.

### ATTRIBUTES

**customer**
Optional
String
Filters report contents to include information for specified customers. Supported Values: One or more comma separated customer IDs as returned in the attribute, Customer.Id, of the Customer object response code.

**term**
Optional
String
Filters report contents based on term or terms supplied. Supported Values: One or more comma separated term IDs as returned in the attribute, Term.Id of the Term object response code.

**accounting_method**
Optional
String
The accounting method used in the report. Supported Values:Cash, Accrual

**end_date**
Optional
String
The end date of the report, in the format YYYY-MM-DD. start_date must be less than end_date. Use if you want the report to cover an explicit date range; otherwise, use date_macro to cover a standard report date range. If not specified value of date_macro is used

**date_macro**
Optional
String
Predefined date range. Use if you want the report to cover a standard report date range; otherwise, use the start_date and end_date to cover an explicit report date range. Supported Values: Today, Yesterday, This Week, Last Week, This Week-to-date, Last Week-to-date, Next Week, Next 4 Weeks, This Month, Last Month, This Month-to-date, Last Month-to-date, Next Month, This Fiscal Quarter, Last Fiscal Quarter, This Fiscal Quarter-to-date, Last Fiscal Quarter-to-date, Next Fiscal Quarter, This Fiscal Year, Last Fiscal Year, This Fiscal Year-to-date, Last Fiscal Year-to-date, Next Fiscal Year

**class**
Optional
String
Filters report contents to include information for specified classes if so configured in the company file. Supported Values: One or more comma separated class IDs as returned in the attribute, Class.Id, of the Class entity response code.

**sort_order**
Optional
String
The sort order. Supported Values: ascend, descend

**summarize_column_by**
Optional
String
The criteria by which to group the report results. Supported Values: Total, Month, Week, Days, Quarter, Year, Customers, Vendors, Classes, Departments, Employees, ProductsAndServices

**department**
Optional
String
Filters report contents to include information for specified departments if so configured in the company file. Supported Values: One or more comma separated department IDs as returned in the attribute, Department.Id of the Department object response code.

**vendor**
Optional
String
Filters report contents to include information for specified vendors. Supported Values: One or more comma separated vendor IDs as returned in the attribute, Vendor.Id, of the Vendor object response code.

**start_date**
Optional
String
The start date of the report, in the format YYYY-MM-DD. start_date must be less than end_date. Use if you want the report to cover an explicit date range; otherwise, use date_macro to cover a standard report date range. If not specified value of date_macro is used

### Sample Query

This query returns the customer income report for Amy's Bird Sanctuary, (customer=1).

### Returns

Returns the report object.

### Request URL

```
GET /v3/company/<realmID>/reports
  /CustomerIncome?<name>=<value
  >[&...]
Accept type:application/json
Production Base URL:https
  ://quickbooks.api.intuit.com
Sandbox Base URL:https://sandbox
  -quickbooks.api.intuit.com
```

### Sample Query

```
BaseURL/v3/company/1386066315/rep
orts/CustomerIncome?customer=1
```

### Returns

```json
{
  "Header": {
    "Customer": "1", 
    "ReportName": 
      "CustomerIncome", 
    "Option": [
      {
        "Name": "NoReportData", 
        "Value": "false"
      }
    ], 
    "DateMacro": "this calendar 
      year-to-date", 
    "ReportBasis": "Accrual", 
    "StartPeriod": "2016-01-01", 
      
    "Currency": "USD", 
    "EndPeriod": "2016-03-10", 
    "Time": "2016-03-10T09:28:05
      -08:00"
  }, 
  "Rows": {
    "Row": [
      {
        "ColData": [
          {
            "id": "1", 
            "value": "Amy's Bird 
              Sanctuary"
          }, 
          {
            "value": "247.66"
          }, 
          {
            "value": "-96.31"
          }, 
          {
            "value": "151.35"
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
              "value": "247.66"
            }, 
            {
              "value": "-96.31"
            }, 
            {
              "value": "151.35"
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
        "ColTitle": "Income"
      }, 
      {
        "ColType": "Money", 
        "ColTitle": "Expenses"
      }, 
      {
        "ColType": "Money", 
        "ColTitle": "Net Income"
      }
    ]
  }
}
```