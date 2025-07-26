# TimeActivity

The TimeActivity entity represents time tracking entries for employees or vendors.

## Operations

### Create
Create a new time activity.

#### Request
```
POST /v3/company/{companyId}/timeactivity
```

#### Request Body
```json
{
  "TxnDate": "2025-01-15",
  "NameOf": "Employee",
  "EmployeeRef": {
    "value": "55",
    "name": "John Smith"
  },
  "CustomerRef": {
    "value": "1",
    "name": "Amy's Bird Sanctuary"
  },
  "ItemRef": {
    "value": "1",
    "name": "Services"
  },
  "BillableStatus": "Billable",
  "Taxable": false,
  "HourlyRate": 75.00,
  "Hours": 3,
  "Minutes": 30,
  "Description": "Landscape design consultation"
}
```

#### Response
```json
{
  "TimeActivity": {
    "TxnDate": "2025-01-15",
    "NameOf": "Employee",
    "EmployeeRef": {
      "value": "55",
      "name": "John Smith"
    },
    "CustomerRef": {
      "value": "1",
      "name": "Amy's Bird Sanctuary"
    },
    "ItemRef": {
      "value": "1",
      "name": "Services"
    },
    "BillableStatus": "Billable",
    "Taxable": false,
    "HourlyRate": 75.00,
    "Hours": 3,
    "Minutes": 30,
    "StartTime": "2025-01-15T09:00:00-08:00",
    "EndTime": "2025-01-15T12:30:00-08:00",
    "Description": "Landscape design consultation",
    "domain": "QBO",
    "sparse": false,
    "Id": "123",
    "SyncToken": "0",
    "MetaData": {
      "CreateTime": "2025-01-15T13:00:00-08:00",
      "LastUpdatedTime": "2025-01-15T13:00:00-08:00"
    }
  },
  "time": "2025-01-15T13:00:00.000-08:00"
}
```

### Read
Retrieve a time activity by ID.

#### Request
```
GET /v3/company/{companyId}/timeactivity/{timeActivityId}
```

### Update
Update an existing time activity.

#### Request
```
POST /v3/company/{companyId}/timeactivity
```

Include the full time activity object with `Id` and updated `SyncToken`.

### Delete
Delete a time activity.

#### Request
```
POST /v3/company/{companyId}/timeactivity?operation=delete
```

#### Request Body
```json
{
  "Id": "123",
  "SyncToken": "0"
}
```

### Query
Query time activities with filters.

#### Request
```
GET /v3/company/{companyId}/query?query=select * from TimeActivity where TxnDate >= '2025-01-01' and TxnDate <= '2025-01-31'
```

## Fields

- `TxnDate` (required) - Date of the time activity
- `NameOf` (required) - "Employee" or "Vendor"
- `EmployeeRef` - Reference to employee (if NameOf is "Employee")
- `VendorRef` - Reference to vendor (if NameOf is "Vendor")
- `CustomerRef` - Customer to bill time to
- `ItemRef` - Service item for billing
- `BillableStatus` - Billable, NotBillable, or HasBeenBilled
- `Taxable` - Whether time is taxable when billed
- `HourlyRate` - Hourly billing rate
- `Hours` - Number of hours
- `Minutes` - Number of minutes
- `StartTime` - Start time (ISO 8601 format)
- `EndTime` - End time (ISO 8601 format)
- `Description` - Description of work performed
- `ClassRef` - Class reference
- `DepartmentRef` - Department reference

## Time Entry Methods

### Duration Entry
Specify hours and minutes:
```json
{
  "Hours": 8,
  "Minutes": 30
}
```

### Start/End Time Entry
Specify exact times:
```json
{
  "StartTime": "2025-01-15T09:00:00-08:00",
  "EndTime": "2025-01-15T17:30:00-08:00"
}
```

## Billable Status

- `Billable` - Can be billed to customer
- `NotBillable` - Internal time, not billable
- `HasBeenBilled` - Already included on an invoice

## Employee Time Activity
```json
{
  "TxnDate": "2025-01-15",
  "NameOf": "Employee",
  "EmployeeRef": {
    "value": "55"
  },
  "CustomerRef": {
    "value": "1"
  },
  "ItemRef": {
    "value": "1"
  },
  "BillableStatus": "Billable",
  "HourlyRate": 75.00,
  "Hours": 8,
  "Minutes": 0,
  "Description": "Full day of consulting services"
}
```

## Vendor Time Activity
```json
{
  "TxnDate": "2025-01-15",
  "NameOf": "Vendor",
  "VendorRef": {
    "value": "41"
  },
  "CustomerRef": {
    "value": "1"
  },
  "ItemRef": {
    "value": "1"
  },
  "BillableStatus": "Billable",
  "HourlyRate": 100.00,
  "Hours": 5,
  "Minutes": 0,
  "Description": "Subcontractor work"
}
```

## Invoicing Time Activities

To bill time activities on an invoice:
```json
{
  "Line": [
    {
      "DetailType": "SalesItemLineDetail",
      "Amount": 262.50,
      "SalesItemLineDetail": {
        "ItemRef": {
          "value": "1"
        }
      },
      "LinkedTxn": [
        {
          "TxnId": "123",
          "TxnType": "TimeActivity"
        }
      ]
    }
  ]
}
```

## Time Reports

Query billable time:
```
GET /v3/company/{companyId}/query?query=select * from TimeActivity where BillableStatus = 'Billable'
```

Query by employee:
```
GET /v3/company/{companyId}/query?query=select * from TimeActivity where EmployeeRef = '55'
```

## Notes
- Used for tracking billable and non-billable time
- Can be linked to invoices for billing
- Supports both employee and vendor time
- Hourly rate can override default rates
- Status automatically updates when billed
- Essential for service-based businesses