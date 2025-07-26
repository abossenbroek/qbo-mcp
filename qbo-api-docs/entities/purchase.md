# Purchase

The Purchase entity represents any expense transaction including cash purchases, checks, and credit card charges.

## Operations

### Create
Create a new purchase transaction.

#### Request
```
POST /v3/company/{companyId}/purchase
```

#### Request Body
```json
{
  "PaymentType": "Cash",
  "AccountRef": {
    "value": "35",
    "name": "Checking"
  },
  "TxnDate": "2025-01-15",
  "EntityRef": {
    "value": "44",
    "name": "Bob's Burger Joint",
    "type": "Vendor"
  },
  "TotalAmt": 52.50,
  "Line": [
    {
      "DetailType": "AccountBasedExpenseLineDetail",
      "Amount": 52.50,
      "AccountBasedExpenseLineDetail": {
        "AccountRef": {
          "value": "13",
          "name": "Meals and Entertainment"
        },
        "BillableStatus": "NotBillable",
        "TaxCodeRef": {
          "value": "NON"
        }
      }
    }
  ]
}
```

#### Response
```json
{
  "Purchase": {
    "AccountRef": {
      "value": "35",
      "name": "Checking"
    },
    "PaymentType": "Cash",
    "EntityRef": {
      "value": "44",
      "name": "Bob's Burger Joint",
      "type": "Vendor"
    },
    "TotalAmt": 52.50,
    "PurchaseEx": {
      "any": []
    },
    "domain": "QBO",
    "sparse": false,
    "Id": "144",
    "SyncToken": "0",
    "MetaData": {
      "CreateTime": "2025-01-15T10:30:00-08:00",
      "LastUpdatedTime": "2025-01-15T10:30:00-08:00"
    },
    "TxnDate": "2025-01-15",
    "CurrencyRef": {
      "value": "USD",
      "name": "United States Dollar"
    },
    "Line": [
      {
        "Id": "1",
        "DetailType": "AccountBasedExpenseLineDetail",
        "Amount": 52.50,
        "AccountBasedExpenseLineDetail": {
          "AccountRef": {
            "value": "13",
            "name": "Meals and Entertainment"
          },
          "BillableStatus": "NotBillable",
          "TaxCodeRef": {
            "value": "NON"
          }
        }
      }
    ]
  },
  "time": "2025-01-15T10:30:00.891-08:00"
}
```

### Read
Retrieve a purchase by ID.

#### Request
```
GET /v3/company/{companyId}/purchase/{purchaseId}
```

### Update
Update an existing purchase.

#### Request
```
POST /v3/company/{companyId}/purchase
```

Include the full purchase object with `Id` and updated `SyncToken`.

### Delete
Delete a purchase.

#### Request
```
POST /v3/company/{companyId}/purchase?operation=delete
```

#### Request Body
```json
{
  "Id": "144",
  "SyncToken": "0"
}
```

### Query
Query purchases with filters.

#### Request
```
GET /v3/company/{companyId}/query?query=select * from Purchase where TxnDate > '2025-01-01'
```

## Payment Types

- `Cash` - Cash purchase
- `Check` - Check payment
- `CreditCard` - Credit card charge

## Line Item Types

### AccountBasedExpenseLineDetail
For categorizing expenses to expense accounts:
```json
{
  "DetailType": "AccountBasedExpenseLineDetail",
  "Amount": 100.00,
  "AccountBasedExpenseLineDetail": {
    "AccountRef": {
      "value": "7"
    },
    "BillableStatus": "Billable",
    "CustomerRef": {
      "value": "1"
    },
    "ClassRef": {
      "value": "5"
    },
    "TaxCodeRef": {
      "value": "NON"
    }
  }
}
```

### ItemBasedExpenseLineDetail
For purchasing inventory items:
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
    "BillableStatus": "NotBillable",
    "TaxCodeRef": {
      "value": "NON"
    }
  }
}
```

## Fields

- `PaymentType` (required) - Type of payment
- `AccountRef` (required) - Account used for payment
- `TxnDate` - Transaction date
- `EntityRef` - Reference to vendor or customer
- `Line` (required) - At least one line item
- `TotalAmt` - Total amount (read-only, calculated)
- `DocNumber` - Reference number
- `PrivateNote` - Internal note
- `Credit` - Boolean indicating if this is a credit
- `TxnTaxDetail` - Tax details for the transaction
- `GlobalTaxCalculation` - Tax calculation method

## Notes
- Purchase can be used for cash, check, or credit card transactions
- For credit purchases from vendors, use Bill entity instead
- Line items can be expense-based or item-based
- Supports billable expenses that can be passed to customers
- Multi-currency purchases supported with ExchangeRate field