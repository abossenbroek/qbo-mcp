# Deposit

The Deposit object represents money received from customers and deposited into a bank account. It can include payments from various sources including cash, checks, credit card transactions, and other forms of payment. Deposits can be linked to existing sales transactions or recorded as standalone deposits.

## Business Rules

- The DepositToAccountRef attribute is required and must reference an active bank or other current asset account
- Line items must specify either an AccountRef (for direct deposits) or LinkedTxn (for customer payments)
- The TotalAmt attribute must equal the sum of all line amounts
- CurrencyRef is required for multicurrency-enabled companies
- Deposits cannot be deleted if they have been reconciled in the bank register

## The Deposit object

### ATTRIBUTES

| Name | Type | Required | Description | Notes |
|------|------|----------|-------------|-------|
| **Id** | String | Required for update | Unique identifier for this object | read only, system defined, filterable, sortable |
| **SyncToken** | String | Required for update | Version number of the object | read only, system defined |
| **TxnDate** | Date | Required | The date entered by the user when this transaction occurred | YYYY-MM-DD format, filterable, sortable |
| **DepositToAccountRef** | ReferenceType | Required | Account where the funds are deposited | Must be Bank or OtherCurrentAsset account type |
| **Line** | Array | Required | Individual line items of the deposit | At least one line item required |
| **TotalAmt** | Decimal | read only | Total amount of the transaction | System calculated, must match sum of lines |
| **CurrencyRef** | ReferenceType | Conditional | Reference to the currency | Required for multicurrency-enabled companies |
| **ExchangeRate** | Decimal | Conditional | Currency exchange rate | Valid for multicurrency-enabled companies |
| **PrivateNote** | String | Optional | User-entered note for internal use | Max 4000 characters |
| **TxnStatus** | String | Optional | Status of the transaction | |
| **LinkedTxn** | Array | Optional | Transactions linked to this deposit | |
| **DepositToAccountRef.name** | String | Optional | Name of the account | read only |
| **DepositToAccountRef.value** | String | Required | Id of the account | |
| **MetaData** | MetaData | read only | Metadata for the object | System defined |
| **DocNumber** | String | Optional | Reference number for the transaction | |
| **TxnSource** | String | Optional | Source of the transaction | |
| **GlobalTaxCalculation** | GlobalTaxCalculationEnum | Optional | Method used for tax calculation | |

### Line Item Attributes

| Name | Type | Required | Description | Notes |
|------|------|----------|-------------|-------|
| **Id** | String | Optional | Line item identifier | |
| **LineNum** | Integer | Optional | Specifies line order | System generated if not provided |
| **Description** | String | Optional | Description of the line item | |
| **Amount** | Decimal | Required | Amount of the line item | Must be positive |
| **DetailType** | String | Required | Type of line detail | Must be "DepositLineDetail" |
| **DepositLineDetail** | DepositLineDetail | Required | Details for this deposit line | |
| **LinkedTxn** | Array | Optional | Linked transactions | |

### DepositLineDetail Attributes

| Name | Type | Required | Description | Notes |
|------|------|----------|-------------|-------|
| **AccountRef** | ReferenceType | Conditional | Account for this deposit line | Required if no linked transaction |
| **PaymentMethodRef** | ReferenceType | Optional | Payment method reference | |
| **CheckNum** | String | Optional | Check number if applicable | |
| **TxnType** | TxnTypeEnum | Optional | Transaction type of linked transaction | |
| **TaxCodeRef** | ReferenceType | Optional | Reference to the tax code | |
| **TaxApplicableOn** | TaxApplicableOnEnum | Optional | Indicates which taxes apply | |
| **ClassRef** | ReferenceType | Optional | Reference to the class | |
| **CustomerRef** | ReferenceType | Optional | Reference to the customer | |
| **EntityRef** | ReferenceType | Optional | Reference to an entity | |

## Sample JSON Response

