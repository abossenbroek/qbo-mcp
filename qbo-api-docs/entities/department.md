# Department

- < Back to Documentation
- Accounting All entities AccountAccountListDetailAPAgingDetailAPAgingSummaryARAgingDetailARAgingSummaryAttachableBalanceSheetBatchBillBillPaymentBudgetCashFlowChangeDataCaptureClassCompanyCurrencyCompanyInfoCreditMemoCreditCardPaymentCustomerCustomerBalanceCustomerBalanceDetailCustomerIncomeFECReportCustomerTypeDepartmentThe Department objectCreate a departmentQuery a departmentRead a departmentFull update a departmentDepositEmployeeEntitlementsEstimateExchangerateGeneralLedgerGeneralLedgerFRInventoryAdjustmentInventoryValuationDetailInventoryValuationSummaryInvoiceItemJournalCodeJournalEntryJournalReportJournalReportFRPaymentPaymentMethodPreferencesProfitAndLossProfitAndLossDetailPurchasePurchaseOrderRecurringTransactionRefundReceiptReimburseChargeSalesByClassSummarySalesByCustomerSalesByDepartmentSalesByProductSalesReceiptTaxClassificationTaxCodeTaxPaymentTaxRateTaxServiceTaxSummaryTaxAgencyTermTimeActivityTransactionListTransactionListByVendorTransactionListByCustomerTransactionListWithSplitsTransferTrialBalanceVendorVendorBalanceVendorBalanceDetailVendorCreditVendorExpensesMost commonly usedE-CommerceReport entities
- All entities AccountAccountListDetailAPAgingDetailAPAgingSummaryARAgingDetailARAgingSummaryAttachableBalanceSheetBatchBillBillPaymentBudgetCashFlowChangeDataCaptureClassCompanyCurrencyCompanyInfoCreditMemoCreditCardPaymentCustomerCustomerBalanceCustomerBalanceDetailCustomerIncomeFECReportCustomerTypeDepartmentThe Department objectCreate a departmentQuery a departmentRead a departmentFull update a departmentDepositEmployeeEntitlementsEstimateExchangerateGeneralLedgerGeneralLedgerFRInventoryAdjustmentInventoryValuationDetailInventoryValuationSummaryInvoiceItemJournalCodeJournalEntryJournalReportJournalReportFRPaymentPaymentMethodPreferencesProfitAndLossProfitAndLossDetailPurchasePurchaseOrderRecurringTransactionRefundReceiptReimburseChargeSalesByClassSummarySalesByCustomerSalesByDepartmentSalesByProductSalesReceiptTaxClassificationTaxCodeTaxPaymentTaxRateTaxServiceTaxSummaryTaxAgencyTermTimeActivityTransactionListTransactionListByVendorTransactionListByCustomerTransactionListWithSplitsTransferTrialBalanceVendorVendorBalanceVendorBalanceDetailVendorCreditVendorExpenses
- Account
- AccountListDetail
- APAgingDetail
- APAgingSummary
- ARAgingDetail
- ARAgingSummary
- Attachable
- BalanceSheet
- Batch
- Bill
- BillPayment
- Budget
- CashFlow
- ChangeDataCapture
- Class
- CompanyCurrency
- CompanyInfo
- CreditMemo
- CreditCardPayment
- Customer
- CustomerBalance
- CustomerBalanceDetail
- CustomerIncome
- FECReport
- CustomerType
- DepartmentThe Department objectCreate a departmentQuery a departmentRead a departmentFull update a department
- The Department object
- Create a department
- Query a department
- Read a department
- Full update a department
- Deposit
- Employee
- Entitlements
- Estimate
- Exchangerate
- GeneralLedger
- GeneralLedgerFR
- InventoryAdjustment
- InventoryValuationDetail
- InventoryValuationSummary
- Invoice
- Item
- JournalCode
- JournalEntry
- JournalReport
- JournalReportFR
- Payment
- PaymentMethod
- Preferences
- ProfitAndLoss
- ProfitAndLossDetail
- Purchase
- PurchaseOrder
- RecurringTransaction
- RefundReceipt
- ReimburseCharge
- SalesByClassSummary
- SalesByCustomer
- SalesByDepartment
- SalesByProduct
- SalesReceipt
- TaxClassification
- TaxCode
- TaxPayment
- TaxRate
- TaxService
- TaxSummary
- TaxAgency
- Term
- TimeActivity
- TransactionList
- TransactionListByVendor
- TransactionListByCustomer
- TransactionListWithSplits
- Transfer
- TrialBalance
- Vendor
- VendorBalance
- VendorBalanceDetail
- VendorCredit
- VendorExpenses
- Most commonly used
- E-Commerce
- Report entities

