# InventoryValuationSummary

The information below provides a reference on how to access the Inventory Valuation Summary report from the QuickBooks Online Report Service.

## The inventory valuation summary report object

The table below lists all possible attributes that can be returned in the report response. Values are not localized unless indicated.

### ATTRIBUTES

#### Header
The report header.

#### Rows
Top level container holding information for report rows.

#### Columns
Top level container holding information for report columns or subcolumns.

## Query a report

### Query Parameters

Customize the information returned in the report by specifying query parameters with the query. Listed below are query parameters available for this report.

#### ATTRIBUTES

##### end_date
* **Optional**
* **Type:** String
* The end date of the report, in the format YYYY-MM-DD. start_date must be less than end_date. Use if you want the report to cover an explicit date range; otherwise, use date_macro to cover a standard report date range. If not specified value of date_macro is used.

##### date_macro
* **Optional**
* **Type:** String
* Predefined date range. Use if you want the report to cover a standard report date range; otherwise, use the start_date and end_date to cover an explicit report date range.
* **Supported Values:** Today, Yesterday, This Week, Last Week, This Week-to-date, Last Week-to-date, Next Week, Next 4 Weeks, This Month, Last Month, This Month-to-date, Last Month-to-date, Next Month, This Fiscal Quarter, Last Fiscal Quarter, This Fiscal Quarter-to-date, Last Fiscal Quarter-to-date, Next Fiscal Quarter, This Fiscal Year, Last Fiscal Year, This Fiscal Year-to-date, Last Fiscal Year-to-date, Next Fiscal Year

##### start_date
* **Optional**
* **Type:** String
* The start date of the report, in the format YYYY-MM-DD. start_date must be less than end_date. Use if you want the report to cover an explicit date range; otherwise, use date_macro to cover a standard report date range. If not specified value of date_macro is used.

##### summarize_column_by
* **Optional**
* **Type:** String
* The criteria by which to group the report results.
* **Supported Values:** Total, Month, Week, Days, Quarter, Year, Customers, Vendors, Classes, Departments, Employees, ProductsAndServices

### Sample Query

This query returns the inventory valuation summary report for this fiscal year-to-date.

### Returns

Returns the report object.

### Request URL

```
GET /v3/company/<realmID>/reports/InventoryValuationSummary?<name>=<value>[&...]
Accept type:application/json
Production Base URL:https://quickbooks.api.intuit.com
Sandbox Base URL:https://sandbox-quickbooks.api.intuit.com
```

### Sample Query

```
BaseURL/v3/company/1386066315/reports/InventoryValuationSummary?date_macro=This Month
```