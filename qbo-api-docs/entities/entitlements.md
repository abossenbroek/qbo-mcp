# Entitlements

## Attributes

### PlanName
- **Type**: String
- **Description**: Billing plan associated with this company.

### Entitlement [0..n]
- **Entitlement.id**: Integer. Name of the entitlement.
- **Entitlement.name**: String. Name of the entitlement.
- **Entitlement.Term**: Boolean. Availability of entitlement: On or Off.

### SupportedLanguages
- **Type**: String
- **Description**: Comma separated list of languages.

### Entitlement
- **Max character**: maximum of 20 chars

### TelephoneNumber
- **Description**: Primary phone number.
- Show child attributes

### CompanyStartDate
- **Type**: DateTime
- **Description**: DateTime when company file was created. This field and Metadata.CreateTime contain the same value.
- Show child attributes

### EmployerId
- **Type**: String
- **Description**: Employer identifier (EIN).

### QboCompany
- **Type**: Boolean
- **Description**: Check if the company is a QuickBooks Online company. false is returned if not a QuickBooks Online company, the company exists in the Intuit ecosystem, but is not a QuickBooks Online company, or the company is a QuickBooks Online company, but the current user does not belong to the company.

### Email
- **Max character**: max 100 chars

### EmailAddress
- **Description**: Default email address.
- Show child attributes

### WebAddr
- **Description**: WebSiteAddress
- Website address.
- Show child attributes

### FiscalYearStartMonth
- **Type**: MonthEnum
- **Description**: The start month of fiscal year.

### Thresholds [0..n]
- **minorVersion**: 43
- **Threshold**: The threshold for this company.
- Show child attributes

### DaysRemainingTrial
- **Type**: Integer
- **Description**: Remaining trial period days.

### MaxUsers
- **Type**: Integer
- **Description**: Maximum billable users allowed in the company.

### CurrentUsers
- **Type**: Integer
- **Description**: Billable users currently in the company.

---
*Source: https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/entitlements*