## The department object

- Id* Required for update  read only  system defined String , filterable , sortable Unique identifier for this object.
Sort order is ASC by default.
- Name* Required  max character: maximum of 100 chars String  User recognizable name for the Department.
- SyncToken* Required for update  read only  system defined String  Version number of the object. It is used to lock an object for use by one app at a time. As soon as an application modifies an object, its SyncToken is incremented. Attempts to modify an object specifying an older SyncToken fails. Only the latest version of the object is maintained by QuickBooks Online.
- ParentRef* Conditionally required   ReferenceType  The immediate parent of the SubDepartment.
Required for the create operation if this object is a SubDepartment. Required if this object is a subdepartment.Show child attributes
- Active Optional Boolean , filterable , sortable If true, this entity is currently enabled for use by QuickBooks. If set to false, this entity is not available.
- MetaData Optional ModificationMetaData , filterable , sortable Descriptive information about the object. The MetaData values are set by Data Services and are read only for all applications. Show child attributes
- FullyQualifiedName read only  system defined String , filterable , sortable Fully qualified name of the entity. The fully qualified name prepends the topmost parent, followed by each sub element separated by colons. Takes the form of Parent:Department1:SubDepartment1:SubDepartment2. Limited to 5 levels.
- SubDepartment read only  system defined Boolean  , sortable Specifies whether this Department object is a SubDepartment.
true--SubDepartment.
false or null--top-level Department.
SAMPLE OBJECT


## Create a department


### Request Body

The elements to create a Department object are listed here.

The elements to create a Department object are listed here.

- Name* Required  max character: maximum of 100 chars String  User recognizable name for the department.
- ParentRef* Conditionally required   ReferenceType  The immediate parent of the SubDepartment.
Required for the create operation if this object is a SubDepartment. Required if this object is a subdepartmentShow child attributes

### Returns

Returns the newly created Department object.

Returns the newly created Department object.

Request URL

Request Body


### Sign in to explore our APIs

Returns


## Query a department


### Returns

Returns the results of the query.

Request URL

Sample Query


### Sign in to explore our APIs

Returns


## Read a department


### Returns

Returns the Department object.

Request URL


### Sign in to explore our APIs

Returns


## Full update a department


### Request Body

- Id* Required for update  read only  system defined String , filterable , sortable Unique identifier for this object.
Sort order is ASC by default.
- Name* Required  max character: maximum of 100 chars String  User recognizable name for the Department.
- SyncToken* Required for update  read only  system defined String  Version number of the object. It is used to lock an object for use by one app at a time. As soon as an application modifies an object, its SyncToken is incremented. Attempts to modify an object specifying an older SyncToken fails. Only the latest version of the object is maintained by QuickBooks Online.
- ParentRef* Conditionally required   ReferenceType  The immediate parent of the SubDepartment.
Required for the create operation if this object is a SubDepartment. Required if this object is a subdepartment.Show child attributes
- Active Optional Boolean , filterable , sortable If true, this entity is currently enabled for use by QuickBooks. If set to false, this entity is not available.
- MetaData Optional ModificationMetaData , filterable , sortable Descriptive information about the object. The MetaData values are set by Data Services and are read only for all applications. Show child attributes
- FullyQualifiedName read only  system defined String , filterable , sortable Fully qualified name of the entity. The fully qualified name prepends the topmost parent, followed by each sub element separated by colons. Takes the form of Parent:Department1:SubDepartment1:SubDepartment2. Limited to 5 levels.
- SubDepartment read only  system defined Boolean  , sortable Specifies whether this Department object is a SubDepartment.
true--SubDepartment.
false or null--top-level Department.

### Returns

The Department object response body.

Request URL

Request Body


### Sign in to explore our APIs

Returns

© 2025 Intuit Inc. All rights reserved. Intuit is a registered trademarks of Intuit Inc. Terms and conditions, features, support, pricing, and service options subject to change without notice.