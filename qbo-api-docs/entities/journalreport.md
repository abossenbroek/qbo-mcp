# JournalReport

## Description
The JournalReport entity represents a journal report in QuickBooks Online. This report provides a detailed list of all journal entries within a specified date range, showing debits and credits for each transaction. It's a read-only report entity that retrieves journal entry data in a report format.

## Endpoint
```
GET /v3/company/{realmID}/reports/JournalReport
```

## Base URLs
- **Production**: `https://quickbooks.api.intuit.com`
- **Sandbox**: `https://sandbox-quickbooks.api.intuit.com`

## Query Parameters

| Parameter | Type | Required | Description | Example |
|-----------|------|----------|-------------|---------|
| start_date | Date | No | The start date for the report period | 2025-01-01 |
| end_date | Date | No | The end date for the report period | 2025-12-31 |
| accounting_method | String | No | Accounting method for the report | Cash or Accrual |
| date_macro | String | No | Predefined date range | This Fiscal Year, Last Month, etc. |
| summarize_column_by | String | No | How to group columns | Day, Week, Month, Quarter, Year |
| sort_by | String | No | Sort order for the report | Date |
| sort_order | String | No | Sort direction | ascend or descend |

## Response Structure

### Attributes Table

| Name | Type | Required | Description | Notes |
|------|------|----------|-------------|-------|
| Header | Object | Yes | Report header information | Contains report name, dates, and metadata |
| Columns | Array | Yes | Column definitions for the report | Defines the structure of report data |
| Rows | Array | Yes | Report data rows | Contains the actual journal entry data |
| Summary | Object | No | Report summary information | May include totals and other summary data |

### Sample JSON Response

```json
{
  "Header": {
    "Time": "2025-07-26T12:00:00-07:00",
    "ReportName": "JournalReport",
    "DateMacro": "This Fiscal Year",
    "StartPeriod": "2025-01-01",
    "EndPeriod": "2025-12-31",
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
        "ColTitle": "Name",
        "ColType": "Text"
      },
      {
        "ColTitle": "Memo/Description",
        "ColType": "Text"
      },
      {
        "ColTitle": "Account",
        "ColType": "Text"
      },
      {
        "ColTitle": "Debit",
        "ColType": "Money"
      },
      {
        "ColTitle": "Credit",
        "ColType": "Money"
      }
    ]
  },
  "Rows": {
    "Row": [
      {
        "ColData": [
          {
            "value": "2025-07-15"
          },
          {
            "value": "Journal Entry"
          },
          {
            "value": "JE-1001"
          },
          {
            "value": ""
          },
          {
            "value": "Monthly depreciation"
          },
          {
            "value": "Depreciation Expense"
          },
          {
            "value": "500.00"
          },
          {
            "value": ""
          }
        ]
      },
      {
        "ColData": [
          {
            "value": "2025-07-15"
          },
          {
            "value": "Journal Entry"
          },
          {
            "value": "JE-1001"
          },
          {
            "value": ""
          },
          {
            "value": "Monthly depreciation"
          },
          {
            "value": "Accumulated Depreciation"
          },
          {
            "value": ""
          },
          {
            "value": "500.00"
          }
        ]
      }
    ]
  }
}
```

## Example Request

```bash
curl -X GET "https://quickbooks.api.intuit.com/v3/company/{realmID}/reports/JournalReport?start_date=2025-01-01&end_date=2025-12-31&accounting_method=Accrual" \
  -H "Accept: application/json" \
  -H "Authorization: Bearer {accessToken}"
```

## Special Notes and Limitations

1. **Report Size Limitation**: QuickBooks report endpoints will cap a response at 400,000 cells. If the response exceeds that limit, you'll receive the error message: "Unable to display more data. Please reduce the date range."

2. **Handling Large Reports**: To handle large reports:
   - Reduce the date range in your request
   - Implement a loop that iterates through date ranges
   - Dynamically shrink the range until the error stops appearing
   - Merge the results into a final dataset

3. **Read-Only**: This is a report entity, so it only supports GET operations. You cannot create, update, or delete journal reports directly through this endpoint.

4. **Related Entity**: For creating or modifying journal entries, use the `JournalEntry` entity endpoint instead.

5. **Authentication**: Requires valid OAuth 2.0 access token with appropriate scopes for reading company data.

6. **Rate Limiting**: Subject to QuickBooks Online API rate limits. Consult the official documentation for current limits.

## Related Endpoints
- `/v3/company/{realmID}/journalentry` - For CRUD operations on journal entries
- `/v3/company/{realmID}/reports/TransactionList` - For transaction list reports
- `/v3/company/{realmID}/reports/GeneralLedger` - For general ledger reports