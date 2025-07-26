# CreditMemo

A CreditMemo is a financial transaction representing a refund or credit of payment or part of a payment for goods or services that have been sold.

## The creditmemo object

### Attributes

| Attribute | Type | Description |
|-----------|------|-------------|
| **Id** | String | Read only, system defined. Unique identifier for this object. |
| **CustomerRef** | ReferenceType | **Required**. Reference to a customer or job. Query the Customer name list resource to determine the appropriate Customer object for this reference. |
| **Line** | Line[] | **Required**. Individual line items of a transaction. Valid Line types include: SalesItemLine, GroupLine, DescriptionLine, DiscountLine, SubtotalLine, and CreditMemoLine. |
| **TotalAmt** | Decimal | Read only. Total amount of the transaction. This includes the total of all the lines, taxes, and discounts. Calculated by QuickBooks. |
| **SyncToken** | String | **Required for update**. Version number of the object. |
| **CurrencyRef** | CurrencyRefType | **Conditionally required**. Reference to the currency in which all amounts on the associated transaction are expressed. Required if multicurrency is enabled. |
| **DocNumber** | String | Optional. Reference number for the transaction. If not explicitly set, QuickBooks will generate a number. |
| **TxnDate** | Date | Optional. Date when the transaction occurred. If not provided, current date is used. |
| **PrivateNote** | String | Optional. User entered, organization-private note about the transaction. Does not appear on the credit memo. |
| **CustomField** | CustomField[] | Optional. Custom field(s) for the transaction. |
| **TxnTaxDetail** | TxnTaxDetail | Optional. Details of taxes charged on the transaction as a whole. |
| **CustomerMemo** | MemoRef | Optional. User-entered message to the customer that appears on the credit memo. |
| **BillAddr** | PhysicalAddress | Optional. Bill-to address of the customer. |
| **ShipAddr** | PhysicalAddress | Optional. Ship-to address of the customer. |
| **ClassRef** | ReferenceType | Optional. Reference to the class associated with this transaction. |
| **PrintStatus** | PrintStatusEnum | Optional. Print status of the credit memo. Valid values: NotSet, NeedToPrint, PrintComplete. |
| **EmailStatus** | EmailStatusEnum | Optional. Email status of the credit memo. Valid values: NotSet, NeedToSend, EmailSent. |
| **Balance** | Decimal | Read only. The balance reflecting any payments made against the transaction. |
| **PaymentMethodRef** | ReferenceType | Optional. Reference to the payment method for the transaction. |
| **DepositToAccountRef** | ReferenceType | Optional. Asset account where the payment money is deposited. |
| **ApplyTaxAfterDiscount** | Boolean | Optional. If true, discount is applied before tax is calculated. |
| **ExchangeRate** | Decimal | Optional. Currency exchange rate. Valid only if multicurrency is enabled. |
| **RemainingCredit** | Decimal | Read only. Indicates the amount of credit remaining to be applied. |
| **DepartmentRef** | ReferenceType | Optional. Reference to the department associated with this transaction. |
| **HomeTotalAmt** | Decimal | Read only. Total amount in home currency. Valid only if multicurrency is enabled. |
| **MetaData** | ModificationMetaData | Optional. Metadata about object creation and last update time. |

## Operations

### Create a creditmemo

Creates a new CreditMemo object.

**Required fields:**
- CustomerRef
- Line (at least one line item)

### Query a creditmemo

Returns the results of the query for CreditMemo objects.

**Example query:**
```
SELECT * FROM CreditMemo WHERE Balance > '0.0'
```

### Read a creditmemo

Retrieves the details of a CreditMemo that has been previously created.

### Update a creditmemo

Updates an existing CreditMemo object.

**Required fields:**
- Id
- SyncToken
- All originally required fields

### Delete a creditmemo

Deletes an existing CreditMemo object.

**Required fields:**
- Id
- SyncToken

## Use Cases

Credit memos are commonly used for:
- **Returns**: When a customer returns purchased goods
- **Allowances**: When providing a discount after the sale
- **Corrections**: To correct billing errors on previous invoices
- **Goodwill credits**: To maintain customer satisfaction

## Credit Application

Credit memos can be applied to:
- **Future invoices**: The credit remains on the customer's account for future use
- **Specific invoices**: Apply immediately to open invoices
- **Refund**: Process as a refund payment to the customer

## Best Practices

1. **Reference original transaction**: Include information about the original invoice or sale
2. **Clear descriptions**: Provide detailed line items explaining the reason for the credit
3. **Proper categorization**: Use appropriate accounts and classes for tracking
4. **Timely processing**: Issue credit memos promptly to maintain accurate customer balances