# Employee Entity - QuickBooks Online API

## Description
The Employee entity represents an employee in QuickBooks Online. This entity contains information about individuals who work for the company, including their personal details, contact information, and employment-related data.

## Attributes

| Name | Type | Required | Description | Notes |
|------|------|----------|-------------|-------|
| Id | String | Read-only | Unique identifier for the employee | System generated |
| SyncToken | String | Read-only | Version number of the entity | Required for updates |
| MetaData | MetaData | Read-only | Metadata about entity creation/modification | System generated |
| DisplayName | String | Yes | The name of the employee as displayed | Used in UI displays |
| GivenName | String | No | First name of the employee | |
| MiddleName | String | No | Middle name of the employee | |
| FamilyName | String | No | Last name of the employee | |
| Suffix | String | No | Suffix of the employee's name (e.g., Jr., Sr.) | |
| Title | String | No | Title or position of the employee | |
| PrintOnCheckName | String | No | Name as printed on checks | |
| Active | Boolean | No | Whether the employee is active | Default: true |
| PrimaryPhone | TelephoneNumber | No | Primary phone number | Uses FreeFormNumber object |
| Mobile | TelephoneNumber | No | Mobile phone number | Uses FreeFormNumber object |
| PrimaryEmailAddr | EmailAddress | No | Primary email address | |
| SSN | String | No | Social Security Number | Write-only field for security |
| EmployeeNumber | String | No | Employee number or ID | |
| BirthDate | Date | No | Date of birth | Format: YYYY-MM-DD |
| Gender | String | No | Gender of the employee | Values: Male, Female |
| HiredDate | Date | No | Date employee was hired | Format: YYYY-MM-DD |
| ReleasedDate | Date | No | Date employee was released/terminated | Format: YYYY-MM-DD |
| PrimaryAddr | PhysicalAddress | No | Primary address | Address object |
| BillableTime | Boolean | No | Whether employee time is billable | Default: false |
| BillRate | Decimal | No | Billing rate for the employee | |
| V4IDPseudonym | String | No | Pseudonym for V4 ID | System use |

## Sample JSON Response

```json
{
  "Employee": {
    "Id": "55",
    "SyncToken": "1",
    "MetaData": {
      "CreateTime": "2024-01-15T09:30:00-08:00",
      "LastUpdatedTime": "2024-01-15T09:30:00-08:00"
    },
    "DisplayName": "John Smith",
    "GivenName": "John",
    "MiddleName": "A",
    "FamilyName": "Smith",
    "PrintOnCheckName": "John A. Smith",
    "Active": true,
    "PrimaryPhone": {
      "FreeFormNumber": "(555) 555-1234"
    },
    "Mobile": {
      "FreeFormNumber": "(555) 555-5678"
    },
    "PrimaryEmailAddr": {
      "Address": "john.smith@example.com"
    },
    "EmployeeNumber": "EMP-001",
    "BirthDate": "1980-05-15",
    "Gender": "Male",
    "HiredDate": "2020-01-01",
    "PrimaryAddr": {
      "Line1": "123 Main Street",
      "City": "San Francisco",
      "CountrySubDivisionCode": "CA",
      "PostalCode": "94105",
      "Country": "USA"
    },
    "BillableTime": true,
    "BillRate": 75.00
  },
  "time": "2024-01-15T09:30:00-08:00"
}
```

## CRUD Operations

### Create Employee
**Endpoint:** `POST /v3/company/{companyID}/employee`

**Request Body:**
```json
{
  "DisplayName": "Jane Doe",
  "GivenName": "Jane",
  "FamilyName": "Doe",
  "SSN": "123-45-6789",
  "PrimaryPhone": {
    "FreeFormNumber": "(555) 555-9999"
  },
  "PrimaryEmailAddr": {
    "Address": "jane.doe@example.com"
  },
  "HiredDate": "2024-01-15"
}
```

### Read Employee

#### Get Single Employee
**Endpoint:** `GET /v3/company/{companyID}/employee/{employeeId}`

#### Query Employees
**Endpoint:** `GET /v3/company/{companyID}/query?query=select * from Employee`

**Query Examples:**
- All employees: `select * from Employee`
- Active employees: `select * from Employee where Active = true`
- By name: `select * from Employee where DisplayName = 'John Smith'`
- With pagination: `select * from Employee startposition 1 maxresults 20`

### Update Employee
**Endpoint:** `POST /v3/company/{companyID}/employee`

**Request Body:**
```json
{
  "Id": "55",
  "SyncToken": "1",
  "DisplayName": "John A. Smith",
  "GivenName": "John",
  "MiddleName": "Andrew",
  "FamilyName": "Smith",
  "PrimaryPhone": {
    "FreeFormNumber": "(555) 555-1234"
  },
  "BillRate": 85.00
}
```

**Note:** Must include current SyncToken value to prevent update conflicts.

### Delete Employee
QuickBooks Online API does not support hard deletion of employees. To deactivate an employee, update the entity with `"Active": false`.

## Special Notes and Limitations

1. **SSN Security**: The SSN field is write-only. It will never be returned in read operations for security purposes.

2. **Sparse Updates**: The API supports sparse updates, meaning you only need to send the fields you want to update (along with Id and SyncToken).

3. **Active Status**: Employees cannot be permanently deleted. Set `Active` to `false` to deactivate.

4. **Phone Number Format**: Phone numbers use the `FreeFormNumber` field within the TelephoneNumber object structure.

5. **Required Fields**: Only `DisplayName` is required when creating an employee.

6. **Query Limitations**: 
   - Maximum of 1000 results per query
   - Use pagination for large result sets
   - Filtering is case-sensitive

7. **Rate Limits**: Subject to QuickBooks Online API rate limits (500 requests per minute for most endpoints).

8. **Permissions**: Requires appropriate OAuth 2.0 scopes:
   - `com.intuit.quickbooks.accounting` for read/write access
   - `com.intuit.quickbooks.payroll` may be required for payroll-related fields

9. **Payroll Integration**: Some fields may only be available or editable if QuickBooks Payroll is enabled.

10. **Audit Trail**: All changes to employee records are tracked in the QuickBooks audit log.