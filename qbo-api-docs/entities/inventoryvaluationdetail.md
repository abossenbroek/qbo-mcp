# InventoryValuationDetail

The information below provides a reference on how to access the Inventory Valuation Detail report from the QuickBooks Online Report Service.

## The inventory valuation detail report object

The table below lists all possible attributes that can be returned in the report response. Values are not localized unless indicated.

### ATTRIBUTES

#### Header
The report header.

#### Rows
Top level container holding information for report rows.

#### Columns
Top level container holding information for report columns or subcolumns.

### SAMPLE OBJECT

```json
{
  "Header": {
    "ReportName": "InventoryValuationDetail", 
    "Option": [
      {
        "Name": "NoReportData", 
        "Value": "false"
      }
    ], 
    "DateMacro": "this month", 
    "StartPeriod": "2024-06-01", 
    "Currency": "USD", 
    "EndPeriod": "2024-06-30", 
    "Time": "2024-06-27T08:27:23-07:00"
  }, 
  "Rows": {
    "Row": [
      {
        "Header": {
          "ColData": [
            {
              "id": "1010000081", 
              "value": "Item One"
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
            }
          ]
        }, 
        "Rows": {
          "Row": [
            {
              "ColData": [
                {
                  "value": "2024-06-27"
                }, 
                {
                  "id": "1455000001", 
                  "value": "Inventory Starting Value"
                }, 
                {
                  "value": "START"
                }, 
                {
                  "id": "", 
                  "value": ""
                }, 
                {
                  "value": "10.00"
                }, 
                {
                  "value": "20.00"
                }, 
                {
                  "value": "200.00"
                }, 
                {
                  "value": "10.00"
                }, 
                {
                  "value": "200.00"
                }
              ], 
              "type": "Data"
            }
          ]
        }, 
        "type": "Section", 
        "Summary": {
          "ColData": [
            {
              "value": "Total for Item One"
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
              "value": "10.00"
            }, 
            {
              "value": ""
            }, 
            {
              "value": "200.00"
            }, 
            {
              "value": "10.00"
            }, 
            {
              "value": "200.00"
            }
          ]
        }
      }
    ]
  }, 
  "Columns": {
    "Column": [
      {
        "ColType": "tx_date", 
        "ColTitle": "Date"
      }, 
      {
        "ColType": "txn_type", 
        "ColTitle": "Transaction Type"
      }, 
      {
        "ColType": "doc_num", 
        "ColTitle": "Num"
      }, 
      {
        "ColType": "name", 
        "ColTitle": "Name"
      }, 
      {
        "ColType": "quantity", 
        "ColTitle": "Qty"
      }, 
      {
        "ColType": "rate", 
        "ColTitle": "Rate"
      }, 
      {
        "ColType": "home_amount", 
        "ColTitle": "FIFO Cost"
      }, 
      {
        "ColType": "qty_on_hand", 
        "ColTitle": "Qty On Hand"
      }, 
      {
        "ColType": "home_asset_value", 
        "ColTitle": "Asset Value"
      }
    ]
  }
}
```

## Query a report

### Query Parameters

Customize the information returned in the report by specifying query parameters with the query. Listed below are query parameters available for this report.

#### ATTRIBUTES

##### end_date
* **Optional**
* **Type:** String
* The end date of the report, in the format YYYY-MM-DD. start_date must be less than end_date. Use if you want the report to cover an explicit date range; otherwise, use date_macro to cover a standard report date range. If not specified value of date_macro is used.

##### end_svcdate
* **Optional**
* **Type:** String
* The end date of the report, in the format YYYY-MM-DD. start_date must be less than end_date. Use if you want the report to cover an explicit date range; otherwise, use date_macro to cover a standard report date range. If not specified value of date_macro is used.

##### date_macro
* **Optional**
* **Type:** String
* Predefined date range. Use if you want the report to cover a standard report date range; otherwise, use the start_date and end_date to cover an explicit report date range.
* **Supported Values:** Today, Yesterday, This Week, Last Week, This Week-to-date, Last Week-to-date, Next Week, Next 4 Weeks, This Month, Last Month, This Month-to-date, Last Month-to-date, Next Month, This Fiscal Quarter, Last Fiscal Quarter, This Fiscal Quarter-to-date, Last Fiscal Quarter-to-date, Next Fiscal Quarter, This Fiscal Year, Last Fiscal Year, This Fiscal Year-to-date, Last Fiscal Year-to-date, Next Fiscal Year

