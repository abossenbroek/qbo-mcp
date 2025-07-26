# SalesReceipt

The SalesReceipt entity represents a sales transaction where payment is received immediately at the time of sale.

## Operations

### Create
Create a new sales receipt.

#### Request
```
POST /v3/company/{companyId}/salesreceipt
```

#### Request Body
```json
{
  "Line": [
    {
      "DetailType": "SalesItemLineDetail",
      "Amount": 100.00,
      "SalesItemLineDetail": {
        "ItemRef": {
          "value": "1",
          "name": "Services"
        },
        "Qty": 2,
        "UnitPrice": 50,
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
  "TotalAmt": 110.00,
  "TxnDate": "2025-01-15",
  "PaymentMethodRef": {
    "value": "1",
    "name": "Cash"
  },
  "PaymentRefNum": "10264",
  "BillEmail": {
    "Address": "amy@example.com"
  },
  "CustomerMemo": {
    "value": "Thank you for your purchase!"
  }
}
```

#### Response
```json
{
  "SalesReceipt": {
    "TxnDate": "2025-01-15",
    "domain": "QBO",
    "PrintStatus": "NeedToPrint",
    "EmailStatus": "NotSet",
    "TotalAmt": 110.00,
    "Line": [
      {
        "Id": "1",
        "LineNum": 1,
        "DetailType": "SalesItemLineDetail",
        "Amount": 100.00,
        "SalesItemLineDetail": {
          "ItemRef": {
            "value": "1",
            "name": "Services"
          },
          "Qty": 2,
          "UnitPrice": 50,
          "TaxCodeRef": {
            "value": "TAX"
          }
        }
      },
      {
        "DetailType": "SubTotalLineDetail",
        "Amount": 100.00,
        "SubTotalLineDetail": {}
      }
    ],
    "TxnTaxDetail": {
      "TotalTax": 10.00,
      "TaxLine": [
        {
          "Amount": 10.00,
          "DetailType": "TaxLineDetail",
          "TaxLineDetail": {
            "TaxRateRef": {
              "value": "3"
            },
            "PercentBased": true,
            "TaxPercent": 10,
            "NetAmountTaxable": 100.00
          }
        }
      ]
    },
    "CustomerRef": {
      "value": "1",
      "name": "Amy's Bird Sanctuary"
    },
    "CustomerMemo": {
      "value": "Thank you for your purchase!"
    },
    "BillAddr": {
      "Id": "2",
      "Line1": "4581 Finch St.",
      "City": "Bayshore",
      "CountrySubDivisionCode": "CA",
      "PostalCode": "94326",
      "Lat": "INVALID",
      "Long": "INVALID"
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
    "Id": "11",
    "MetaData": {
      "CreateTime": "2025-01-15T10:33:41-08:00",
      "LastUpdatedTime": "2025-01-15T10:33:41-08:00"
    }
  },
  "time": "2025-01-15T10:33:41.287-08:00"
}
```

### Read
Retrieve a sales receipt by ID.

#### Request
```
GET /v3/company/{companyId}/salesreceipt/{salesReceiptId}
```

### Update
Update an existing sales receipt.

#### Request
```
POST /v3/company/{companyId}/salesreceipt
```

Include the full sales receipt object with `Id` and updated `SyncToken`.

### Delete
Delete a sales receipt.

#### Request
```
POST /v3/company/{companyId}/salesreceipt?operation=delete
```

#### Request Body
```json
{
  "Id": "11",
  "SyncToken": "0"
}
```

### Query
Query sales receipts with filters.

#### Request
```
GET /v3/company/{companyId}/query?query=select * from SalesReceipt where TxnDate > '2025-01-01'
```

### Send Email
Send sales receipt via email.

#### Request
```
POST /v3/company/{companyId}/salesreceipt/{salesReceiptId}/send
```

## Line Item Types

### SalesItemLineDetail
For products and services:
```json
{
  "DetailType": "SalesItemLineDetail",
  "Amount": 150.00,
  "SalesItemLineDetail": {
    "ItemRef": {
      "value": "1"
    },
    "Qty": 3,
    "UnitPrice": 50,
    "TaxCodeRef": {
      "value": "TAX"
    },
    "ServiceDate": "2025-01-15"
  }
}
```

### GroupLineDetail
For bundled items:
```json
{
  "DetailType": "GroupLineDetail",
  "GroupLineDetail": {
    "GroupItemRef": {
      "value": "19"
    },
    "Quantity": 1
  }
}
```

### DescriptionOnly
For informational lines:
```json
{
  "DetailType": "DescriptionOnly",
  "DescriptionLineDetail": {
    "ServiceDate": "2025-01-15"
  },
  "Description": "Installation services included"
}
```

### DiscountLineDetail
For discounts:
```json
{
  "DetailType": "DiscountLineDetail",
  "Amount": 10.00,
  "DiscountLineDetail": {
    "PercentBased": true,
    "DiscountPercent": 10
  }
}
```

## Fields

- `CustomerRef` (required) - Reference to the customer
- `Line` (required) - At least one line item
- `TxnDate` - Transaction date
- `DepositToAccountRef` (required) - Account to deposit payment
- `PaymentMethodRef` - Payment method used
- `PaymentRefNum` - Check or reference number
- `DocNumber` - Sales receipt number
- `CustomerMemo` - Memo visible to customer
- `PrivateNote` - Internal note
- `BillEmail` - Email for sending receipt
- `BillAddr` - Billing address
- `ShipAddr` - Shipping address
- `ShipMethodRef` - Shipping method
- `ShipDate` - Shipping date
- `TrackingNum` - Tracking number
- `PrintStatus` - Print status
- `EmailStatus` - Email status
- `TotalAmt` - Total amount (read-only)
- `ApplyTaxAfterDiscount` - Tax calculation method
- `ExchangeRate` - Currency exchange rate

## Payment Processing

### Credit Card Info
```json
{
  "CreditCardPayment": {
    "CreditChargeInfo": {
      "Type": "Visa",
      "NameOnAcct": "John Doe",
      "CcExpiryMonth": 12,
      "CcExpiryYear": 2025,
      "BillAddrStreet": "123 Main St",
      "PostalCode": "94043"
    }
  }
}
```

## Notes
- Payment received immediately at time of sale
- Affects customer balance immediately
- Money deposited to specified account
- Can be emailed to customer
- Supports multiple payment methods
- Tax automatically calculated
- Can include shipping information