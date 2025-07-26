# Budget

The budget resource provides create and query operations.

## The budget object

### Attributes

| Attribute | Type | Description |
|-----------|------|-------------|
| **Id** | String | Read only, system defined. Unique identifier for this object. |
| **Name** | String | **Required**. User recognizable name for the budget. |
| **StartDate** | Date | **Required**. Start date for the budget. |
| **EndDate** | Date | **Required**. End date for the budget. |
| **BudgetType** | BudgetTypeEnum | **Required**. Profit and Loss budget type. |
| **Active** | Boolean | Optional. Indicates whether budget is active. Inactive budgets are hidden from most views. |
| **BudgetDetail** | BudgetDetail | **Required**. Holds the budget amount and account info. |
| **SyncToken** | String | **Required for update**. Version number of the object. It is used to lock an object for use by one app at a time. As soon as an application modifies an object, its SyncToken is incremented. |
| **MetaData** | ModificationMetaData | Optional. Descriptive information about the object. The MetaData values are set by Data Services and are read only for all applications. |

## Operations

### Create a budget

Creates a new Budget object.

**Required fields:**
- Name
- StartDate
- EndDate
- BudgetType
- BudgetDetail (containing budget amounts and account information)

### Query a budget

Returns the results of the query for Budget objects.

Note: The Budget API currently only supports create and query operations. Update and delete operations are not available for Budget objects.