# JournalReportFr

The JournalReportFr entity represents a journal report with French localization in QuickBooks Online.

## Operations

### Query
Retrieve journal report data with French formatting.

#### Request
```
GET /v3/company/{companyId}/reports/JournalReportFr
```

#### Parameters
- `start_date` (string): Start date for the report period (YYYY-MM-DD format)
- `end_date` (string): End date for the report period (YYYY-MM-DD format)
- `accounting_method` (string): Accounting method (Cash or Accrual)
- `summarize_column_by` (string): Column summarization option

#### Response
```json
{
  "Header": {
    "Time": "2025-01-15T10:00:00-08:00",
    "ReportName": "JournalReportFr",
    "StartPeriod": "2025-01-01",
    "EndPeriod": "2025-01-31"
  },
  "Columns": {
    "Column": [
      {
        "ColTitle": "Date",
        "ColType": "Date"
      },
      {
        "ColTitle": "Num Transaction",
        "ColType": "String"
      },
      {
        "ColTitle": "Type",
        "ColType": "String"
      },
      {
        "ColTitle": "Nom",
        "ColType": "String"
      },
      {
        "ColTitle": "Compte",
        "ColType": "String"
      },
      {
        "ColTitle": "Débit",
        "ColType": "Money"
      },
      {
        "ColTitle": "Crédit",
        "ColType": "Money"
      }
    ]
  },
  "Rows": {
    "Row": []
  }
}
```

## Notes
- This report is specifically formatted for French accounting standards
- All monetary values use European number formatting
- Column headers are in French
- Date formats follow DD/MM/YYYY convention