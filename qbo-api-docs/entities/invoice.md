# Invoice

## Entity Description
The Invoice entity represents a sales form where the customer pays for a product or service later. An invoice is a request for payment that contains a detailed list of goods shipped or services rendered, the total amount due, and the payment terms.

## Attributes

| Name | Type | Required | Description | Notes |
|------|------|----------|-------------|-------|
| Id | String | Read-only | Unique identifier for this object | System generated |
| SyncToken | String | Required for update | Version number of the object | Used for optimistic concurrency control |
| MetaData | MetaData | Read-only | Metadata for the object | Contains CreateTime and LastUpdatedTime |
| CustomField | CustomField[] | No | Custom field(s) for the transaction | |
| DocNumber | String | No | Reference number for the transaction | If not provided, system generates based on preferences |
| TxnDate | Date | No | Date when the transaction occurred | Format: YYYY-MM-DD |
| CurrencyRef | ReferenceType | No | Reference to the Currency | Required for multicurrency |
| ExchangeRate | Decimal | No | Currency exchange rate | Valid for multicurrency |
| PrivateNote | String | No | User entered note for internal use | Not visible to customer |
| LinkedTxn | LinkedTxn[] | No | Linked transactions | |
| Line | Line[] | Yes | Individual line items of the transaction | At least one line item required |
| TxnTaxDetail | TxnTaxDetail | No | Transaction level tax details | |
| CustomerRef | ReferenceType | Yes | Reference to the Customer | Required field |
| CustomerMemo | String | No | User-entered message to the customer | Appears on the invoice |
| BillAddr | PhysicalAddress | No | Bill-to address | |
| ShipAddr | PhysicalAddress | No | Ship-to address | |
| ClassRef | ReferenceType | No | Reference to the Class | |
| SalesTermRef | ReferenceType | No | Reference to the sales term | |
| DueDate | Date | No | Date when payment is due | |
| GlobalTaxCalculation | GlobalTaxCalculationEnum | No | Method used to calculate tax | |
| ShipMethodRef | ReferenceType | No | Reference to the shipping method | |
| ShipDate | Date | No | Date of shipment | |
| TrackingNum | String | No | Shipping tracking number | |
| TotalAmt | Decimal | Read-only | Total amount of the transaction | System calculated |
| HomeTotalAmt | Decimal | Read-only | Total amount in home currency | For multicurrency |
| ApplyTaxAfterDiscount | Boolean | No | Whether to apply tax after discount | |
| PrintStatus | PrintStatusEnum | No | Print status | |
| EmailStatus | EmailStatusEnum | No | Email status | |
| BillEmail | EmailAddress | No | Email address for billing | |
| BillEmailCc | EmailAddress | No | CC email address for billing | |
| BillEmailBcc | EmailAddress | No | BCC email address for billing | |
| DepositToAccountRef | ReferenceType | No | Asset account for deposit | |
| Deposit | Decimal | No | Deposit amount received | |
| AllowIPNPayment | Boolean | No | Whether IPN payment is allowed | |
| AllowOnlinePayment | Boolean | No | Whether online payment is allowed | |
| AllowOnlineACHPayment | Boolean | No | Whether online ACH payment is allowed | |
| AllowOnlineCreditCardPayment | Boolean | No | Whether online credit card payment is allowed | |
| DeliveryInfo | DeliveryInfo | No | Delivery information | For emailed transactions |

### Line Item Details
Each Line item can be one of the following types:
- **ItemBasedExpenseLine** - Line item based on an item
- **AccountBasedExpenseLine** - Line item based on an account
- **DescriptionOnlyLine** - Line item with description only
- **DiscountLine** - Discount line item
- **SubTotalLine** - Subtotal line (read-only)
- **GroupLine** - Grouped line items

## Sample JSON Response

