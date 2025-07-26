# Transfer

The Transfer entity represents money transfers between accounts.

## Operations

### Create
Create a new transfer.

#### Request
```
POST /v3/company/{companyId}/transfer
```

#### Request Body
```json
{
  "FromAccountRef": {
    "value": "35",
    "name": "Checking"
  },
  "ToAccountRef": {
    "value": "36",
    "name": "Savings"
  },
  "Amount": 1000.00,
  "TxnDate": "2025-01-15",
  "PrivateNote": "Transfer to savings for tax reserve"
}
```

#### Response
```json
{
  "Transfer": {
    "FromAccountRef": {
      "value": "35",
      "name": "Checking"
    },
    "ToAccountRef": {
      "value": "36",
      "name": "Savings"
    },
    "Amount": 1000.00,
    "TxnDate": "2025-01-15",
    "PrivateNote": "Transfer to savings for tax reserve",
    "domain": "QBO",
    "sparse": false,
    "Id": "145",
    "SyncToken": "0",
    "MetaData": {
      "CreateTime": "2025-01-15T10:00:00-08:00",
      "LastUpdatedTime": "2025-01-15T10:00:00-08:00"
    }
  },
  "time": "2025-01-15T10:00:00.000-08:00"
}
```

### Read
Retrieve a transfer by ID.

#### Request
```
GET /v3/company/{companyId}/transfer/{transferId}
```

### Update
Update an existing transfer.

#### Request
```
POST /v3/company/{companyId}/transfer
```

Include the full transfer object with `Id` and updated `SyncToken`.

### Delete
Delete a transfer.

#### Request
```
POST /v3/company/{companyId}/transfer?operation=delete
```

#### Request Body
```json
{
  "Id": "145",
  "SyncToken": "0"
}
```

### Query
Query transfers with filters.

#### Request
```
GET /v3/company/{companyId}/query?query=select * from Transfer where TxnDate > '2025-01-01'
```

## Fields

- `FromAccountRef` (required) - Source account
- `ToAccountRef` (required) - Destination account
- `Amount` (required) - Transfer amount
- `TxnDate` - Transaction date
- `PrivateNote` - Internal note
- `ClassRef` - Class reference (for tracking)
- `DepartmentRef` - Department reference

## Common Transfer Scenarios

### Bank to Bank Transfer
```json
{
  "FromAccountRef": {
    "value": "35"
  },
  "ToAccountRef": {
    "value": "36"
  },
  "Amount": 5000.00,
  "TxnDate": "2025-01-15",
  "PrivateNote": "Monthly savings transfer"
}
```

### Petty Cash Replenishment
```json
{
  "FromAccountRef": {
    "value": "35"
  },
  "ToAccountRef": {
    "value": "37"
  },
  "Amount": 200.00,
  "TxnDate": "2025-01-15",
  "PrivateNote": "Replenish petty cash"
}
```

### Credit Card Payment
For credit card payments from bank:
```json
{
  "FromAccountRef": {
    "value": "35"
  },
  "ToAccountRef": {
    "value": "41"
  },
  "Amount": 1500.00,
  "TxnDate": "2025-01-15",
  "PrivateNote": "Credit card payment"
}
```

### Investment Transfer
```json
{
  "FromAccountRef": {
    "value": "36"
  },
  "ToAccountRef": {
    "value": "38"
  },
  "Amount": 10000.00,
  "TxnDate": "2025-01-15",
  "PrivateNote": "Transfer to investment account"
}
```

## Multi-Currency Transfers

For transfers between accounts in different currencies:
```json
{
  "FromAccountRef": {
    "value": "35"
  },
  "ToAccountRef": {
    "value": "40"
  },
  "Amount": 1000.00,
  "ExchangeRate": 0.85,
  "TxnDate": "2025-01-15",
  "PrivateNote": "USD to EUR transfer"
}
```

## Account Type Restrictions

Valid account types for transfers:
- Bank
- Credit Card
- Other Current Asset
- Other Current Liability

Cannot transfer to/from:
- Income accounts
- Expense accounts
- Accounts Receivable
- Accounts Payable

## Impact on Reports

Transfers affect:
- Bank reconciliation
- Balance sheet
- Cash flow statement
- Account registers

Transfers do NOT affect:
- Profit & Loss
- Income accounts
- Expense accounts

## Notes
- Transfers move money between balance sheet accounts
- No impact on P&L
- Cannot transfer to/from AR or AP accounts
- Multi-currency transfers use exchange rates
- Useful for cash management
- Shows in both account registers