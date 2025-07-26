# QuickBooks Online API - Item Entity

## Entity Overview

The Item entity represents products and services that a business sells, purchases, or uses in its operations. Items in QuickBooks Online can be of different types including Service, Inventory, and NonInventory items.

### Item Types

- **Service**: Services offered to clients, typically charged by task or hourly rate
- **Inventory**: Physical products that are tracked in stock with quantity on hand
- **NonInventory**: Products or services that are not tracked as inventory
- **Category**: Used to group and organize items (subcategories supported)
- **Bundle**: A collection of items sold together (QuickBooks Online Plus only)

## Attributes Table

| Name | Type | Required | Description | Notes |
|------|------|----------|-------------|-------|
| Id | String | Read-only | Unique identifier for the item | System generated |
| SyncToken | String | Required for updates | Version control token | Prevents conflicting updates |
| Name | String | Required | Display name of the item | Maximum 100 characters |
| Active | Boolean | Optional | Whether the item is active | Default: true |
| Type | Enum | Required | Item type | Values: Inventory, Service, NonInventory, Category, Bundle |
| Description | String | Optional | Sales description | Maximum 4000 characters |
| FullyQualifiedName | String | Read-only | Full hierarchical name | System generated |
| Taxable | Boolean | Optional | Whether item is subject to sales tax | Default: false |
| UnitPrice | Decimal | Optional | Sales price per unit | |
| PurchaseDesc | String | Optional | Purchase description | Maximum 4000 characters |
| PurchaseCost | Decimal | Optional | Cost to purchase the item | |
| Sku | String | Optional | Stock keeping unit | |
| IncomeAccountRef | Reference | Conditional | Income account reference | Required for Service and NonInventory items |
| ExpenseAccountRef | Reference | Conditional | Expense account reference | Required for Inventory and NonInventory items |
| AssetAccountRef | Reference | Conditional | Asset account reference | Required for Inventory items |
| TrackQtyOnHand | Boolean | Conditional | Track inventory quantity | Required for Inventory items |
| QtyOnHand | Decimal | Conditional | Current quantity in stock | Read-only for Inventory items |
| InvStartDate | Date | Conditional | Inventory start date | Required when setting initial QtyOnHand |
| ReorderPoint | Decimal | Optional | Minimum quantity before reorder | Inventory items only |
| PurchaseTaxCodeRef | Reference | Optional | Purchase tax code reference | |
| SalesTaxCodeRef | Reference | Optional | Sales tax code reference | |
| PrefVendorRef | Reference | Optional | Preferred vendor reference | |
| ParentRef | Reference | Optional | Parent item reference | For sub-items |
| Level | Integer | Read-only | Hierarchy level | 0 for top-level items |
| PrintGroupedItems | Boolean | Optional | Print sub-items on forms | |
| SalesTaxIncluded | Boolean | Optional | Sales tax included in price | |
| PurchaseTaxIncluded | Boolean | Optional | Purchase tax included in cost | |
| MetaData | MetaData | Read-only | Creation and modification timestamps | |
| domain | String | Read-only | Always "QBO" | |
| sparse | Boolean | Optional | Sparse update indicator | |

### Reference Object Structure

```json
{
  "value": "string",  // ID of the referenced entity
  "name": "string"    // Display name of the referenced entity
}
```

## Sample JSON Responses

### Service Item
```json
{
  "Name": "Consulting Services",
  "Active": true,
  "FullyQualifiedName": "Consulting Services",
  "Taxable": false,
  "UnitPrice": 150.00,
  "Type": "Service",
  "IncomeAccountRef": {
    "value": "1",
    "name": "Services"
  },
  "Description": "Professional consulting services",
  "PurchaseCost": 0,
  "TrackQtyOnHand": false,
  "domain": "QBO",
  "sparse": false,
  "Id": "21",
  "SyncToken": "0",
  "MetaData": {
    "CreateTime": "2024-01-15T10:30:00-08:00",
    "LastUpdatedTime": "2024-01-15T10:30:00-08:00"
  }
}
```

### Inventory Item
```json
{
  "Name": "Widget Pro",
  "Description": "Professional-grade widget",
  "Active": true,
  "FullyQualifiedName": "Widget Pro",
  "Taxable": true,
  "UnitPrice": 25.00,
  "Type": "Inventory",
  "IncomeAccountRef": {
    "value": "79",
    "name": "Sales of Product Income"
  },
  "PurchaseDesc": "Widget for resale",
  "PurchaseCost": 15.00,
  "ExpenseAccountRef": {
    "value": "80",
    "name": "Cost of Goods Sold"
  },
  "AssetAccountRef": {
    "value": "81",
    "name": "Inventory Asset"
  },
  "TrackQtyOnHand": true,
  "QtyOnHand": 100,
  "InvStartDate": "2024-01-01",
  "ReorderPoint": 25,
  "domain": "QBO",
  "sparse": false,
  "Id": "11",
  "SyncToken": "3",
  "MetaData": {
    "CreateTime": "2024-01-01T09:00:00-08:00",
    "LastUpdatedTime": "2024-01-15T14:30:00-08:00"
  }
}
```