```json
{
  "Invoice": {
    "Id": "130",
    "SyncToken": "0",
    "MetaData": {
      "CreateTime": "2019-12-20T10:08:51-08:00",
      "LastUpdatedTime": "2019-12-20T10:08:51-08:00"
    },
    "CustomField": [],
    "DocNumber": "1037",
    "TxnDate": "2019-12-20",
    "CurrencyRef": {
      "value": "USD",
      "name": "United States Dollar"
    },
    "LinkedTxn": [],
    "Line": [
      {
        "Id": "1",
        "LineNum": 1,
        "Amount": 100.00,
        "DetailType": "SalesItemLineDetail",
        "SalesItemLineDetail": {
          "ItemRef": {
            "value": "1",
            "name": "Services"
          },
          "TaxCodeRef": {
            "value": "NON"
          }
        }
      },
      {
        "Amount": 100.00,
        "DetailType": "SubTotalLineDetail",
        "SubTotalLineDetail": {}
      }
    ],
    "TxnTaxDetail": {
      "TotalTax": 0
    },
    "CustomerRef": {
      "value": "1",
      "name": "Amy's Bird Sanctuary"
    },
    "CustomerMemo": {
      "value": "Thank you for your business!"
    },
    "BillAddr": {
      "Id": "2",
      "Line1": "4581 Finch St.",
      "City": "Bayshore",
      "CountrySubDivisionCode": "CA",
      "PostalCode": "94326",
      "Lat": "37.3930855",
      "Long": "-122.1074429"
    },
    "ShipAddr": {
      "Id": "2",
      "Line1": "4581 Finch St.",
      "City": "Bayshore",
      "CountrySubDivisionCode": "CA",
      "PostalCode": "94326",
      "Lat": "37.3930855",
      "Long": "-122.1074429"
    },
    "SalesTermRef": {
      "value": "3"
    },
    "DueDate": "2020-01-19",
    "GlobalTaxCalculation": "TaxExcluded",
    "TotalAmt": 100.00,
    "ApplyTaxAfterDiscount": false,
    "PrintStatus": "NeedToPrint",
    "EmailStatus": "NotSet",
    "Balance": 100.00,
    "Deposit": 0,
    "AllowIPNPayment": false,
    "AllowOnlinePayment": false,
    "AllowOnlineACHPayment": false,
    "AllowOnlineCreditCardPayment": false
  },
  "time": "2019-12-20T10:08:51.369-08:00"
}
```

## CRUD Operations

### Create Invoice
- **Endpoint**: `POST /v3/company/{companyId}/invoice`
- **Content-Type**: `application/json`
- **Required fields**: CustomerRef, Line (at least one line item)

### Read Invoice
- **Single Invoice**: `GET /v3/company/{companyId}/invoice/{invoiceId}`
- **Query Invoices**: `GET /v3/company/{companyId}/query?query=select * from Invoice`

### Update Invoice
- **Endpoint**: `POST /v3/company/{companyId}/invoice`
- **Content-Type**: `application/json`
- **Required fields**: Id, SyncToken, plus fields to update
- **Note**: Sparse update is supported

### Delete Invoice
- **Endpoint**: `POST /v3/company/{companyId}/invoice?operation=delete`
- **Content-Type**: `application/json`
- **Required fields**: Id, SyncToken

### Send Invoice
- **Endpoint**: `POST /v3/company/{companyId}/invoice/{invoiceId}/send`
- **Note**: Sends invoice to the email specified in BillEmail

## Special Notes and Limitations

1. **Line Items**: At least one line item is required for creating an invoice
2. **SyncToken**: Required for update operations to prevent conflicting changes
3. **Voiding**: Invoices cannot be deleted if they have been partially or fully paid. Use void operation instead
4. **Maximum Lines**: There is a limit on the number of line items (typically 1000)
5. **Custom Fields**: Maximum of 3 custom fields allowed
6. **Currency**: Once set, currency cannot be changed
7. **Tax Calculation**: GlobalTaxCalculation affects how taxes are calculated and displayed
8. **Payment Integration**: AllowOnlinePayment flags control payment options shown to customers
9. **Linked Transactions**: Invoices can be linked to estimates, sales receipts, and payments
10. **Email Delivery**: Use the send endpoint to email invoices to customers

## Related Entities
- Customer
- Item
- Account
- Payment
- CreditMemo
- Estimate
- SalesReceipt
- Class
- TaxCode
- Term

## Common Use Cases
1. Creating invoices for products/services delivered
2. Tracking accounts receivable
3. Managing payment terms and due dates
4. Sending invoices to customers via email
5. Applying payments to invoices
6. Creating recurring invoices
7. Handling multi-currency transactions