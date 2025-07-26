# PurchaseOrder

The PurchaseOrder entity represents a request to purchase goods or services from a vendor.

## Operations

### Create
Create a new purchase order.

#### Request
```
POST /v3/company/{companyId}/purchaseorder
```

#### Request Body
```json
{
  "Line": [
    {
      "DetailType": "ItemBasedExpenseLineDetail",
      "Amount": 250.00,
      "ItemBasedExpenseLineDetail": {
        "ItemRef": {
          "value": "11",
          "name": "Rock Fountain"
        },
        "Qty": 5,
        "UnitPrice": 50,
        "TaxCodeRef": {
          "value": "TAX"
        }
      }
    }
  ],
  "VendorRef": {
    "value": "41",
    "name": "Hicks Hardware"
  },
  "APAccountRef": {
    "value": "33",
    "name": "Accounts Payable"
  },
  "TotalAmt": 275.00,
  "ShipAddr": {
    "Line1": "123 Main Street",
    "City": "Mountain View",
    "CountrySubDivisionCode": "CA",
    "PostalCode": "94043",
    "Country": "USA"
  },
  "TxnDate": "2025-01-15",
  "DueDate": "2025-02-14"
}
```

#### Response
```json
{
  "PurchaseOrder": {
    "domain": "QBO",
    "sparse": false,
    "Id": "154",
    "SyncToken": "0",
    "MetaData": {
      "CreateTime": "2025-01-15T10:45:00-08:00",
      "LastUpdatedTime": "2025-01-15T10:45:00-08:00"
    },
    "DocNumber": "1004",
    "TxnDate": "2025-01-15",
    "CurrencyRef": {
      "value": "USD",
      "name": "United States Dollar"
    },
    "Line": [
      {
        "Id": "1",
        "DetailType": "ItemBasedExpenseLineDetail",
        "Amount": 250.00,
        "ItemBasedExpenseLineDetail": {
          "ItemRef": {
            "value": "11",
            "name": "Rock Fountain"
          },
          "Qty": 5,
          "UnitPrice": 50,
          "BillableStatus": "NotBillable",
          "TaxCodeRef": {
            "value": "TAX"
          }
        }
      },
      {
        "DetailType": "SubTotalLineDetail",
        "Amount": 250.00,
        "SubTotalLineDetail": {}
      }
    ],
    "TxnTaxDetail": {
      "TotalTax": 25.00,
      "TaxLine": [
        {
          "Amount": 25.00,
          "DetailType": "TaxLineDetail",
          "TaxLineDetail": {
            "TaxRateRef": {
              "value": "3"
            },
            "PercentBased": true,
            "TaxPercent": 10,
            "NetAmountTaxable": 250.00
          }
        }
      ]
    },
    "VendorRef": {
      "value": "41",
      "name": "Hicks Hardware"
    },
    "APAccountRef": {
      "value": "33",
      "name": "Accounts Payable"
    },
    "TotalAmt": 275.00,
    "DueDate": "2025-02-14",
    "POStatus": "Open",
    "GlobalTaxCalculation": "TaxExcluded"
  },
  "time": "2025-01-15T10:45:00.891-08:00"
}
```

### Read
Retrieve a purchase order by ID.

#### Request
```
GET /v3/company/{companyId}/purchaseorder/{purchaseOrderId}
```

### Update
Update an existing purchase order.

#### Request
```
POST /v3/company/{companyId}/purchaseorder
```

Include the full purchase order object with `Id` and updated `SyncToken`.

### Delete
Delete a purchase order.

#### Request
```
POST /v3/company/{companyId}/purchaseorder?operation=delete
```

#### Request Body
```json
{
  "Id": "154",
  "SyncToken": "0"
}
```

### Query
Query purchase orders with filters.

#### Request
```
GET /v3/company/{companyId}/query?query=select * from PurchaseOrder where POStatus = 'Open'
```

## Status Values

- `Open` - Purchase order is open
- `Closed` - Purchase order is closed

## Line Item Types

### ItemBasedExpenseLineDetail
For ordering inventory items:
```json
{
  "DetailType": "ItemBasedExpenseLineDetail",
  "Amount": 500.00,
  "ItemBasedExpenseLineDetail": {
    "ItemRef": {
      "value": "11"
    },
    "Qty": 10,
    "UnitPrice": 50,
    "CustomerRef": {
      "value": "1"
    },
    "BillableStatus": "Billable",
    "TaxCodeRef": {
      "value": "TAX"
    }
  }
}
```

### AccountBasedExpenseLineDetail
For ordering services or non-inventory items:
```json
{
  "DetailType": "AccountBasedExpenseLineDetail",
  "Amount": 150.00,
  "AccountBasedExpenseLineDetail": {
    "AccountRef": {
      "value": "64"
    },
    "CustomerRef": {
      "value": "1"
    },
    "BillableStatus": "Billable",
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
- `DueDate` - Expected delivery date
- `DocNumber` - Purchase order number
- `POStatus` - Status of the purchase order
- `APAccountRef` - Accounts payable account
- `ShipAddr` - Shipping address
- `ShipMethodRef` - Shipping method
- `POEmail` - Email for sending PO
- `Memo` - Memo visible to vendor
- `PrivateNote` - Internal note
- `VendorAddr` - Vendor address
- `TotalAmt` - Total amount (read-only)
- `TxnTaxDetail` - Tax details
- `GlobalTaxCalculation` - Tax calculation method

## Linking to Bills

Purchase orders can be linked to bills when goods are received:
```json
{
  "LinkedTxn": [
    {
      "TxnId": "154",
      "TxnType": "PurchaseOrder"
    }
  ]
}
```

## Notes
- Purchase orders don't affect accounting until converted to bills
- Can be partially or fully received
- Supports drop shipping with ShipToCustomer option
- Can track billable expenses for customers
- Multi-currency supported with ExchangeRate field