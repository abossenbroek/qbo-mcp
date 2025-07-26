# Payment Entity - QuickBooks Online API

## Entity Description
The Payment entity represents a customer payment transaction in QuickBooks Online. It records money received from customers for goods or services, and can be applied to invoices, credit memos, or recorded as unapplied customer payments.

## Attributes

| Name | Type | Required | Description | Notes |
|------|------|----------|-------------|-------|
| Id | String | Read-only | Unique identifier for the payment | System generated |
| SyncToken | String | Required for updates | Version number of the entity | Used for optimistic locking |
| MetaData | MetaData | Read-only | Metadata for the entity | Contains CreateTime and LastUpdatedTime |
| TxnDate | Date | Required | Date of the payment transaction | Format: YYYY-MM-DD |
| PrivateNote | String | Optional | Private note about the payment | Not visible to customer |
| Line | Array[Line] | Optional | Individual line items of the payment | Links payment to invoices/transactions |
| CustomerRef | ReferenceType | Required | Reference to the customer | Must be an existing customer |
| DepositToAccountRef | ReferenceType | Optional | Account where payment is deposited | Defaults to Undeposited Funds |
| PaymentMethodRef | ReferenceType | Optional | Reference to payment method | E.g., Cash, Check, Credit Card |
| PaymentRefNum | String | Optional | Reference number for the payment | Check number or transaction ID |
| TotalAmt | Decimal | Required | Total amount of the payment | Must equal sum of line amounts |
| UnappliedAmt | Decimal | Read-only | Amount not yet applied to invoices | System calculated |
| ProcessPayment | Boolean | Optional | Process payment through merchant service | Default: false |
| Currency | CurrencyRef | Optional | Currency of the payment | Required for multicurrency |
| ExchangeRate | Decimal | Optional | Currency exchange rate | Required if currency differs from home currency |
| TxnSource | String | Optional | Source of the transaction | System populated |

### Line Item Attributes

| Name | Type | Required | Description | Notes |
|------|------|----------|-------------|-------|
| Amount | Decimal | Required | Amount applied on this line | Must be positive |
| LinkedTxn | Array[LinkedTxn] | Required | Transactions this payment is applied to | Invoices, Credit Memos, etc. |

### LinkedTxn Attributes

| Name | Type | Required | Description | Notes |
|------|------|----------|-------------|-------|
| TxnId | String | Required | ID of the linked transaction | Must be valid transaction |
| TxnType | String | Required | Type of linked transaction | Invoice, CreditMemo, etc. |

## Sample JSON Response

```json
{
  "Payment": {
    "Id": "145",
    "SyncToken": "0",
    "MetaData": {
      "CreateTime": "2023-10-15T09:42:35-07:00",
      "LastUpdatedTime": "2023-10-15T09:42:35-07:00"
    },
    "TxnDate": "2023-10-15",
    "CurrencyRef": {
      "value": "USD",
      "name": "United States Dollar"
    },
    "Line": [
      {
        "Amount": 555.00,
        "LinkedTxn": [
          {
            "TxnId": "130",
            "TxnType": "Invoice"
          }
        ]
      }
    ],
    "CustomerRef": {
      "value": "1",
      "name": "Amy's Bird Sanctuary"
    },
    "DepositToAccountRef": {
      "value": "4",
      "name": "Undeposited Funds"
    },
    "PaymentMethodRef": {
      "value": "1",
      "name": "Cash"
    },
    "PaymentRefNum": "10264",
    "TotalAmt": 555.00,
    "UnappliedAmt": 0.00,
    "ProcessPayment": false,
    "domain": "QBO",
    "sparse": false
  },
  "time": "2023-10-15T09:42:35.531-07:00"
}
```

## CRUD Operations

### Create Payment
- **Endpoint**: `POST /v3/company/{companyID}/payment`
- **Content-Type**: `application/json`
- **Required Fields**: CustomerRef, TotalAmt, TxnDate

### Read Payment
- **Single Payment**: `GET /v3/company/{companyID}/payment/{paymentId}`
- **Query Payments**: `GET /v3/company/{companyID}/query?query=select * from Payment where TxnDate > '2023-01-01'`

### Update Payment
- **Endpoint**: `POST /v3/company/{companyID}/payment`
- **Content-Type**: `application/json`
- **Required**: Include Id and SyncToken from existing payment
- **Note**: Supports both full and sparse updates

### Delete Payment
- **Endpoint**: `POST /v3/company/{companyID}/payment?operation=delete`
- **Content-Type**: `application/json`
- **Required**: Include Id and SyncToken
- **Note**: Soft delete only; payment is marked as deleted but retained

## Special Notes and Limitations

1. **Payment Application**: Payments can be applied to multiple invoices or credit memos through the Line items
2. **Unapplied Payments**: Payments can be created without applying them to any invoices (unapplied payments)
3. **Currency**: For multicurrency companies, the payment currency must match the customer's currency
4. **Deposit Account**: If DepositToAccountRef is not specified, payments go to "Undeposited Funds" account
5. **Payment Processing**: Setting ProcessPayment to true will attempt to process the payment through QuickBooks Payments
6. **Voiding**: Payments cannot be voided directly; they must be deleted and recreated
7. **Linked Transactions**: When a payment is linked to invoices, the invoice balance is automatically updated
8. **Maximum Lines**: A payment can be applied to multiple invoices but check API limits for maximum line items

## Business Rules

- Payment amount must be greater than zero
- Customer must exist before creating a payment
- Cannot modify a payment that has been deposited
- Payment date cannot be in a closed accounting period
- For credit card payments processed through QuickBooks Payments, certain fields become read-only

## Error Codes
- 610: Object Not Found (invalid CustomerRef or LinkedTxn)
- 2020: Update Failed, Object has been modified (SyncToken mismatch)
- 6000: A business validation error has occurred