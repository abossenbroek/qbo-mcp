# CustomerType


- < Back to Documentation
- Accounting All entities AccountAccountListDetailAPAgingDetailAPAgingSummaryARAgingDetailARAgingSummaryAttachableBalanceSheetBatchBillBillPaymentBudgetCashFlowChangeDataCaptureClassCompanyCurrencyCompanyInfoCreditMemoCreditCardPaymentCustomerCustomerBalanceCustomerBalanceDetailCustomerIncomeFECReportCustomerTypeThe CustomerType objectQuery a customertypeRead a customertypeDepartmentDepositEmployeeEntitlementsEstimateExchangerateGeneralLedgerGeneralLedgerFRInventoryAdjustmentInventoryValuationDetailInventoryValuationSummaryInvoiceItemJournalCodeJournalEntryJournalReportJournalReportFRPaymentPaymentMethodPreferencesProfitAndLossProfitAndLossDetailPurchasePurchaseOrderRecurringTransactionRefundReceiptReimburseChargeSalesByClassSummarySalesByCustomerSalesByDepartmentSalesByProductSalesReceiptTaxClassificationTaxCodeTaxPaymentTaxRateTaxServiceTaxSummaryTaxAgencyTermTimeActivityTransactionListTransactionListByVendorTransactionListByCustomerTransactionListWithSplitsTransferTrialBalanceVendorVendorBalanceVendorBalanceDetailVendorCreditVendorExpensesMost commonly usedE-CommerceReport entities

- All entities AccountAccountListDetailAPAgingDetailAPAgingSummaryARAgingDetailARAgingSummaryAttachableBalanceSheetBatchBillBillPaymentBudgetCashFlowChangeDataCaptureClassCompanyCurrencyCompanyInfoCreditMemoCreditCardPaymentCustomerCustomerBalanceCustomerBalanceDetailCustomerIncomeFECReportCustomerTypeThe CustomerType objectQuery a customertypeRead a customertypeDepartmentDepositEmployeeEntitlementsEstimateExchangerateGeneralLedgerGeneralLedgerFRInventoryAdjustmentInventoryValuationDetailInventoryValuationSummaryInvoiceItemJournalCodeJournalEntryJournalReportJournalReportFRPaymentPaymentMethodPreferencesProfitAndLossProfitAndLossDetailPurchasePurchaseOrderRecurringTransactionRefundReceiptReimburseChargeSalesByClassSummarySalesByCustomerSalesByDepartmentSalesByProductSalesReceiptTaxClassificationTaxCodeTaxPaymentTaxRateTaxServiceTaxSummaryTaxAgencyTermTimeActivityTransactionListTransactionListByVendorTransactionListByCustomerTransactionListWithSplitsTransferTrialBalanceVendorVendorBalanceVendorBalanceDetailVendorCreditVendorExpenses
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
- CustomerTypeThe CustomerType objectQuery a customertypeRead a customertype
- The CustomerType object
- Query a customertype
- Read a customertype

- Department
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


## The CustomerType object


- Id* Required for update  read only  system defined String , filterable , sortable Unique identifier for this object.
Sort order is ASC by default.
- SyncToken* Required for update  read only  system defined String  Version number of the object. It is used to lock an object for use by one app at a time. As soon as an application modifies an object, its SyncToken is incremented. Attempts to modify an object specifying an older SyncToken fails. Only the latest version of the object is maintained by QuickBooks Online.
- Name* Required for update  system defined String  The full name of the customer type.
- Active Optional Boolean , filterable , sortable Indicates whether this customer type is active in the company or not.
true--This customer type is active and enabled for use by QuickBooks.
false—This customer type is inactive, is hidden from most display purposes, and is not availble for use with financial transactions.
- MetaData Optional ModificationMetaData , filterable , sortable Descriptive information about the object. The MetaData values are set by Data Services and are read only for all applications. Show child attributes

SAMPLE OBJECT


## Query a customertype


### Returns

Returns the results of the query.

Request URL

Sample Query


### Sign in to explore our APIs

Returns


## Read a customertype


### Returns

Returns the Customertype object.

Returns the Customertype object.

Request URL


### Sign in to explore our APIs

Returns

© 2025 Intuit Inc. All rights reserved. Intuit is a registered trademarks of Intuit Inc. Terms and conditions, features, support, pricing, and service options subject to change without notice.