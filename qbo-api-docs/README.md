# QuickBooks Online REST API Documentation

This repository contains a comprehensive offline reference of the QuickBooks Online REST API documentation, scraped from the official Intuit Developer portal.

## Table of Contents

### Core Accounting Entities
- [Account](entities/account.md) - Chart of accounts management
- [JournalEntry](entities/journalentry.md) - Manual journal entries
- [JournalCode](entities/journalcode.md) - Journal codes for categorization
- [Transfer](entities/transfer.md) - Money transfers between accounts

### Sales Entities
- [Customer](entities/customer.md) - Customer records
- [CustomerType](entities/customertype.md) - Customer categorization
- [Invoice](entities/invoice.md) - Sales invoices
- [Estimate](entities/estimate.md) - Sales estimates/quotes
- [SalesReceipt](entities/salesreceipt.md) - Point of sale transactions
- [Payment](entities/payment.md) - Customer payments
- [CreditMemo](entities/creditmemo.md) - Credit memos for customers
- [RefundReceipt](entities/refundreceipt.md) - Customer refunds
- [Deposit](entities/deposit.md) - Bank deposits
- [ReimburseCharge](entities/reimbursecharge.md) - Reimbursable charges

### Purchase Entities
- [Vendor](entities/vendor.md) - Vendor/supplier records
- [Bill](entities/bill.md) - Vendor bills
- [BillPayment](entities/billpayment.md) - Bill payments
- [Purchase](entities/purchase.md) - Direct purchases
- [PurchaseOrder](entities/purchaseorder.md) - Purchase orders
- [VendorCredit](entities/vendorcredit.md) - Vendor credits
- [CreditCardPayment](entities/creditcardpayment.md) - Credit card payments

### Item & Inventory Entities
- [Item](entities/item.md) - Products and services
- [InventoryAdjustment](entities/inventoryadjustment.md) - Inventory adjustments
- [InventoryValuationSummary](entities/inventoryvaluationsummary.md) - Inventory valuation summary
- [InventoryValuationDetail](entities/inventoryvaluationdetail.md) - Detailed inventory valuation

### Employee & Time Tracking
- [Employee](entities/employee.md) - Employee records
- [TimeActivity](entities/timeactivity.md) - Time tracking entries

### Tax Entities
- [TaxAgency](entities/taxagency.md) - Tax agencies
- [TaxCode](entities/taxcode.md) - Tax codes
- [TaxRate](entities/taxrate.md) - Tax rates
- [TaxPayment](entities/taxpayment.md) - Tax payments
- [TaxClassification](entities/taxclassification.md) - Tax classifications
- [TaxService](entities/taxservice.md) - Tax calculation service
- [TaxSummary](entities/taxsummary.md) - Tax summary reports

### Reports - Financial Statements
- [BalanceSheet](entities/balancesheet.md) - Balance sheet report
- [ProfitAndLoss](entities/profitandloss.md) - Income statement
- [ProfitAndLossDetail](entities/profitandlossdetail.md) - Detailed P&L
- [CashFlow](entities/cashflow.md) - Cash flow statement
- [TrialBalance](entities/trialbalance.md) - Trial balance report

### Reports - Ledgers & Journals
- [GeneralLedger](entities/generalledger.md) - General ledger report
- [GeneralLedgerFR](entities/generalledgerfr.md) - General ledger (French format)
- [JournalReport](entities/journalreport.md) - Journal report
- [JournalReportFR](entities/journalreportfr.md) - Journal report (French format)
- [FECReport](entities/fecreport.md) - FEC report (French compliance)

### Reports - Aging & Balances
- [ARAgingSummary](entities/aragingsummary.md) - Accounts receivable aging summary
- [ARAgingDetail](entities/aragingdetail.md) - Accounts receivable aging detail
- [APAgingSummary](entities/apagingsummary.md) - Accounts payable aging summary
- [APAgingDetail](entities/apagingdetail.md) - Accounts payable aging detail
- [CustomerBalance](entities/customerbalance.md) - Customer balances
- [CustomerBalanceDetail](entities/customerbalancedetail.md) - Detailed customer balances
- [VendorBalance](entities/vendorbalance.md) - Vendor balances
- [VendorBalanceDetail](entities/vendorbalancedetail.md) - Detailed vendor balances

### Reports - Sales Analysis
- [SalesByCustomer](entities/salesbycustomer.md) - Sales by customer report
- [SalesByProduct](entities/salesbyproduct.md) - Sales by product report
- [SalesByClassSummary](entities/salesbyclasssummary.md) - Sales by class summary
- [SalesByDepartment](entities/salesbydepartment.md) - Sales by department
- [CustomerIncome](entities/customerincome.md) - Customer income report
- [VendorExpenses](entities/vendorexpenses.md) - Vendor expenses report

### Reports - Transaction Lists
- [TransactionList](entities/transactionlist.md) - General transaction list
- [TransactionListByCustomer](entities/transactionlistbycustomer.md) - Transactions by customer
- [TransactionListByVendor](entities/transactionlistbyvendor.md) - Transactions by vendor
- [TransactionListWithSplits](entities/transactionlistwithsplits.md) - Transactions with split details
- [AccountListDetail](entities/accountlistdetail.md) - Account list with details

### Organization & Setup
- [CompanyInfo](entities/companyinfo.md) - Company information
- [Preferences](entities/preferences.md) - Company preferences
- [Class](entities/class.md) - Classes for tracking
- [Department](entities/department.md) - Departments
- [PaymentMethod](entities/paymentmethod.md) - Payment methods
- [Term](entities/term.md) - Payment terms
- [CompanyCurrency](entities/companycurrency.md) - Multi-currency setup
- [ExchangeRate](entities/exchangerate.md) - Currency exchange rates
- [Budget](entities/budget.md) - Budget management
- [RecurringTransaction](entities/recurringtransaction.md) - Recurring transactions

### System & Utilities
- [Attachable](entities/attachable.md) - File attachments
- [Batch](entities/batch.md) - Batch operations
- [ChangeDataCapture](entities/changedatacapture.md) - Change tracking
- [Entitlements](entities/entitlements.md) - Feature entitlements

## Usage

Each entity documentation includes:
- Object schema and field descriptions
- Supported operations (Create, Read, Update, Delete, Query)
- Request/response examples
- Business rules and validations
- Related entities and workflows

## Source

This documentation was scraped from the official QuickBooks Online API documentation at:
https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/

## License

This documentation is provided for reference purposes. Please refer to Intuit's official documentation and terms of service for the most up-to-date information and licensing details.