# RecurringTransaction

The RecurringTransaction entity represents templates for automatically creating recurring transactions like invoices, bills, or journal entries.

## Operations

### Create
Create a new recurring transaction template.

#### Request
```
POST /v3/company/{companyId}/recurringtransaction
```

#### Request Body
```json
{
  "RecurType": "Reminder",
  "Schedule": {
    "IntervalType": "Monthly",
    "NumInterval": 1,
    "DayOfMonth": "15",
    "NextDate": "2025-02-15",
    "PreviousDate": "2025-01-15"
  },
  "IntuitObject": {
    "Invoice": {
      "CustomerRef": {
        "value": "1"
      },
      "Line": [
        {
          "DetailType": "SalesItemLineDetail",
          "Amount": 500.00,
          "SalesItemLineDetail": {
            "ItemRef": {
              "value": "1"
            }
          }
        }
      ],
      "CustomerMemo": {
        "value": "Monthly service fee"
      }
    }
  }
}
```

#### Response
```json
{
  "RecurringTransaction": {
    "Id": "123",
    "SyncToken": "0",
    "RecurType": "Reminder",
    "Schedule": {
      "IntervalType": "Monthly",
      "NumInterval": 1,
      "DayOfMonth": "15",
      "NextDate": "2025-02-15",
      "PreviousDate": "2025-01-15",
      "MaxOccurrences": "-1",
      "RemindDays": "3",
      "Active": true
    },
    "IntuitObject": {
      "Invoice": {
        "CustomerRef": {
          "value": "1",
          "name": "Amy's Bird Sanctuary"
        },
        "Line": [
          {
            "DetailType": "SalesItemLineDetail",
            "Amount": 500.00,
            "SalesItemLineDetail": {
              "ItemRef": {
                "value": "1",
                "name": "Services"
              }
            }
          }
        ],
        "CustomerMemo": {
          "value": "Monthly service fee"
        }
      }
    },
    "MetaData": {
      "CreateTime": "2025-01-15T10:00:00-08:00",
      "LastUpdatedTime": "2025-01-15T10:00:00-08:00"
    }
  },
  "time": "2025-01-15T10:00:00.000-08:00"
}
```

### Read
Retrieve a recurring transaction by ID.

#### Request
```
GET /v3/company/{companyId}/recurringtransaction/{recurringTransactionId}
```

### Update
Update an existing recurring transaction template.

#### Request
```
POST /v3/company/{companyId}/recurringtransaction
```

Include the full recurring transaction object with `Id` and updated `SyncToken`.

### Delete
Delete a recurring transaction template.

#### Request
```
POST /v3/company/{companyId}/recurringtransaction?operation=delete
```

#### Request Body
```json
{
  "Id": "123",
  "SyncToken": "1"
}
```

### Query
Query recurring transactions with filters.

#### Request
```
GET /v3/company/{companyId}/query?query=select * from RecurringTransaction where Schedule.Active = true
```

## Recurrence Types

- `Scheduled` - Automatically creates transactions
- `Reminder` - Sends reminders to create transactions
- `UnScheduled` - Template only, no automatic creation

## Schedule Configuration

### IntervalType Options
- `Daily`
- `Weekly`
- `Monthly`
- `Yearly`

### Schedule Fields
```json
{
  "Schedule": {
    "IntervalType": "Monthly",
    "NumInterval": 1,
    "DayOfMonth": "15",
    "DayOfWeek": "Monday",
    "WeekOfMonth": "1",
    "MonthOfYear": "1",
    "NextDate": "2025-02-15",
    "PreviousDate": "2025-01-15",
    "StartDate": "2025-01-15",
    "EndDate": "2025-12-31",
    "MaxOccurrences": "12",
    "RemindDays": "3",
    "Active": true
  }
}
```

## Supported Transaction Types

### Invoice
```json
{
  "IntuitObject": {
    "Invoice": {
      "CustomerRef": {
        "value": "1"
      },
      "Line": [
        {
          "DetailType": "SalesItemLineDetail",
          "Amount": 100.00,
          "SalesItemLineDetail": {
            "ItemRef": {
              "value": "1"
            }
          }
        }
      ]
    }
  }
}
```

### Bill
```json
{
  "IntuitObject": {
    "Bill": {
      "VendorRef": {
        "value": "1"
      },
      "Line": [
        {
          "DetailType": "AccountBasedExpenseLineDetail",
          "Amount": 100.00,
          "AccountBasedExpenseLineDetail": {
            "AccountRef": {
              "value": "7"
            }
          }
        }
      ]
    }
  }
}
```

### JournalEntry
```json
{
  "IntuitObject": {
    "JournalEntry": {
      "Line": [
        {
          "DetailType": "JournalEntryLineDetail",
          "Amount": 100.00,
          "JournalEntryLineDetail": {
            "PostingType": "Debit",
            "AccountRef": {
              "value": "1"
            }
          }
        },
        {
          "DetailType": "JournalEntryLineDetail",
          "Amount": 100.00,
          "JournalEntryLineDetail": {
            "PostingType": "Credit",
            "AccountRef": {
              "value": "2"
            }
          }
        }
      ]
    }
  }
}
```

### Other Supported Types
- `Deposit`
- `Transfer`
- `SalesReceipt`
- `RefundReceipt`
- `Purchase`
- `CreditMemo`
- `Estimate`
- `VendorCredit`

## Fields

- `RecurType` (required) - Type of recurrence
- `Schedule` (required) - Schedule configuration
- `IntuitObject` (required) - Transaction template
- `Active` - Whether the recurring transaction is active
- `Name` - Name for the recurring transaction

## Notes
- Scheduled transactions are created automatically based on the schedule
- Reminder transactions require manual creation
- Transaction numbers are automatically incremented
- Dates in the template are adjusted based on the schedule
- Can pause recurring transactions by setting Active to false