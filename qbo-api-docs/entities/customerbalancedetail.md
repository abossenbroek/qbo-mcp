# CustomerBalanceDetail

## Description
The CustomerBalanceDetail report provides detailed balance information for customers in QuickBooks Online. This report shows transaction-level details for each customer's balance, including invoices, payments, credits, and other transactions that affect the customer's balance.

## Attributes

| Name | Type | Required | Description | Notes |
|------|------|----------|-------------|-------|
| ReportName | String | Yes | The name of the report | Fixed value: "CustomerBalanceDetail" |
| start_date | Date | No | Start date for the report period | Format: YYYY-MM-DD |
| end_date | Date | No | End date for the report period | Format: YYYY-MM-DD |
| date_macro | String | No | Predefined date range | Options may include: This Month, Last Month, This Year, etc. |
| customer | String | No | Filter by specific customer ID | Customer ID to filter results |
| summarize_column_by | String | No | Column to summarize by | Common options: Total, Customer, Transaction Type |
| sort_by | String | No | Sort order for results | Options may include: Date, Customer, Amount |
| sort_order | String | No | Sort direction | "ascend" or "descend" |

## Sample JSON Response

```json
{
  "Header": {
    "Time": "2025-01-26T10:30:00-08:00",
    "ReportName": "CustomerBalanceDetail",
    "DateMacro": "This Fiscal Year-to-date",
    "StartPeriod": "2025-01-01",
    "EndPeriod": "2025-01-26",
    "Currency": "USD",
    "Option": [
      {
        "Name": "report_date",
        "Value": "2025-01-26"
      }
    ]
  },
  "Columns": {
    "Column": [
      {
        "ColTitle": "Date",
        "ColType": "Date"
      },
      {
        "ColTitle": "Transaction Type",
        "ColType": "Text"
      },
      {
        "ColTitle": "Num",
        "ColType": "Text"
      },
      {
        "ColTitle": "Due Date",
        "ColType": "Date"
      },
      {
        "ColTitle": "Balance",
        "ColType": "Money"
      },
      {
        "ColTitle": "Total",
        "ColType": "Money"
      }
    ]
  },
  "Rows": {
    "Row": [
      {
        "Header": {
          "ColData": [
            {
              "value": "Customer Name"
            }
          ]
        },
        "Rows": {
          "Row": [
            {
              "ColData": [
                {
                  "value": "2025-01-15"
                },
                {
                  "value": "Invoice"
                },
                {
                  "value": "1001"
                },
                {
                  "value": "2025-02-14"
                },
                {
                  "value": "500.00"
                },
                {
                  "value": "500.00"
                }
              ]
            }
          ]
        }
      }
    ]
  }
}
```

## API Endpoint and Operations

### Read Report
- **Method**: GET
- **Endpoint**: `/v3/company/{companyID}/reports/CustomerBalanceDetail`
- **Query Parameters**: See attributes table above

### Example Request
```
GET https://sandbox-quickbooks.api.intuit.com/v3/company/{companyID}/reports/CustomerBalanceDetail?start_date=2025-01-01&end_date=2025-01-31
```

## Special Notes and Limitations

1. **Date Parameters**: If no date parameters are specified, the report may use default date ranges based on the company's fiscal year settings.

2. **Data Access**: The report only includes data that the authenticated user has permission to access.

3. **Performance**: For companies with large transaction volumes, consider using date filters to limit the data returned and improve performance.

4. **Customer Filter**: Use the customer parameter to retrieve balance details for specific customers rather than all customers.

5. **Currency**: All amounts are returned in the company's home currency unless otherwise specified.

6. **Report Refresh**: Report data may be cached. Check the Header.Time field to verify data freshness.

## Important Note
This documentation is based on typical QuickBooks API report patterns. Please verify the exact parameters and response format with the official QuickBooks Online API documentation at:
https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/customerbalancedetail