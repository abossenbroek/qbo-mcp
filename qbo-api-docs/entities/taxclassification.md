# TaxClassification

The TaxClassification entity represents tax classifications used for automated sales tax calculation.

## Operations

### Query
Retrieve tax classifications.

#### Request
```
GET /v3/company/{companyId}/query?query=select * from TaxClassification
```

#### Response
```json
{
  "QueryResponse": {
    "TaxClassification": [
      {
        "Id": "EUC-99990201-V1-00020000",
        "Name": "Clothing",
        "Description": "Clothing and apparel items",
        "ParentRef": {
          "value": "EUC-99990201-V1-00020000"
        },
        "Level": 1,
        "Active": true,
        "MetaData": {
          "CreateTime": "2025-01-15T10:00:00-08:00",
          "LastUpdatedTime": "2025-01-15T10:00:00-08:00"
        }
      },
      {
        "Id": "EUC-99990201-V1-00020001",
        "Name": "Children's Clothing",
        "Description": "Clothing for children",
        "ParentRef": {
          "value": "EUC-99990201-V1-00020000"
        },
        "Level": 2,
        "Active": true,
        "MetaData": {
          "CreateTime": "2025-01-15T10:00:00-08:00",
          "LastUpdatedTime": "2025-01-15T10:00:00-08:00"
        }
      },
      {
        "Id": "EUC-99990201-V1-00060000",
        "Name": "Food & Beverages",
        "Description": "Food and beverage products",
        "Level": 1,
        "Active": true,
        "MetaData": {
          "CreateTime": "2025-01-15T10:00:00-08:00",
          "LastUpdatedTime": "2025-01-15T10:00:00-08:00"
        }
      },
      {
        "Id": "EUC-99990201-V1-00060100",
        "Name": "Prepared Food",
        "Description": "Ready-to-eat food items",
        "ParentRef": {
          "value": "EUC-99990201-V1-00060000"
        },
        "Level": 2,
        "Active": true,
        "MetaData": {
          "CreateTime": "2025-01-15T10:00:00-08:00",
          "LastUpdatedTime": "2025-01-15T10:00:00-08:00"
        }
      },
      {
        "Id": "EUC-99990201-V1-00080000",
        "Name": "Medical",
        "Description": "Medical supplies and equipment",
        "Level": 1,
        "Active": true,
        "MetaData": {
          "CreateTime": "2025-01-15T10:00:00-08:00",
          "LastUpdatedTime": "2025-01-15T10:00:00-08:00"
        }
      }
    ],
    "startPosition": 1,
    "maxResults": 5,
    "totalCount": 100
  },
  "time": "2025-01-15T10:30:00.000-08:00"
}
```

### Read
Retrieve a specific tax classification by ID.

#### Request
```
GET /v3/company/{companyId}/taxclassification/{taxClassificationId}
```

## Fields

- `Id` - Unique identifier for the tax classification
- `Name` - Name of the tax classification
- `Description` - Detailed description
- `ParentRef` - Reference to parent classification (for hierarchical structure)
- `Level` - Hierarchy level (1 for top-level, 2 for sub-classification, etc.)
- `Active` - Whether the classification is active

## Common Tax Classifications

### Products
- **Clothing** - General apparel
  - Children's Clothing
  - Adult Clothing
  - Footwear
- **Food & Beverages**
  - Prepared Food
  - Grocery Items
  - Candy & Snacks
  - Soft Drinks
- **Medical**
  - Prescription Drugs
  - Medical Devices
  - Over-the-Counter Drugs

### Services
- **Professional Services**
  - Legal Services
  - Accounting Services
  - Consulting
- **Personal Services**
  - Hair Salon
  - Spa Services
  - Fitness Training

## Usage with Items

Assign tax classification to items:
```json
{
  "Item": {
    "Name": "T-Shirt",
    "Type": "Inventory",
    "TaxClassificationRef": {
      "value": "EUC-99990201-V1-00020000"
    }
  }
}
```

## Automated Sales Tax

Tax classifications work with Automated Sales Tax (AST) to:
- Determine correct tax rates
- Apply exemptions
- Handle special tax rules
- Calculate tax across jurisdictions

## Notes
- Tax classifications are provided by tax service providers
- Cannot create or modify classifications via API
- Used only with Automated Sales Tax enabled
- Classifications may vary by region/country
- Hierarchical structure allows specific tax treatment
- Essential for accurate tax calculation on products/services