##### svcdate_macro
* **Optional**
* **Type:** String
* Predefined date range. Use if you want the report to cover a standard report date range; otherwise, use the start_date and end_date to cover an explicit report date range.
* **Supported Values:** Today, Yesterday, This Week, Last Week, This Week-to-date, Last Week-to-date, Next Week, Next 4 Weeks, This Month, Last Month, This Month-to-date, Last Month-to-date, Next Month, This Fiscal Quarter, Last Fiscal Quarter, This Fiscal Quarter-to-date, Last Fiscal Quarter-to-date, Next Fiscal Quarter, This Fiscal Year, Last Fiscal Year, This Fiscal Year-to-date, Last Fiscal Year-to-date, Next Fiscal Year

##### start_svcdate
* **Optional**
* **Type:** String
* The start date of the report, in the format YYYY-MM-DD. start_date must be less than end_date. Use if you want the report to cover an explicit date range; otherwise, use date_macro to cover a standard report date range. If not specified value of date_macro is used.

##### group_by
* **Optional**
* **Type:** String
* The field in the transaction by which to group results.
* **Supported Values:** Name, Account, Transaction Type, Customer, Vendor, Employee, Location, Payment Method, Day, Week, Month, Quarter, Year, None

##### start_date
* **Optional**
* **Type:** String
* The start date of the report, in the format YYYY-MM-DD. start_date must be less than end_date. Use if you want the report to cover an explicit date range; otherwise, use date_macro to cover a standard report date range. If not specified value of date_macro is used.

##### columns
* **Optional**
* **Type:** String
* Column types to show in the report.
* **Supported Values:** tx_date, txn_id, txn_type, doc_num, name, quantity, rate, home_amount, qty_on_hand, asset_value, create_date, create_by, last_mod_date, last_mod_by, item_sku, memo, exch_rate, account_name, service_date, rate_inventory, qty_on_hand, asset_value_nt, tracking_num

### Sample Query

This query returns get the inventory valuation detail report for this fiscal year-to-date.

### Returns

Returns the report object.

### Request URL

```
GET /v3/company/<realmID>/reports/InventoryValuationDetail?<name>=<value>[&...]
Accept type:application/json
Production Base URL:https://quickbooks.api.intuit.com
Sandbox Base URL:https://sandbox-quickbooks.api.intuit.com
```

### Sample Query

```
BaseURL/v3/company/1386066315/reports/InventoryValuationDetail?date_macro=This Month
```

### Returns

```json
{
  "Header": {
    "ReportName": "InventoryValuationDetail", 
    "Option": [
      {
        "Name": "NoReportData", 
        "Value": "false"
      }
    ], 
    "DateMacro": "this month", 
    "StartPeriod": "2024-06-01", 
    "Currency": "USD", 
    "EndPeriod": "2024-06-30", 
    "Time": "2024-06-27T08:27:23-07:00"
  }, 
  "Rows": {
    "Row": [
      {
        "Header": {
          "ColData": [
            {
              "id": "1010000081", 
              "value": "Item One"
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
            }
          ]
        }, 
        "Rows": {
          "Row": [
            {
              "ColData": [
                {
                  "value": "2024-06-27"
                }, 
                {
                  "id": "1455000001", 
                  "value": "Inventory Starting Value"
                }, 
                {
                  "value": "START"
                }, 
                {
                  "id": "", 
                  "value": ""
                }, 
                {
                  "value": "10.00"
                }, 
                {
                  "value": "20.00"
                }, 
                {
                  "value": "200.00"
                }, 
                {
                  "value": "10.00"
                }, 
                {
                  "value": "200.00"
                }
              ], 
              "type": "Data"
            }
          ]
        }, 
        "type": "Section", 
        "Summary": {
          "ColData": [
            {
              "value": "Total for Item One"
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
              "value": "10.00"
            }, 
            {
              "value": ""
            }, 
            {
              "value": "200.00"
            }, 
            {
              "value": "10.00"
            }, 
            {
              "value": "200.00"
            }
          ]
        }
      }
    ]
  }, 
  "Columns": {
    "Column": [
      {
        "ColType": "tx_date", 
        "ColTitle": "Date"
      }, 
      {
        "ColType": "txn_type", 
        "ColTitle": "Transaction Type"
      }, 
      {
        "ColType": "doc_num", 
        "ColTitle": "Num"
      }, 
      {
        "ColType": "name", 
        "ColTitle": "Name"
      }, 
      {
        "ColType": "quantity", 
        "ColTitle": "Qty"
      }, 
      {
        "ColType": "rate", 
        "ColTitle": "Rate"
      }, 
      {
        "ColType": "home_amount", 
        "ColTitle": "FIFO Cost"
      }, 
      {
        "ColType": "qty_on_hand", 
        "ColTitle": "Qty On Hand"
      }, 
      {
        "ColType": "home_asset_value", 
        "ColTitle": "Asset Value"
      }
    ]
  }
}
```