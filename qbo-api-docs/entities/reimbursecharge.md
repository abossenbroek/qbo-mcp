# ReimburseCharge

The ReimburseCharge entity represents a billable expense charge that can be passed to a customer for reimbursement.

## Operations

### Create
Create a new reimbursable charge.

#### Request
```
POST /v3/company/{companyId}/reimbursecharge
```

#### Request Body
```json
{
  "Amount": 125.00,
  "CustomerRef": {
    "value": "1",
    "name": "Amy's Bird Sanctuary"
  },
  "VendorRef": {
    "value": "41",
    "name": "Hicks Hardware"
  },
  "ItemRef": {
    "value": "11",
    "name": "Rock Fountain"
  },
  "TxnDate": "2025-01-15",
  "HasBeenInvoiced": false,
  "QtyOnHand": 1,
  "UnitPrice": 125.00,
  "PrivateNote": "Customer requested special order",
  "Description": "Special order rock fountain for customer"
}
```

#### Response
```json
{
  "ReimburseCharge": {
    "Id": "145",
    "SyncToken": "0",
    "Amount": 125.00,
    "CustomerRef": {
      "value": "1",
      "name": "Amy's Bird Sanctuary"
    },
    "VendorRef": {
      "value": "41",
      "name": "Hicks Hardware"
    },
    "ItemRef": {
      "value": "11",
      "name": "Rock Fountain"
    },
    "TxnDate": "2025-01-15",
    "HasBeenInvoiced": false,
    "QtyOnHand": 1,
    "UnitPrice": 125.00,
    "PrivateNote": "Customer requested special order",
    "Description": "Special order rock fountain for customer",
    "domain": "QBO",
    "sparse": false,
    "MetaData": {
      "CreateTime": "2025-01-15T11:00:00-08:00",
      "LastUpdatedTime": "2025-01-15T11:00:00-08:00"
    }
  },
  "time": "2025-01-15T11:00:00.000-08:00"
}
```

### Read
Retrieve a reimbursable charge by ID.

#### Request
```
GET /v3/company/{companyId}/reimbursecharge/{reimburseChargeId}
```

### Update
Update an existing reimbursable charge.

#### Request
```
POST /v3/company/{companyId}/reimbursecharge
```

Include the full reimbursable charge object with `Id` and updated `SyncToken`.

### Delete
Delete a reimbursable charge.

#### Request
```
POST /v3/company/{companyId}/reimbursecharge?operation=delete
```

#### Request Body
```json
{
  "Id": "145",
  "SyncToken": "0"
}
```

### Query
Query reimbursable charges with filters.

#### Request
```
GET /v3/company/{companyId}/query?query=select * from ReimburseCharge where HasBeenInvoiced = false
```

## Fields

- `Amount` (required) - Total charge amount
- `CustomerRef` (required) - Customer to charge
- `VendorRef` - Vendor who provided the item/service
- `ItemRef` - Item being charged
- `TxnDate` - Transaction date
- `HasBeenInvoiced` - Whether charge has been invoiced
- `QtyOnHand` - Quantity
- `UnitPrice` - Price per unit
- `Description` - Description of the charge
- `PrivateNote` - Internal note
- `LinkedTxnRef` - Reference to source transaction
- `ClassRef` - Class reference
- `DepartmentRef` - Department reference
- `MarkupInfo` - Markup information

## MarkupInfo Structure
```json
{
  "MarkupInfo": {
    "PercentBased": true,
    "Percent": 20,
    "Value": 25.00,
    "MarkUpIncomeAccountRef": {
      "value": "82",
      "name": "Markup Income"
    }
  }
}
```

## Linking to Invoices

To invoice a reimbursable charge, include it in an invoice line:
```json
{
  "Line": [
    {
      "DetailType": "ReimburseLineDetail",
      "Amount": 150.00,
      "ReimburseLineDetail": {
        "ReimburseChargeRef": {
          "value": "145"
        }
      }
    }
  ]
}
```

## Common Use Cases

### Billable Expense from Purchase
When creating a purchase marked as billable:
```json
{
  "LinkedTxnRef": {
    "TxnId": "123",
    "TxnType": "Purchase"
  },
  "Amount": 100.00,
  "MarkupInfo": {
    "PercentBased": true,
    "Percent": 15
  }
}
```

### Time Tracking Charges
For billable time entries:
```json
{
  "LinkedTxnRef": {
    "TxnId": "456",
    "TxnType": "TimeActivity"
  },
  "Description": "Consulting services - 2 hours",
  "Amount": 200.00
}
```

## Notes
- Tracks billable expenses before invoicing
- Can include markup on vendor costs
- Links to source transactions (purchases, bills, time activities)
- Automatically marked as invoiced when included in an invoice
- Supports class and department tracking
- Can be filtered to show only uninvoiced charges