```json
{
  "Deposit": {
    "Id": "162",
    "SyncToken": "0",
    "MetaData": {
      "CreateTime": "2024-01-15T14:30:45-08:00",
      "LastUpdatedTime": "2024-01-15T14:30:45-08:00"
    },
    "TxnDate": "2024-01-15",
    "CurrencyRef": {
      "value": "USD",
      "name": "United States Dollar"
    },
    "ExchangeRate": 1,
    "PrivateNote": "Weekly deposit",
    "Line": [
      {
        "Id": "1",
        "LineNum": 1,
        "Description": "Payment received - Invoice #1001",
        "Amount": 500.00,
        "DetailType": "DepositLineDetail",
        "DepositLineDetail": {
          "AccountRef": {
            "value": "83",
            "name": "Undeposited Funds"
          },
          "PaymentMethodRef": {
            "value": "1",
            "name": "Cash"
          },
          "CustomerRef": {
            "value": "21",
            "name": "John Smith"
          }
        },
        "LinkedTxn": [
          {
            "TxnId": "145",
            "TxnType": "Payment"
          }
        ]
      },
      {
        "Id": "2",
        "LineNum": 2,
        "Description": "Direct deposit",
        "Amount": 250.00,
        "DetailType": "DepositLineDetail",
        "DepositLineDetail": {
          "AccountRef": {
            "value": "1",
            "name": "Services Income"
          }
        }
      }
    ],
    "TotalAmt": 750.00,
    "DepositToAccountRef": {
      "value": "35",
      "name": "Checking Account"
    }
  },
  "time": "2024-01-15T14:30:45.892-08:00"
}
```

## CRUD Operations

### Create (POST)
```
POST /v3/company/{companyId}/deposit
Content-Type: application/json
```

Creates a new deposit transaction. Required fields:
- TxnDate
- DepositToAccountRef
- At least one Line item with Amount and DepositLineDetail

### Read (GET)
```
GET /v3/company/{companyId}/deposit/{depositId}
```

Retrieves a specific deposit by ID.

### Update (POST)
```
POST /v3/company/{companyId}/deposit
Content-Type: application/json
```

Updates an existing deposit. Required fields:
- Id
- SyncToken
- All fields from Create operation

Note: Deposits use full update mode - all fields must be provided.

### Delete (POST)
```
POST /v3/company/{companyId}/deposit?operation=delete
Content-Type: application/json

{
  "Id": "162",
  "SyncToken": "0"
}
```

Deletes a deposit. Only Id and SyncToken are required in the request body.

### Query
```
GET /v3/company/{companyId}/query?query=SELECT * FROM Deposit WHERE TxnDate > '2024-01-01'
```

Query deposits using SQL-like syntax. Filterable fields include:
- Id
- TxnDate
- TotalAmt
- DepositToAccountRef

## Special Notes and Limitations

1. **Linking Payments**: When depositing customer payments, use LinkedTxn to reference the original Payment transactions. This maintains proper accounting links.

2. **Undeposited Funds**: Payments typically flow through an "Undeposited Funds" account before being deposited to the bank account.

3. **Bank Reconciliation**: Once a deposit has been reconciled in the bank register, it cannot be modified or deleted.

4. **Multi-currency**: For companies with multi-currency enabled:
   - CurrencyRef is required
   - ExchangeRate must be provided for non-home currencies
   - All amounts are in the transaction currency

5. **Line Item Validation**: 
   - Each line must have either AccountRef (for direct deposits) or LinkedTxn (for payment deposits)
   - Line amounts must be positive
   - The sum of all line amounts must equal TotalAmt

6. **Account Types**: DepositToAccountRef must reference an account of type:
   - Bank
   - OtherCurrentAsset

7. **Sparse Updates**: Deposits do not support sparse updates. The entire object must be sent when updating.

8. **Maximum Lines**: There is a practical limit of 1000 line items per deposit transaction.

9. **Date Restrictions**: TxnDate cannot be prior to the company's start date or in a closed accounting period.