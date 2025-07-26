# Preferences

The Preferences entity contains company-wide settings and preferences for QuickBooks Online.

## Operations

### Read
Retrieve the current company preferences.

#### Request
```
GET /v3/company/{companyId}/preferences
```

#### Response
```json
{
  "Preferences": {
    "AccountingInfoPrefs": {
      "TrackDepartments": true,
      "DepartmentTerminology": "Department",
      "ClassTrackingPerTxn": false,
      "ClassTrackingPerTxnLine": true,
      "CustomerTerminology": "Customers"
    },
    "ProductAndServicesPrefs": {
      "ForSales": true,
      "ForPurchase": true,
      "QuantityWithPriceAndRate": true,
      "QuantityOnHand": true
    },
    "SalesFormsPrefs": {
      "CustomField": [
        {
          "Name": "SalesFormsPrefs.UseSalesCustom3",
          "Type": "BooleanType",
          "BooleanValue": false
        },
        {
          "Name": "SalesFormsPrefs.UseSalesCustom2",
          "Type": "BooleanType",
          "BooleanValue": false
        },
        {
          "Name": "SalesFormsPrefs.UseSalesCustom1",
          "Type": "BooleanType",
          "BooleanValue": true
        }
      ],
      "CustomTxnNumbers": false,
      "AllowDeposit": false,
      "AllowDiscount": true,
      "AllowEstimates": true,
      "ETransactionEnabledStatus": "NotApplicable",
      "IPNSupportEnabled": false,
      "AllowServiceDate": false,
      "AllowShipping": false,
      "DefaultTerms": {
        "value": "3"
      }
    },
    "EmailMessagesPrefs": {
      "InvoiceMessage": {
        "Subject": "Invoice from {CompanyName}",
        "Message": "Your invoice is attached. Please remit payment at your earliest convenience."
      },
      "EstimateMessage": {
        "Subject": "Estimate from {CompanyName}",
        "Message": "Please review the estimate below. Feel free to contact us if you have any questions."
      },
      "SalesReceiptMessage": {
        "Subject": "Sales Receipt from {CompanyName}",
        "Message": "Your sales receipt is attached."
      }
    },
    "VendorAndPurchasesPrefs": {
      "TrackingByCustomer": true,
      "BillableExpenseTracking": true,
      "DefaultTerms": {
        "value": "3"
      }
    },
    "TimeTrackingPrefs": {
      "UseServices": true,
      "BillCustomers": true,
      "ShowBillRateToAll": false,
      "MarkTimeEntriesBillable": true
    },
    "TaxPrefs": {
      "UsingSalesTax": true,
      "TaxGroupCodeRef": {
        "value": "2"
      }
    },
    "CurrencyPrefs": {
      "MultiCurrencyEnabled": false,
      "HomeCurrency": {
        "value": "USD"
      }
    },
    "OtherPrefs": {
      "NameValue": [
        {
          "Name": "SalesFormsPrefs.DefaultCustomerMessage",
          "Value": ""
        },
        {
          "Name": "SalesFormsPrefs.DefaultItem",
          "Value": "1"
        }
      ]
    },
    "MetaData": {
      "CreateTime": "2015-07-24T10:33:39-07:00",
      "LastUpdatedTime": "2015-07-24T10:58:01-07:00"
    },
    "Id": "1",
    "SyncToken": "6"
  },
  "time": "2015-07-24T10:58:01.544-07:00"
}
```

### Update
Update company preferences.

#### Request
```
POST /v3/company/{companyId}/preferences
```

#### Request Body
```json
{
  "SalesFormsPrefs": {
    "AllowDeposit": true,
    "AllowDiscount": true,
    "DefaultTerms": {
      "value": "3"
    }
  },
  "EmailMessagesPrefs": {
    "InvoiceMessage": {
      "Subject": "Invoice from {CompanyName}",
      "Message": "Your invoice is attached. Please remit payment at your earliest convenience."
    }
  },
  "SyncToken": "6"
}
```

## Fields

### AccountingInfoPrefs
- `TrackDepartments` - Enable department tracking
- `DepartmentTerminology` - Terminology used for departments
- `ClassTrackingPerTxn` - Track classes per transaction
- `ClassTrackingPerTxnLine` - Track classes per transaction line
- `CustomerTerminology` - Terminology used for customers

### ProductAndServicesPrefs
- `ForSales` - Enable products/services for sales
- `ForPurchase` - Enable products/services for purchases
- `QuantityWithPriceAndRate` - Track quantity with price and rate
- `QuantityOnHand` - Track quantity on hand

### SalesFormsPrefs
- `CustomTxnNumbers` - Enable custom transaction numbers
- `AllowDeposit` - Allow deposits on invoices
- `AllowDiscount` - Allow discounts
- `AllowEstimates` - Enable estimates
- `DefaultTerms` - Default payment terms

### VendorAndPurchasesPrefs
- `TrackingByCustomer` - Track expenses by customer
- `BillableExpenseTracking` - Track billable expenses
- `DefaultTerms` - Default payment terms for bills

### TimeTrackingPrefs
- `UseServices` - Use service items for time tracking
- `BillCustomers` - Mark time entries as billable
- `MarkTimeEntriesBillable` - Default time entries to billable

### TaxPrefs
- `UsingSalesTax` - Sales tax enabled
- `TaxGroupCodeRef` - Default tax code

### CurrencyPrefs
- `MultiCurrencyEnabled` - Multi-currency feature status
- `HomeCurrency` - Home currency code

## Notes
- Preferences are company-wide settings
- Only specific preference groups can be updated
- SyncToken is required for updates
- Some preferences may be read-only depending on subscription level