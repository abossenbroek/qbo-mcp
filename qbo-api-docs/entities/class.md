# Class

A class is a way to track different segments of your business, so you can get sales and expense reports by class. For construction companies, this may be by job, for retailers by location, or for consultants by client.

## The class object

### Attributes

| Attribute | Type | Description |
|-----------|------|-------------|
| **Id** | String | Read only, system defined. Unique identifier for this object. |
| **Name** | String | **Required**. User recognizable name for the class. |
| **SubClass** | Boolean | Optional. Specifies whether this class is a parent (false) or a sub-class (true). Default value is false. |
| **ParentRef** | ReferenceType | **Conditionally required**. Required if SubClass is true. Reference to the parent class. Query the Class name list resource to determine the appropriate Class object for this reference. |
| **FullyQualifiedName** | String | Optional. Fully qualified name of the class. System generated. For a top-level class, this is the same as Name. For a subclass, this is the parent class name followed by colon, followed by the subclass name. |
| **Active** | Boolean | Optional. Whether or not the class is active. Inactive class will not show up in transaction forms. Default value is true. |
| **SyncToken** | String | **Required for update**. Version number of the object. It is used to lock an object for use by one app at a time. |
| **MetaData** | ModificationMetaData | Optional. Descriptive information about the object. The MetaData values are set by Data Services and are read only for all applications. |

## Operations

### Create a class

Creates a new Class object.

**Required fields:**
- Name

**Optional fields:**
- SubClass (if true, ParentRef is required)
- Active

### Query a class

Returns the results of the query for Class objects.

**Example query:**
```
SELECT * FROM Class WHERE Active = true
```

### Read a class

Retrieves the details of a Class that has been previously created.

### Update a class

Updates an existing Class object.

**Required fields:**
- Id
- SyncToken
- Name

**Note:** You cannot change a class from a parent to a subclass or vice versa after creation.

## Use Cases

Classes are commonly used for:
- **Construction**: Track income and expenses by job or project
- **Retail**: Separate financial data by store location
- **Consulting**: Organize data by client or engagement
- **Non-profit**: Track funds by program or grant

## Best Practices

1. **Plan your class structure** before creating classes, as the hierarchy cannot be changed later
2. **Use consistent naming conventions** for easier reporting
3. **Keep the hierarchy simple** - QuickBooks Online supports only one level of subclasses
4. **Deactivate unused classes** rather than deleting them to preserve historical data