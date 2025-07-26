# QuickBooks Online API Documentation Index

This index provides quick access to all 77 QuickBooks Online API entities documentation.

## Core Entities

### Customer & Sales
- [Customer](entities/customer.md) - Customer management
- [CustomerType](entities/customertype.md) - Customer categorization
- [Invoice](entities/invoice.md) - Sales invoices
- [Estimate](entities/estimate.md) - Sales estimates
- [SalesReceipt](entities/salesreceipt.md) - Sales receipts
- [Payment](entities/payment.md) - Customer payments
- [CreditMemo](entities/creditmemo.md) - Credit memo transactions
- [RefundReceipt](entities/refundreceipt.md) - Refund receipts
- [Deposit](entities/deposit.md) - Bank deposits

### Vendor & Expenses
- [Vendor](entities/vendor.md) - Vendor management
- [Bill](entities/bill.md) - Vendor bills
- [BillPayment](entities/billpayment.md) - Bill payment transactions
- [Purchase](entities/purchase.md) - Purchase transactions
- [PurchaseOrder](entities/purchaseorder.md) - Purchase orders
- [VendorCredit](entities/vendorcredit.md) - Vendor credits
- [CreditCardPayment](entities/creditcardpayment.md) - Credit card payments
- [ReimburseCharge](entities/reimbursecharge.md) - Reimbursable charges

### Items & Inventory
- [Item](entities/item.md) - Products and services
- [InventoryAdjustment](entities/inventoryadjustment.md) - Inventory adjustments

### Banking & Financial
- [Account](entities/account.md) - Chart of accounts
- [Transfer](entities/transfer.md) - Bank transfers
- [JournalEntry](entities/journalentry.md) - Journal entries
- [JournalCode](entities/journalcode.md) - Journal codes (France)

### Employees & Time Tracking
- [Employee](entities/employee.md) - Employee management
- [TimeActivity](entities/timeactivity.md) - Time tracking activities

### Organization & Settings
- [CompanyInfo](entities/companyinfo.md) - Company information
- [Preferences](entities/preferences.md) - Company preferences
- [Class](entities/class.md) - Classification tracking
- [Department](entities/department.md) - Department tracking
- [PaymentMethod](entities/paymentmethod.md) - Payment method configuration
- [Term](entities/term.md) - Payment terms

### Tax Management
- [TaxAgency](entities/taxagency.md) - Tax agencies
- [TaxCode](entities/taxcode.md) - Tax codes
- [TaxRate](entities/taxrate.md) - Tax rate definitions
- [TaxClassification](entities/taxclassification.md) - Tax classifications
- [TaxService](entities/taxservice.md) - Tax calculation services
- [TaxPayment](entities/taxpayment.md) - Tax payment records

### Multi-Currency
- [CompanyCurrency](entities/companycurrency.md) - Multi-currency support
- [ExchangeRate](entities/exchangerate.md) - Currency exchange rates

### Advanced Features
- [RecurringTransaction](entities/recurringtransaction.md) - Recurring transaction templates
- [Attachable](entities/attachable.md) - File attachment management
- [Batch](entities/batch.md) - Batch operations
- [Budget](entities/budget.md) - Budget management
- [ChangedDataCapture](entities/changedatacapture.md) - Change tracking
- [Entitlements](entities/entitlements.md) - Feature entitlements

## Reports

### Financial Reports
- [BalanceSheet](entities/balancesheet.md) - Balance Sheet report
- [ProfitAndLoss](entities/profitandloss.md) - Profit and Loss report
- [ProfitAndLossDetail](entities/profitandlossdetail.md) - Detailed P&L report
- [CashFlow](entities/cashflow.md) - Cash Flow report
- [TrialBalance](entities/trialbalance.md) - Trial Balance report
- [GeneralLedger](entities/generalledger.md) - General Ledger report
- [GeneralLedgerFR](entities/generalledgerfr.md) - General Ledger (French)
- [JournalReport](entities/journalreport.md) - Journal report
- [JournalReportFR](entities/journalreportfr.md) - Journal report (French)

### Accounts Receivable Reports
- [ARAgingSummary](entities/aragingsummary.md) - AR Aging Summary report
- [ARAgingDetail](entities/aragingdetail.md) - AR Aging Detail report
- [CustomerBalance](entities/customerbalance.md) - Customer balance report
- [CustomerBalanceDetail](entities/customerbalancedetail.md) - Customer balance detail report
- [CustomerIncome](entities/customerincome.md) - Customer income report

### Accounts Payable Reports
- [APAgingSummary](entities/apagingsummary.md) - AP Aging Summary report
- [APAgingDetail](entities/apagingdetail.md) - AP Aging Detail report
- [VendorBalance](entities/vendorbalance.md) - Vendor balance report
- [VendorBalanceDetail](entities/vendorbalancedetail.md) - Detailed vendor balance report
- [VendorExpenses](entities/vendorexpenses.md) - Vendor expenses report

### Sales Reports
- [SalesByClassSummary](entities/salesbyclasssummary.md) - Sales by class summary report
- [SalesByCustomer](entities/salesbycustomer.md) - Sales by customer report
- [SalesByDepartment](entities/salesbydepartment.md) - Sales by department report
- [SalesByProduct](entities/salesbyproduct.md) - Sales by product report

### Transaction Reports
- [TransactionList](entities/transactionlist.md) - Transaction list report
- [TransactionListByVendor](entities/transactionlistbyvendor.md) - Vendor transaction report
- [TransactionListByCustomer](entities/transactionlistbycustomer.md) - Customer transaction report
- [TransactionListWithSplits](entities/transactionlistwithsplits.md) - Detailed transaction report

### Inventory Reports
- [InventoryValuationSummary](entities/inventoryvaluationsummary.md) - Inventory valuation summary
- [InventoryValuationDetail](entities/inventoryvaluationdetail.md) - Inventory valuation detail

### Tax Reports
- [TaxSummary](entities/taxsummary.md) - Tax summary report

### Other Reports
- [AccountListDetail](entities/accountlistdetail.md) - Account list detail report
- [FECReport](entities/fecreport.md) - FEC report (French)

## Additional Resources

- [Scraping Summary](scraping_summary.md) - Documentation collection progress and details
- [QuickBooks API Reference](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities) - Official API documentation

## Usage Notes

Each entity documentation includes:
- Entity description and purpose
- Available API operations (Create, Read, Update, Delete, Query)
- Request/response examples with JSON formatting
- Query parameters and filtering options
- Field definitions and requirements
- Common use cases and implementation examples
- Important notes and limitations

For the most up-to-date information, always refer to the official QuickBooks Online API documentation.