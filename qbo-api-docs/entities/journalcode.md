# JournalCode Entity - QuickBooks Online API

## Overview

The JournalCode entity is a **France (FR) locale-specific** entity in the QuickBooks Online API. This entity is part of the NAME LIST ENTITIES category and is only available for QuickBooks Online companies set up with the French locale.

**Important Note**: This entity is exclusively available for FR locale and is not accessible in other locales.

## Entity Description

JournalCode represents journal codes used in the French accounting system. This entity is designed to support French accounting requirements and compliance with the French chart of accounts (Plan Comptable Général) system.

## Attributes

> **Note**: Complete attribute details are not fully documented in the public API reference. The following table represents the standard QuickBooks entity structure. For detailed field information, consult the official Intuit Developer documentation or use the API Explorer with a French company file.

| Name | Type | Required | Description | Notes |
|------|------|----------|-------------|-------|
| Id | String | Read-only | Unique identifier for the JournalCode | System-generated |
| SyncToken | String | Required for updates | Version control token | Increments with each update |
| MetaData | Object | Read-only | Metadata about entity creation/modification | Contains CreateTime and LastUpdatedTime |
| Name | String | Required | Name of the journal code | Must be unique |
| Active | Boolean | Optional | Whether the journal code is active | Defaults to true |
| Description | String | Optional | Description of the journal code | Additional details |

## Sample JSON Response

```json
{
  "JournalCode": {
    "Id": "1",
    "SyncToken": "0",
    "MetaData": {
      "CreateTime": "2024-01-15T10:30:00-08:00",
      "LastUpdatedTime": "2024-01-15T10:30:00-08:00"
    },
    "Name": "ACH",
    "Active": true,
    "Description": "Achats"
  }
}
```

## CRUD Operations

### Create JournalCode
- **Endpoint**: `POST /v3/company/{companyId}/journalcode`
- **Note**: Available only for FR locale companies

### Read JournalCode
- **Get by ID**: `GET /v3/company/{companyId}/journalcode/{journalcodeId}`
- **Query**: `GET /v3/company/{companyId}/query?query=select * from JournalCode`

### Update JournalCode
- **Endpoint**: `POST /v3/company/{companyId}/journalcode`
- **Note**: Include the Id and updated SyncToken in the request body

### Delete JournalCode
- **Endpoint**: `POST /v3/company/{companyId}/journalcode?operation=delete`
- **Note**: Include the Id and SyncToken in the request body

## Query Examples

### Find all JournalCodes
```sql
SELECT * FROM JournalCode
```

### Find active JournalCodes
```sql
SELECT * FROM JournalCode WHERE Active = true
```

### Find by name
```sql
SELECT * FROM JournalCode WHERE Name = 'ACH'
```

## Special Notes and Limitations

1. **Locale Restriction**: JournalCode is available **only for French (FR) locale** QuickBooks Online companies. Attempting to use this entity with companies in other locales will result in an error.

2. **French Accounting Compliance**: This entity is designed to support French accounting standards and the Plan Comptable Général (PCG) system.

3. **Name Uniqueness**: Journal code names must be unique within the company.

4. **Deletion Restrictions**: JournalCodes that are referenced by transactions cannot be deleted. They can be marked as inactive instead.

5. **API Access**: Requires appropriate OAuth 2.0 scopes for accounting data access.

## Integration Notes

When working with JournalCode entities:

- Ensure your application checks the company locale before attempting to use JournalCode endpoints
- Handle locale-specific errors appropriately
- Consider implementing fallback logic for non-FR locale companies
- Cache JournalCode lists as they typically don't change frequently

## Related Entities

- **JournalEntry**: Uses JournalCode for categorization in FR locale
- **Account**: May be associated with specific journal codes
- **Transaction**: Various transaction types may reference journal codes

## Additional Resources

- [QuickBooks Online API Documentation](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/journalcode)
- [French Accounting Standards](https://www.anc.gouv.fr/)
- [QuickBooks API Explorer](https://developer.intuit.com/app/developer/qbo/docs/develop/explore-the-quickbooks-online-api/api-explorer)

---

*Note: This documentation is based on available public information. For the most current and detailed information, please refer to the official Intuit Developer documentation and test with a French locale QuickBooks Online company.*