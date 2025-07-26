# PaymentMethod Entity - QuickBooks Online API

## Entity Description
The PaymentMethod entity represents the various payment methods that can be used to record payments in QuickBooks Online. This includes methods such as cash, check, credit card, ACH, and custom payment types. Payment methods are referenced when creating payments, sales receipts, and other transaction types.

## Attributes

| Name | Type | Required | Description | Notes |
|------|------|----------|-------------|-------|
| Id | String | Read-only | Unique identifier for the payment method | System generated |
| Name | String | Required | Display name of the payment method | Max 31 characters |
| Active | Boolean | Optional | Whether the payment method is active | Default: true |
| Type | String | Read-only | Type of payment method | System defined |
| MetaData | MetaData | Read-only | Metadata for the entity | Contains CreateTime and LastUpdatedTime |
| SyncToken | String | Required for updates | Version number of the entity | Used for optimistic locking |

## Sample JSON Response

```json
{
  "PaymentMethod": {
    "Id": "5",
    "Name": "Credit Card",
    "Active": true,
    "Type": "CREDIT_CARD",
    "MetaData": {
      "CreateTime": "2023-01-15T10:30:00-08:00",
      "LastUpdatedTime": "2023-01-15T10:30:00-08:00"
    },
    "SyncToken": "0",
    "domain": "QBO",
    "sparse": false
  },
  "time": "2023-01-15T10:30:00.123-08:00"
}
```

## CRUD Operations

### Create Payment Method
- **Endpoint**: `POST /v3/company/{companyID}/paymentmethod`
- **Content-Type**: `application/json`
- **Required Fields**: Name
- **Note**: Some payment methods are system-defined and cannot be created

### Read Payment Method
- **Single Payment Method**: `GET /v3/company/{companyID}/paymentmethod/{paymentmethodId}`
- **Query Payment Methods**: `GET /v3/company/{companyID}/query?query=select * from PaymentMethod where Active = true`

### Update Payment Method
- **Endpoint**: `POST /v3/company/{companyID}/paymentmethod`
- **Content-Type**: `application/json`
- **Required**: Include Id and SyncToken from existing payment method
- **Updatable Fields**: Name, Active

### Delete Payment Method
- **Note**: Payment methods cannot be deleted, only deactivated by setting Active to false

## Special Notes and Limitations

1. **System Payment Methods**: QuickBooks provides several built-in payment methods (Cash, Check, Credit Card, etc.) that cannot be deleted
2. **Custom Payment Methods**: Users can create custom payment methods for specific business needs
3. **Active Status**: Inactive payment methods won't appear in selection lists but remain in historical transactions
4. **Name Constraints**: Payment method names must be unique within a company
5. **Usage**: Payment methods are referenced in Payment, SalesReceipt, and other transaction entities via PaymentMethodRef

## Business Rules

- Payment method names must be unique (case-insensitive)
- Cannot delete system-defined payment methods
- Deactivated payment methods remain available for historical reporting
- Maximum of 31 characters for payment method names

## Common Payment Method Types

- Cash
- Check
- Credit Card
- ACH
- Wire Transfer
- Other (custom types)

## Error Codes
- 610: Object Not Found (invalid PaymentMethod ID)
- 2020: Update Failed, Object has been modified (SyncToken mismatch)
- 6140: Duplicate Name exists (payment method name already in use)