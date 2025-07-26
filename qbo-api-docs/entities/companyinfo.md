# CompanyInfo

The CompanyInfo resource contains basic company information including company name, addresses, and other legal information.

## The companyinfo object

### Attributes

| Attribute | Type | Description |
|-----------|------|-------------|
| **Id** | String | Read only, system defined. Unique identifier for this object. Always "1" for CompanyInfo. |
| **CompanyName** | String | **Required**. The name of the company as displayed to users. |
| **LegalName** | String | Optional. Legal name of the company for official documents and filings. |
| **CompanyAddr** | PhysicalAddress | Optional. Primary company address. |
| **CustomerCommunicationAddr** | PhysicalAddress | Optional. Address used for customer communication and on sales forms. |
| **LegalAddr** | PhysicalAddress | Optional. Legal address of the company for official documents. |
| **PrimaryPhone** | TelephoneNumber | Optional. Primary phone number for the company. |
| **CompanyStartDate** | Date | Optional. Date the company was started/established. |
| **FiscalYearStartMonth** | String | Optional. The month in which the fiscal year starts (e.g., "January"). |
| **Country** | String | Optional. Country name where the company is located. |
| **Email** | EmailAddress | Optional. Primary company email address. |
| **WebAddr** | WebSiteAddress | Optional. Company website URL. |
| **SupportedLanguages** | String | Optional. Comma separated list of languages supported by the company. |
| **NameValue** | NameValue[] | Optional. Array of name/value pairs for additional company information. |
| **SyncToken** | String | **Required for update**. Version number of the object. |
| **MetaData** | ModificationMetaData | Optional. Descriptive information about the object including create and last updated time. |

## Operations

### Query companyinfo

Returns the company information. Since there is only one CompanyInfo object per company, the query will always return a single record.

**Example query:**
```
SELECT * FROM CompanyInfo
```

### Read a companyinfo

Retrieves the company information details.

**Endpoint:** `GET /v3/company/{companyId}/companyinfo/1`

**Note:** The Id is always "1" for CompanyInfo.

### Update a companyinfo

Updates the company information. Not all fields can be updated - some are set during company creation and are read-only.

**Updatable fields:**
- CompanyName
- CompanyAddr
- CustomerCommunicationAddr
- LegalAddr
- PrimaryPhone
- Email
- WebAddr

**Read-only fields:**
- Id
- Country
- FiscalYearStartMonth
- CompanyStartDate
- MetaData

## Address Objects

The address fields use the PhysicalAddress type with the following structure:
- Line1 - Street address line 1
- Line2 - Street address line 2
- Line3 - Street address line 3
- Line4 - Street address line 4
- Line5 - Street address line 5
- City - City name
- Country - Country name
- CountrySubDivisionCode - State/Province code
- PostalCode - ZIP or postal code

## Special Considerations

1. **Single Object**: There is only one CompanyInfo object per company, always with Id = "1"
2. **Company Setup**: Many fields are set during initial company setup and cannot be changed via API
3. **Fiscal Year**: The fiscal year start month affects reporting and cannot be changed after company creation
4. **Multi-currency**: The base currency is determined by the Country field and cannot be changed