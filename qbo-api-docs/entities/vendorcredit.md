# VendorCredit

The VendorCredit entity represents a credit from a vendor that reduces the amount owed.

## Operations

### Create
Create a new vendor credit.

#### Request
```
POST /v3/company/{companyId}/vendorcredit
```

#### Request Body
```json
{
  "VendorRef": {
    "value": "41",
    "name": "Hicks Hardware"
  },
  "TxnDate": "2025-01-15",
  "Line": [
    {
      "DetailType": "AccountBasedExpenseLineDetail",
      "Amount": 75.00,
      "AccountBasedExpenseLineDetail": {
        "AccountRef": {
          "value": "64",
          "name": "Office Supplies"
        },
        "CustomerRef": {
          "value": "1"
        },
        "BillableStatus": "NotBillable",
        "TaxCodeRef": {
          "value": "NON"
        }
      }
    }
  ],
  "APAccountRef": {
    "value": "33",
    "name": "Accounts Payable"
  },
  "TotalAmt": 75.00,
  "PrivateNote": "Credit for returned office supplies"
}
```

#### Response
```json
{
  "VendorCredit": {
    "VendorRef": {
      "value": "41",
      "name": "Hicks Hardware"
    },
    "TxnDate": "2025-01-15",
    "Line": [
      {
        "Id": "1",
        "DetailType": "AccountBasedExpenseLineDetail",
        "Amount": 75.00,
        "AccountBasedExpenseLineDetail": {
          "AccountRef": {
            "value": "64",
            "name": "Office Supplies"
          },
          "CustomerRef": {
            "value": "1"
          },
          "BillableStatus": "NotBillable",
          "TaxCodeRef": {
            "value": "NON"
          }
        }
      }
    ],
    "APAccountRef": {
      "value": "33",
      "name": "Accounts Payable"
    },
    "TotalAmt": 75.00,
    "Balance": 75.00,
    "PrivateNote": "Credit for returned office supplies",
    "domain": "QBO",
    "sparse": false,
    "Id": "158",
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
Retrieve a vendor credit by ID.

#### Request
```
GET /v3/company/{companyId}/vendorcredit/{vendorCreditId}
```

### Update
Update an existing vendor credit.

#### Request
```
POST /v3/company/{companyId}/vendorcredit
```

Include the full vendor credit object with `Id` and updated `SyncToken`.

### Delete
Delete a vendor credit.

#### Request
```
POST /v3/company/{companyId}/vendorcredit?operation=delete
```

#### Request Body
```json
{
  "Id": "158",
  "SyncToken": "0"
}
```

### Query
Query vendor credits with filters.

#### Request
```
GET /v3/company/{companyId}/query?query=select * from VendorCredit where Balance > '0'
```

## Line Item Types

### AccountBasedExpenseLineDetail
For expense account credits:
```json
{
  "DetailType": "AccountBasedExpenseLineDetail",
  "Amount": 100.00,
  "AccountBasedExpenseLineDetail": {
    "AccountRef": {
      "value": "64"
    },
    "CustomerRef": {
      "value": "1"
    },
    "ClassRef": {
      "value": "5"
    },
    "BillableStatus": "Billable",
    "TaxCodeRef": {
      "value": "NON"
    }
  }
}
```

### ItemBasedExpenseLineDetail
For item-based credits:
```json
{
  "DetailType": "ItemBasedExpenseLineDetail",
  "Amount": 250.00,
  "ItemBasedExpenseLineDetail": {
    "ItemRef": {
      "value": "11"
    },
    "Qty": 5,
    "UnitPrice": 50,
    "CustomerRef": {
      "value": "1"
    },
    "BillableStatus": "NotBillable",
    "TaxCodeRef": {
      "value": "NON"
    }
  }
}
```

## Fields

- `VendorRef` (required) - Reference to the vendor
- `Line` (required) - At least one line item
- `TxnDate` - Transaction date
- `APAccountRef` - Accounts payable account
- `DocNumber` - Document number
- `PrivateNote` - Internal note
- `TotalAmt` - Total credit amount (read-only)
- `Balance` - Unapplied balance (read-only)
- `GlobalTaxCalculation` - Tax calculation method
- `ExchangeRate` - Currency exchange rate

## Applying Credits to Bills

### Link During Bill Payment
```json
{
  "BillPayment": {
    "VendorRef": {
      "value": "41"
    },
    "PayType": "Check",
    "Line": [
      {
        "Amount": 500.00,
        "LinkedTxn": [
          {
            "TxnId": "152",
            "TxnType": "Bill"
          }
        ]
      },
      {
        "Amount": 75.00,
        "LinkedTxn": [
          {
            "TxnId": "158",
            "TxnType": "VendorCredit"
          }
        ]
      }
    ]
  }
}
```

### Apply Credit Directly
```json
{
  "LinkedTxn": [
    {
      "TxnId": "152",
      "TxnType": "Bill"
    }
  ]
}
```

## Common Scenarios

### Return of Goods
```json
{
  "VendorRef": {
    "value": "41"
  },
  "Line": [
    {
      "DetailType": "ItemBasedExpenseLineDetail",
      "Amount": 125.00,
      "ItemBasedExpenseLineDetail": {
        "ItemRef": {
          "value": "11"
        },
        "Qty": 5,
        "UnitPrice": 25
      }
    }
  ],
  "PrivateNote": "Returned defective items - RMA #12345"
}
```

### Price Adjustment
```json
{
  "VendorRef": {
    "value": "41"
  },
  "Line": [
    {
      "DetailType": "AccountBasedExpenseLineDetail",
      "Amount": 50.00,
      "AccountBasedExpenseLineDetail": {
        "AccountRef": {
          "value": "64"
        }
      }
    }
  ],
  "PrivateNote": "Price adjustment per agreement"
}
```

### Volume Rebate
```json
{
  "VendorRef": {
    "value": "41"
  },
  "Line": [
    {
      "DetailType": "AccountBasedExpenseLineDetail",
      "Amount": 250.00,
      "AccountBasedExpenseLineDetail": {
        "AccountRef": {
          "value": "80"
        }
      }
    }
  ],
  "PrivateNote": "Q4 volume rebate"
}
```

## Balance Tracking

- `Balance` field shows unapplied amount
- Automatically updated when applied to bills
- Query for open credits: `Balance > '0'`

## Notes
- Reduces amount owed to vendor
- Can be applied to specific bills
- Balance tracked automatically
- Supports billable expenses
- Can include multiple line items
- Shows in vendor reports