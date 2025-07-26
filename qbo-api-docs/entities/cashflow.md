# CashFlow

CashFlow is a read-only report resource that provides details of cash flow for a company for a specified date range. By default, the report period is the current fiscal year-to-date.

## The cashflow report object

### Report Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| **StartPeriod** | String | Optional. The start date for the report period in the format YYYY-MM-DD. |
| **EndPeriod** | String | Optional. The end date for the report period in the format YYYY-MM-DD. |
| **SummarizeColumnsBy** | String | Optional. The method by which report columns are organized. Values include: Days, Weeks, Months, Quarters, Years. |

### Report Structure

| Element | Type | Description |
|---------|------|-------------|
| **Columns** | Column | Report column details including column type and values. |
| **ColData** | ColData | Column data containing the values. |
| **Group** | Group | Row groups in the report. |
| **Header** | Header | Report header information including company name, report name, and date range. |
| **Rows** | Row | Report data organized by rows containing the cash flow details. |
| **Summary** | Summary | Report summary information including totals. |

## Operations

### Read a cashflow report

Retrieves the cash flow report for the specified date range.

**Endpoint:** `GET /v3/company/{companyId}/reports/CashFlow`

**Query Parameters:**
- `start_date` - The start date for the report (YYYY-MM-DD format)
- `end_date` - The end date for the report (YYYY-MM-DD format)
- `summarize_column_by` - How to summarize the columns (Days, Weeks, Months, Quarters, Years)

**Example Request:**
```
GET /v3/company/1234/reports/CashFlow?start_date=2024-01-01&end_date=2024-12-31&summarize_column_by=Months
```

**Note:** This is a read-only report endpoint. Create, update, and delete operations are not available for CashFlow reports.