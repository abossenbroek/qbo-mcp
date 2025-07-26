# ChangeDataCapture

The ChangeDataCapture (CDC) operation returns a list of objects that have changed since a specified time. This allows you to synchronize changes efficiently without having to query all objects.

## Overview

Use change data capture to keep your app data in sync with data from your customers' QuickBooks Online company. This synchronization operations let you determine which objects were changed, added, or deleted since a given point in time.

## Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| **entities** | String | **Required**. Comma separated list of entity names to search for changes. Example: "Customer,Invoice,Payment" |
| **changedSince** | DateTime | **Required**. Date and time to search for changes since, in ISO 8601 format (YYYY-MM-DDTHH:MM:SS-HH:MM). |
| **maxResults** | Integer | Optional. Maximum number of objects to return. Used for pagination. |

## Response Structure

| Element | Type | Description |
|---------|------|-------------|
| **CDCResponse** | Object | Response containing arrays of changed entities, each with their change type (Created, Updated, Deleted). |

## Operations

### Query for changed data

Retrieves all entities that have been created, updated, or deleted since the specified timestamp.

**Endpoint:** `GET /v3/company/{companyId}/cdc`

**Query Parameters:**
- `entities` - Comma-separated list of entity types to check for changes
- `changedSince` - ISO 8601 formatted datetime

**Example Request:**
```
GET /v3/company/1234/cdc?entities=Customer,Invoice,Payment&changedSince=2024-01-01T00:00:00-08:00
```

**Example Response Structure:**
```json
{
  "CDCResponse": [
    {
      "QueryResponse": [
        {
          "Customer": [
            {
              "Id": "123",
              "status": "Deleted"
            }
          ],
          "startPosition": 1,
          "maxResults": 100
        },
        {
          "Invoice": [
            {
              "Id": "456",
              "SyncToken": "0",
              "MetaData": {
                "CreateTime": "2024-01-15T10:30:00-08:00",
                "LastUpdatedTime": "2024-01-15T10:30:00-08:00"
              },
              "status": "Created"
              // ... other Invoice fields
            }
          ],
          "startPosition": 1,
          "maxResults": 100
        }
      ]
    }
  ],
  "time": "2024-01-20T14:30:45.123-08:00"
}
```

## Supported Entities

The following entities support change data capture:
- Account
- Bill
- BillPayment
- Budget
- Class
- CreditMemo
- Customer
- Department
- Deposit
- Employee
- Estimate
- Invoice
- Item
- JournalEntry
- Payment
- PaymentMethod
- Purchase
- PurchaseOrder
- RefundReceipt
- SalesReceipt
- TaxAgency
- TaxCode
- TaxRate
- Term
- TimeActivity
- Transfer
- Vendor
- VendorCredit

## Best Practices

1. **Store the timestamp** - After each CDC query, store the timestamp from the response to use as the changedSince parameter in your next query.
2. **Handle pagination** - Use maxResults to limit response size and paginate through large result sets.
3. **Process changes in order** - Process deleted entities before created/updated ones to avoid referential issues.
4. **Regular polling** - Set up regular polling intervals appropriate for your use case (e.g., every 5 minutes, hourly, daily).