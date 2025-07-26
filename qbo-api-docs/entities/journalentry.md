# JournalEntry

## Entity Description

Journal entries are transactions where you can move money between accounts and force balance your books in specific ways. Use journal entries only if you understand accounting and understand debits and credits well OR if you are following the advice of your accountant.

Journal entries must follow double-entry bookkeeping principles where at least one pair of lines must be a debit and the other a credit. The total of the debit column must equal the total of the credit column.

## Attributes

### Main JournalEntry Object

| Name | Type | Required | Description | Notes |
|------|------|----------|-------------|-------|
| Id | String | Read-only | Unique identifier for this object | Assigned by QuickBooks Online |
| SyncToken | String | Yes (for updates) | Version number of the object | Used for concurrency control |
| DocNumber | String | No | Reference number for the transaction | If not provided, QBO assigns using next-in-sequence |
| TxnDate | Date | Yes | The date of the transaction | Format: YYYY-MM-DD |
| PrivateNote | String | No | Organization-private note about the transaction | Does not appear on transaction records by default |
| Adjustment | Boolean | No | Indicates whether this is an adjustment entry | Default: false |
| Line | Array | Yes | Line items of the journal entry | Must contain at least 2 lines (1 debit, 1 credit) |
| TotalAmt | Decimal | Read-only | Total amount of the transaction | Computed by QuickBooks |
| CurrencyRef | Object | No | Reference to the currency | Required for multi-currency |
| ExchangeRate | Decimal | No | Currency exchange rate | Valid only for multi-currency |
| MetaData | Object | Read-only | Metadata about object creation/updates | Contains CreateTime and LastUpdatedTime |
| HomeTotalAmt | Decimal | Read-only | Total amount in home currency | For multi-currency transactions |

### Line Item (JournalEntryLineDetail)

| Name | Type | Required | Description | Notes |
|------|------|----------|-------------|-------|
| Id | String | No | Line ID | Used for updating specific lines |
| Description | String | No | Line item description | Text description of the entry |
| Amount | Decimal | Yes | The monetary amount | Must be positive value |
| DetailType | String | Yes | Type of line detail | Must be "JournalEntryLineDetail" |
| JournalEntryLineDetail | Object | Yes | Detailed information for the line | Contains PostingType and AccountRef |

### JournalEntryLineDetail Object

| Name | Type | Required | Description | Notes |
|------|------|----------|-------------|-------|
| PostingType | Enum | Yes | Posting type of the line item | Values: "Debit" or "Credit" |
| AccountRef | Object | Yes | Reference to the account | Contains value (ID) and name |
| Entity | Object | No | Reference to a customer or vendor | Required for AR/AP accounts |
| ClassRef | Object | No | Reference to a class | For class tracking |
| DepartmentRef | Object | No | Reference to a department | For location tracking |

## Sample JSON Response

```json
{
  "JournalEntry": {
    "Adjustment": false,
    "domain": "QBO",
    "sparse": false,
    "Id": "1056",
    "SyncToken": "2",
    "MetaData": {
      "CreateTime": "2014-02-07T13:21:51-08:00",
      "LastUpdatedTime": "2014-02-07T13:29:53-08:00"
    },
    "DocNumber": "4",
    "TxnDate": "2014-02-08",
    "CurrencyRef": {
      "value": "USD",
      "name": "United States Dollar"
    },
    "TotalAmt": 504.00,
    "HomeTotalAmt": 504.00,
    "Line": [
      {
        "Id": "0",
        "Description": "Office supplies expense",
        "Amount": 252.00,
        "DetailType": "JournalEntryLineDetail",
        "JournalEntryLineDetail": {
          "PostingType": "Debit",
          "AccountRef": {
            "value": "29",
            "name": "Office Supplies"
          }
        }
      },
      {
        "Id": "1",
        "Description": "Cash payment for supplies",
        "Amount": 252.00,
        "DetailType": "JournalEntryLineDetail",
        "JournalEntryLineDetail": {
          "PostingType": "Credit",
          "AccountRef": {
            "value": "35",
            "name": "Checking"
          }
        }
      }
    ]
  }
}
```

## CRUD Operations

### Create (POST)
**Endpoint:** `POST /v3/company/{companyId}/journalentry`

**Required fields:**
- TxnDate
- Line (array with at least 2 items - one debit and one credit)
- Each line must have Amount, DetailType, and JournalEntryLineDetail

**Example Request Body:**
```json
{
  "TxnDate": "2024-01-15",
  "Line": [
    {
      "Description": "Monthly rent expense",
      "Amount": 1500.00,
      "DetailType": "JournalEntryLineDetail",
      "JournalEntryLineDetail": {
        "PostingType": "Debit",
        "AccountRef": {
          "value": "45"
        }
      }
    },
    {
      "Description": "Monthly rent payment",
      "Amount": 1500.00,
      "DetailType": "JournalEntryLineDetail",
      "JournalEntryLineDetail": {
        "PostingType": "Credit",
        "AccountRef": {
          "value": "35"
        }
      }
    }
  ]
}
```

### Read (GET)
**Endpoint:** `GET /v3/company/{companyId}/journalentry/{journalentryId}`

Returns the full JournalEntry object with all details.

### Update (POST)
**Endpoint:** `POST /v3/company/{companyId}/journalentry`

**Required fields:**
- Id (of existing journal entry)
- SyncToken (from previous read)
- All required fields from create operation

**Note:** You must provide the complete object, not just the fields you want to update.

### Delete (POST)
**Endpoint:** `POST /v3/company/{companyId}/journalentry?operation=delete`

**Request Body:**
```json
{
  "Id": "1056",
  "SyncToken": "2"
}
```

### Query (GET)
**Endpoint:** `GET /v3/company/{companyId}/query?query=SELECT * FROM JournalEntry WHERE TxnDate > '2024-01-01'`

## Special Notes and Limitations

1. **Balance Requirement:** The sum of all debit amounts must equal the sum of all credit amounts. QuickBooks will reject unbalanced entries.

2. **Minimum Lines:** Every journal entry must have at least 2 lines - one debit and one credit.

3. **Negative Amounts:** QuickBooks Online doesn't support negative amounts in journal entries. To represent a negative transaction, swap the PostingType (use Credit instead of Debit or vice versa).

4. **Account Type Restrictions:**
   - Journal entries with Accounts Receivable accounts must include a Customer reference in the Entity field
   - Journal entries with Accounts Payable accounts must include a Vendor reference in the Entity field

5. **SyncToken:** The SyncToken is critical for updates and deletes. It prevents concurrent modifications. Always use the latest SyncToken from a read operation.

6. **DocNumber:** If not provided and Custom Transaction Numbers is "Off", QuickBooks assigns the next sequential number.

7. **Multi-Currency:** When using multi-currency:
   - CurrencyRef must be specified
   - ExchangeRate represents home currency units per 1 foreign currency unit
   - HomeTotalAmt will show the converted amount in home currency

8. **Line Ordering:** Lines can be provided in any order. QuickBooks will display debits before credits in the UI regardless of the order in the API request.

9. **Maximum Lines:** While there's no documented hard limit, very large journal entries (100+ lines) may experience performance issues.

10. **Audit Trail:** All changes to journal entries are tracked in QuickBooks' audit log, including API changes.