# TaxSummary

The TaxSummary report provides a comprehensive overview of tax collected and owed for a specified period.

## Operations

### Query
Retrieve tax summary report data.

#### Request
```
GET /v3/company/{companyId}/reports/TaxSummary
```

#### Parameters
- `start_date` (string, required): Start date for the report period (YYYY-MM-DD)
- `end_date` (string, required): End date for the report period (YYYY-MM-DD)
- `accounting_method` (string): Accounting method - Cash or Accrual (default: Accrual)
- `tax_agency` (string): Filter by specific tax agency ID

#### Response
```json
{
  "Header": {
    "Time": "2025-01-15T10:30:00-08:00",
    "ReportName": "TaxSummary",
    "ReportBasis": "Accrual",
    "StartPeriod": "2025-01-01",
    "EndPeriod": "2025-01-31",
    "Currency": "USD",
    "Option": [
      {
        "Name": "NoReportData",
        "Value": "false"
      }
    ]
  },
  "Columns": {
    "Column": [
      {
        "ColTitle": "Tax Name",
        "ColType": "Account",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "tax_name"
          }
        ]
      },
      {
        "ColTitle": "Tax Agency",
        "ColType": "String",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "tax_agency"
          }
        ]
      },
      {
        "ColTitle": "Rate",
        "ColType": "Percent",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "tax_rate"
          }
        ]
      },
      {
        "ColTitle": "Gross Sales",
        "ColType": "Money",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "gross_sales"
          }
        ]
      },
      {
        "ColTitle": "Non-Taxable",
        "ColType": "Money",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "non_taxable"
          }
        ]
      },
      {
        "ColTitle": "Taxable",
        "ColType": "Money",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "taxable_amount"
          }
        ]
      },
      {
        "ColTitle": "Tax Collected",
        "ColType": "Money",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "tax_collected"
          }
        ]
      },
      {
        "ColTitle": "Tax Owed",
        "ColType": "Money",
        "MetaData": [
          {
            "Name": "ColKey",
            "Value": "tax_owed"
          }
        ]
      }
    ]
  },
  "Rows": {
    "Row": [
      {
        "Header": {
          "ColData": [
            {
              "value": "Sales Tax"
            }
          ]
        },
        "Rows": {
          "Row": [
            {
              "ColData": [
                {
                  "value": "California State Tax",
                  "id": "3"
                },
                {
                  "value": "California State Board of Equalization",
                  "id": "1"
                },
                {
                  "value": "7.25%"
                },
                {
                  "value": "50000.00"
                },
                {
                  "value": "5000.00"
                },
                {
                  "value": "45000.00"
                },
                {
                  "value": "3262.50"
                },
                {
                  "value": "3262.50"
                }
              ],
              "type": "Data"
            },
            {
              "ColData": [
                {
                  "value": "County Tax",
                  "id": "4"
                },
                {
                  "value": "Santa Clara County",
                  "id": "2"
                },
                {
                  "value": "1.00%"
                },
                {
                  "value": "50000.00"
                },
                {
                  "value": "5000.00"
                },
                {
                  "value": "45000.00"
                },
                {
                  "value": "450.00"
                },
                {
                  "value": "450.00"
                }
              ],
              "type": "Data"
            }
          ]
        },
        "Summary": {
          "ColData": [
            {
              "value": "Total Sales Tax"
            },
            {
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": "50000.00"
            },
            {
              "value": "5000.00"
            },
            {
              "value": "45000.00"
            },
            {
              "value": "3712.50"
            },
            {
              "value": "3712.50"
            }
          ]
        },
        "type": "Section",
        "group": "SalesTax"
      },
      {
        "Header": {
          "ColData": [
            {
              "value": "Purchases Tax"
            }
          ]
        },
        "Rows": {
          "Row": [
            {
              "ColData": [
                {
                  "value": "Purchase Tax",
                  "id": "5"
                },
                {
                  "value": "California State Board of Equalization",
                  "id": "1"
                },
                {
                  "value": "7.25%"
                },
                {
                  "value": "10000.00"
                },
                {
                  "value": "2000.00"
                },
                {
                  "value": "8000.00"
                },
                {
                  "value": "580.00"
                },
                {
                  "value": "-580.00"
                }
              ],
              "type": "Data"
            }
          ]
        },
        "Summary": {
          "ColData": [
            {
              "value": "Total Purchases Tax"
            },
            {
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": "10000.00"
            },
            {
              "value": "2000.00"
            },
            {
              "value": "8000.00"
            },
            {
              "value": "580.00"
            },
            {
              "value": "-580.00"
            }
          ]
        },
        "type": "Section",
        "group": "PurchasesTax"
      },
      {
        "Header": {
          "ColData": [
            {
              "value": "Adjustments"
            }
          ]
        },
        "Rows": {
          "Row": [
            {
              "ColData": [
                {
                  "value": "Tax Adjustment",
                  "id": "6"
                },
                {
                  "value": "California State Board of Equalization",
                  "id": "1"
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": ""
                },
                {
                  "value": "-50.00"
                },
                {
                  "value": "-50.00"
                }
              ],
              "type": "Data"
            }
          ]
        },
        "Summary": {
          "ColData": [
            {
              "value": "Total Adjustments"
            },
            {
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": "-50.00"
            },
            {
              "value": "-50.00"
            }
          ]
        },
        "type": "Section",
        "group": "Adjustments"
      },
      {
        "Summary": {
          "ColData": [
            {
              "value": "NET TAX OWED"
            },
            {
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": ""
            },
            {
              "value": "3082.50"
            }
          ]
        },
        "type": "Section",
        "group": "NetTaxOwed"
      }
    ]
  }
}
```

## Report Sections

### Sales Tax
- Shows tax collected on sales
- Grouped by tax rate/agency
- Includes gross sales, non-taxable, and taxable amounts

### Purchases Tax
- Shows tax paid on purchases
- Can be used for input tax credits
- Negative values reduce tax owed

### Adjustments
- Manual tax adjustments
- Corrections and amendments
- Credit/debit adjustments

### Net Tax Owed
- Final amount owed to tax agencies
- Sales tax minus purchase tax minus adjustments

## Column Definitions

- **Tax Name** - Name of the tax rate
- **Tax Agency** - Agency collecting the tax
- **Rate** - Tax percentage rate
- **Gross Sales** - Total sales including non-taxable
- **Non-Taxable** - Exempt or non-taxable sales
- **Taxable** - Amount subject to tax
- **Tax Collected** - Tax collected on sales
- **Tax Owed** - Net tax liability

## Tax Filing Workflow

1. **Generate Report**
   - Run for filing period
   - Review all transactions

2. **Make Adjustments**
   - Add any manual adjustments
   - Correct any errors

3. **File Return**
   - Use report data for filing
   - Record filing information

4. **Make Payment**
   - Create TaxPayment entry
   - Reference tax agency

## Notes
- Essential for tax compliance
- Basis (cash/accrual) affects timing
- Groups by tax agency for filing
- Shows both collected and paid taxes
- Includes adjustments for corrections
- Net amount shows liability/credit