### NonInventory Item
```json
{
  "Name": "Shipping Supplies",
  "Active": true,
  "FullyQualifiedName": "Shipping Supplies",
  "Taxable": false,
  "UnitPrice": 5.00,
  "Type": "NonInventory",
  "IncomeAccountRef": {
    "value": "79",
    "name": "Sales of Product Income"
  },
  "ExpenseAccountRef": {
    "value": "82",
    "name": "Supplies"
  },
  "Description": "Boxes and packaging materials",
  "PurchaseCost": 3.00,
  "TrackQtyOnHand": false,
  "domain": "QBO",
  "sparse": false,
  "Id": "15",
  "SyncToken": "1",
  "MetaData": {
    "CreateTime": "2024-01-10T11:00:00-08:00",
    "LastUpdatedTime": "2024-01-10T11:00:00-08:00"
  }
}
```

## CRUD Operations

### Base URL
```
https://sandbox-quickbooks.api.intuit.com/v3/company/{companyId}/
```
For production, replace `sandbox-quickbooks` with `quickbooks`

### Create (POST)
**Endpoint:** `/item`

**Request:**
```http
POST /v3/company/{companyId}/item
Content-Type: application/json
Accept: application/json
Authorization: Bearer {accessToken}

{
  "Name": "New Product",
  "Type": "Service",
  "IncomeAccountRef": {
    "value": "1"
  }
}
```

### Read (GET)
**Single Item:** `/item/{itemId}`

**Request:**
```http
GET /v3/company/{companyId}/item/{itemId}
Accept: application/json
Authorization: Bearer {accessToken}
```

**Query Items:** `/query?query={query}`

**Request:**
```http
GET /v3/company/{companyId}/query?query=select * from Item where Active = true
Accept: application/json
Authorization: Bearer {accessToken}
```

### Update (POST)
**Endpoint:** `/item`

**Request:**
```http
POST /v3/company/{companyId}/item
Content-Type: application/json
Accept: application/json
Authorization: Bearer {accessToken}

{
  "Id": "11",
  "SyncToken": "3",
  "Name": "Updated Product Name",
  "UnitPrice": 30.00
}
```

### Delete (POST)
Items cannot be permanently deleted. Set `Active` to `false` to deactivate.

**Request:**
```http
POST /v3/company/{companyId}/item
Content-Type: application/json
Accept: application/json
Authorization: Bearer {accessToken}

{
  "Id": "11",
  "SyncToken": "4",
  "Active": false
}
```

## Query Examples

### Get all active inventory items
```
select * from Item where Type = 'Inventory' and Active = true
```

### Get items by name pattern
```
select * from Item where Name like 'Widget%'
```

### Get items with low stock
```
select * from Item where Type = 'Inventory' and QtyOnHand < ReorderPoint
```

### Filter Service and NonInventory items
```
select * from Item where Type IN ('Service', 'NonInventory')
```
Note: Use `minorversion=42` or higher for correct filtering results

## Special Notes and Limitations

1. **Item Types Cannot Be Changed**: Once created, you cannot change an Inventory item to a different type. You can only change between Service and NonInventory types.

2. **Inventory Tracking**: Inventory tracking is only available in QuickBooks Online Plus and Advanced subscriptions.

3. **Account References**: 
   - Service items require `IncomeAccountRef`
   - NonInventory items require both `IncomeAccountRef` and `ExpenseAccountRef`
   - Inventory items require `IncomeAccountRef`, `ExpenseAccountRef`, and `AssetAccountRef`

4. **Quantity Management**: 
   - QtyOnHand is read-only and updated through inventory adjustment transactions
   - Initial quantity can be set using `InvStartDate` and `QtyOnHand` when creating the item

5. **Bundle Items**: Only available in QuickBooks Online Plus and Advanced

6. **Maximum Limits**:
   - Name: 100 characters
   - Description: 4000 characters
   - SKU: 100 characters

7. **Sparse Updates**: Set `sparse=true` to update only specified fields

8. **SyncToken**: Always required for updates to prevent conflicting changes

9. **Sub-items**: Use `ParentRef` to create hierarchical item structures

10. **Tax Handling**: Tax-inclusive pricing available in certain regions only

## Error Handling

Common error codes:
- `6000`: A business validation error has occurred (check required fields)
- `5010`: Stale object error (SyncToken mismatch)
- `2050`: Invalid reference (check account references)
- `610`: Object not found

## Additional Resources

- [Items and Inventory in QuickBooks Online](https://developer.intuit.com/app/developer/qbo/docs/learn/learn-basic-bookkeeping/manage-inventory)
- [Create Products, Services, and Inventory Items Workflow](https://developer.intuit.com/app/developer/qbo/docs/workflows/manage-inventory)
- [QuickBooks Online API Reference](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/item)