# RefundReceipt

The RefundReceipt entity represents a refund to a customer for a returned product or service.

## Operations

### Create
Create a new refund receipt.

#### Request
```
POST /v3/company/{companyId}/refundreceipt
```

#### Request Body
```json
{
  "Line": [
    {
      "DetailType": "SalesItemLineDetail",
      "Amount": 90.00,
      "SalesItemLineDetail": {
        "ItemRef": {
          "value": "1",
          "name": "Services"
        },
        "Qty": 3,
        "UnitPrice": 30,
        "TaxCodeRef": {
          "value": "TAX"
        }
      }
    }
  ],
  "CustomerRef": {
    "value": "1",
    "name": "Amy's Bird Sanctuary"
  },
  "DepositToAccountRef": {
    "value": "35",
    "name": "Checking"
  },
  "TotalAmt": 99.00,
  "TxnDate": "2025-01-15",
  "PaymentMethodRef": {
    "value": "1"
  },
  "PrintStatus": "NeedToPrint",
  "PaymentRefNum": "10264"
}
```

#### Response
```json
{
  "RefundReceipt": {
    "TxnDate": "2025-01-15",
    "domain": "QBO",
    "PrintStatus": "NeedToPrint",
    "TotalAmt": 99.00,
    "Line": [
      {
        "Id": "1",
        "DetailType": "SalesItemLineDetail",
        "Amount": 90.00,
        "SalesItemLineDetail": {
          "Qty": 3,
          "UnitPrice": 30,
          "ItemRef": {
            "value": "1",
            "name": "Services"
          },
          "TaxCodeRef": {
            "value": "TAX"
          }
        }
      },
      {
        "DetailType": "SubTotalLineDetail",
        "Amount": 90.00,
        "SubTotalLineDetail": {}
      }
    ],
    "TxnTaxDetail": {
      "TotalTax": 9.00,
      "TaxLine": [
        {
          "Amount": 9.00,
          "DetailType": "TaxLineDetail",
          "TaxLineDetail": {
            "TaxRateRef": {
              "value": "3"
            },
            "PercentBased": true,
            "TaxPercent": 10,
            "NetAmountTaxable": 90.00
          }
        }
      ]
    },
    "CustomerRef": {
      "value": "1",
      "name": "Amy's Bird Sanctuary"
    },
    "CustomerMemo": {
      "value": "Refund for returned item"
    },
    "SyncToken": "0",
    "PaymentMethodRef": {
      "value": "1"
    },
    "PaymentRefNum": "10264",
    "DepositToAccountRef": {
      "value": "35",
      "name": "Checking"
    },
    "sparse": false,
    "Id": "162",
    "MetaData": {
      "CreateTime": "2025-01-15T10:33:41-08:00",
      "LastUpdatedTime": "2025-01-15T10:33:41-08:00"
    }
  },
  "time": "2025-01-15T10:33:41.287-08:00"
}
```

### Read
Retrieve a refund receipt by ID.

#### Request
```
GET /v3/company/{companyId}/refundreceipt/{refundReceiptId}
```

### Update
Update an existing refund receipt.

#### Request
```
POST /v3/company/{companyId}/refundreceipt
```

Include the full refund receipt object with `Id` and updated `SyncToken`.

### Delete
Delete a refund receipt.

#### Request
```
POST /v3/company/{companyId}/refundreceipt?operation=delete
```

#### Request Body
```json
{
  "Id": "162",
  "SyncToken": "0"
}
```

### Query
Query refund receipts with filters.

#### Request
```
GET /v3/company/{companyId}/query?query=select * from RefundReceipt where TxnDate > '2025-01-01'
```

## Line Item Types

### SalesItemLineDetail
For refunding products or services:
```json
{
  "DetailType": "SalesItemLineDetail",
  "Amount": 150.00,
  "SalesItemLineDetail": {
    "ItemRef": {
      "value": "1"
    },
    "Qty": 5,
    "UnitPrice": 30,
    "TaxCodeRef": {
      "value": "TAX"
    }
  }
}
```

### GroupLineDetail
For refunding bundled items:
```json
{
  "DetailType": "GroupLineDetail",
  "GroupLineDetail": {
    "GroupItemRef": {
      "value": "19"
    },
    "Quantity": 1,
    "Line": [
      {
        "DetailType": "SalesItemLineDetail",
        "Amount": 50.00,
        "SalesItemLineDetail": {
          "ItemRef": {
            "value": "1"
          },
          "Qty": 1
        }
      }
    ]
  }
}
```

### DescriptionOnly
For adding description lines:
```json
{
  "DetailType": "DescriptionOnly",
  "DescriptionLineDetail": {
    "ServiceDate": "2025-01-15"
  },
  "Description": "Refund for services not rendered"
}
```

## Fields

- `CustomerRef` (required) - Reference to the customer
- `Line` (required) - At least one line item
- `TxnDate` - Transaction date
- `DepositToAccountRef` (required) - Account to deposit refund from
- `PaymentMethodRef` - Payment method used
- `PaymentRefNum` - Check or reference number
- `PrintStatus` - Print status (NotSet, NeedToPrint, PrintComplete)
- `CustomerMemo` - Memo visible to customer
- `PrivateNote` - Internal note
- `DocNumber` - Document number
- `TotalAmt` - Total amount (read-only)
- `ApplyTaxAfterDiscount` - Apply tax after discount
- `ExchangeRate` - Currency exchange rate
- `GlobalTaxCalculation` - Tax calculation method

## Linking to Credit Memos

Refund receipts can be linked to credit memos:
```json
{
  "LinkedTxn": [
    {
      "TxnId": "89",
      "TxnType": "CreditMemo"
    }
  ]
}
```

## Notes
- Refund receipts immediately affect the customer balance
- Money is refunded from the specified bank account
- Can be linked to credit memos to apply existing credits
- Supports partial refunds
- Tax is automatically calculated based on items
- Multi-currency refunds supported