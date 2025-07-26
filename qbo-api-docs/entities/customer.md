# Customer

A customer is a consumer of the service or product that your business offers. An individual customer can have an underlying nested structure, with a parent customer (the top-level object) having zero or more sub-customers and jobs associated with it.

Sub-customer examples:
- Members of a team or league: the team itself is the parent customer and the members are sub-customers.
- Properties managed by a property management company: the management company is the parent customer and the properties are the sub-customers.

Job examples:
- Tracking a kitchen remodel: the home owner is the parent customer and individual kitchen remodel tasks are jobs.
- Tracking car repairs: the car owner is the parent customer and individual car repairs are jobs.

Use the Customer resource to create parent customer objects, sub-customer objects, and job objects according to your business requirements. Use the ParentRef and Job attributes in the customer object to designate whether the object is a parent, nested job or nested sub-customer.

First, create parent customer objects: Set Job to false (default) and do not define ParentRef.
Then, create sub-customer and job objects: Set Job to true and set ParentRef to reference parent customer object.

Going forward, specify an individual parent customer object, sub-customer object, or job object in sales transactions via the transaction's CustomerRef attribute, based on your business requirements. See QuickBooks product documentation for more about sub-customers and jobs.

## Business Rules

- The DisplayName, Title, GivenName, MiddleName, FamilyName, Suffix, and PrintOnCheckName attributes must not contain colon (:), tab (\t), or newline (\n) characters.
- The DisplayName attribute must be unique across all other customer, employee, and vendor objects.
- The PrimaryEmailAddress attribute must contain an at sign (@) and dot (.).
- Nested Customer objects can be used to define sub-customers, jobs, or a combination of both, under a parent.
- Up to four levels of nesting can be defined under a top-level parent Customer object.
- The Job attribute defines whether the object is a parent customer or nested sub-customer/job.
- The DisplayName attribute or at least one of Title, GivenName, MiddleName, FamilyName, or Suffix attributes is required during object create.

## The Customer object

### ATTRIBUTES

**Id**
* Required for update
read only
system defined
String , filterable , sortable
Unique identifier for this object. Sort order is ASC by default.

**SyncToken**
* Required for update
read only
system defined
String
Version number of the object. It is used to lock an object for use by one app at a time. As soon as an application modifies an object, its SyncToken is incremented. Attempts to modify an object specifying an older SyncToken fails. Only the latest version of the object is maintained by QuickBooks Online.

**DisplayName**
* Conditionally required
max character: maximum of 500 chars
String , filterable , sortable
The name of the person or organization as displayed. Must be unique across all Customer, Vendor, and Employee objects. Cannot be removed with sparse update. If not supplied, the system generates DisplayName by concatenating customer name components supplied in the request from the following list: Title, GivenName, MiddleName, FamilyName, and Suffix.

**Title**
* Conditionally required
max character: maximum of 16 chars
String
Title of the person. This tag supports i18n, all locales. The DisplayName attribute or at least one of Title, GivenName, MiddleName, FamilyName, or Suffix attributes is required.

**GivenName**
* Conditionally required
max character: maximum of 100 chars
String , filterable , sortable
Given name or first name of a person. The DisplayName attribute or at least one of Title, GivenName, MiddleName, FamilyName, or Suffix attributes is required.

**MiddleName**
* Conditionally required
max character: maximum of 100 chars
String , filterable , sortable
Middle name of the person. The person can have zero or more middle names. The DisplayName attribute or at least one of Title, GivenName, MiddleName, FamilyName, or Suffix attributes is required.

**Suffix**
* Conditionally required
max character: maximum of 16 chars
String
Suffix of the name. For example, Jr. The DisplayName attribute or at least one of Title, GivenName, MiddleName, FamilyName, or Suffix attributes is required.

**FamilyName**
* Conditionally required
max character: maximum of 100 chars
String , filterable , sortable
Family name or the last name of the person. The DisplayName attribute or at least one of Title, GivenName, MiddleName, FamilyName, or Suffix attributes is required.

**PrimaryEmailAddr**
Optional
EmailAddress , filterable
Primary email address.
Show child attributes 

**ResaleNum**
Optional
max character: 16 chars
String
Resale number or some additional info about the customer.

**SecondaryTaxIdentifier**
Optional
minorVersion: 3
String
Also called UTR No. in ( UK ) , CST Reg No. ( IN ) also represents the tax registration number of the Person or Organization. This value is masked in responses, exposing only last five characters. For example, the ID of 123-45-6789 is returned as XXXXXX56789.

**ARAccountRef**
Optional
minorVersion: 3
ReferenceType
Identifies the accounts receivable account to be used for this customer. Each customer must have his own AR account. Applicable for France companies, only. Available when endpoint is evoked with the minorversion=3 query parameter. Query the Account name list resource to determine the appropriate Account object for this reference, where Account.AccountType=Accounts Receivable. Use Account.Id and Account.Name from that object for ARAccountRef.value and ARAccountRef.name, respectively.
Show child attributes 

**DefaultTaxCodeRef**
Optional
ReferenceType
Reference to a default tax code associated with this Customer object. Reference is valid if Customer.Taxable is set to true; otherwise, it is ignored. If automated sales tax is enabled (Preferences.TaxPrefs.PartnerTaxEnabled is set to true) the default tax code is set by the system and can not be overridden. Query the TaxCode name list resource to determine the appropriate TaxCode object for this reference. Use TaxCode.Id and TaxCode.Name from that object for DefaultTaxCodeRef.value and DefaultTaxCodeRef.name, respectively.
Show child attributes 

**PreferredDeliveryMethod**
Optional
String
Preferred delivery method. Values are Print, Email, or None.

**GSTIN**
Optional
max character: maximum of 15 chars
minorVersion: 33
String
GSTIN is an identification number assigned to every GST registered business.

**SalesTermRef**
Optional
ReferenceType
Reference to a SalesTerm associated with this Customer object. Query the Term name list resource to determine the appropriate Term object for this reference. Use Term.Id and Term.Name from that object for SalesTermRef.value and SalesTermRef.name, respectively.
Show child attributes 

**CustomerTypeRef**
Optional
String
Reference to the customer type assigned to a customer. This field is only returned if the customer is assigned a customer type.
Show child attributes 

**Fax**
Optional
max character: maximum of 30 chars
TelephoneNumber
Fax number.
Show child attributes 

**BusinessNumber**
Optional
max character: maximum of 10 chars
minorVersion: 33
String
Also called, PAN (in India) is a code that acts as an identification for individuals, families and corporates, especially for those who pay taxes on their income.

**BillWithParent**
Optional
Boolean
If true, this Customer object is billed with its parent. If false, or null the customer is not to be billed with its parent. This attribute is valid only if this entity is a Job or sub Customer.

**CurrencyRef**
Optional
max character: 16 chars
read only
CurrencyRef
Reference to the currency in which all amounts associated with this customer are expressed. Once set, it cannot be changed. If specified currency is not currently in the company's currency list, it is added. If not specified, currency for this customer is the home currency of the company, as defined by Preferences.CurrencyPrefs.HomeCurrency.
Show child attributes 

**Mobile**
Optional
max character: maximum of 30 chars
TelephoneNumber
Mobile phone number.
Show child attributes 

**Job**
Optional
Boolean
If true, this is a Job or sub-customer. If false or null, this is a top level customer, not a Job or sub-customer.

**BalanceWithJobs**
Optional
Decimal , sortable
Cumulative open balance amount for the Customer (or Job) and all its sub-jobs. Cannot be written to QuickBooks.

**PrimaryPhone**
Optional
max character: maximum of 30 chars
TelephoneNumber
Primary phone number.
Show child attributes 

**OpenBalanceDate**
Optional
Date
Date of the Open Balance for the create operation. Write-on-create.
Show child attributes 

**Taxable**
Optional
Boolean
If true, transactions for this customer are taxable. Default behavior with minor version 10 and above: true, if DefaultTaxCodeRef is defined or false if TaxExemptionReasonId is set.

**AlternatePhone**
Optional
max character: maximum of 30 chars
TelephoneNumber
Alternate phone number.
Show child attributes 

**MetaData**
Optional
ModificationMetaData
Descriptive information about the entity. The MetaData values are set by Data Services and are read only for all applications.
Show child attributes 

**ParentRef**
Optional
ReferenceType
A reference to a Customer object that is the immediate parent of the Sub-Customer/Job in the hierarchical Customer:Job list. Required for the create operation if this object is a sub-customer or Job. Query the Customer name list resource to determine the appropriate Customer object for this reference. Use Customer.Id and Customer.DisplayName from that object for ParentRef.value and ParentRef.name, respectively.
Show child attributes 

**Notes**
Optional
max character: maximum of 2000 chars
String
Free form text describing the Customer.

**WebAddr**
Optional
max character: maximum of 1000 chars
WebSiteAddress
Website address.
Show child attributes 

**Active**
Optional
Boolean , filterable , sortable
If true, this entity is currently enabled for use by QuickBooks. If there is an amount in Customer.Balance when setting this Customer object to inactive through the QuickBooks UI, a CreditMemo balancing transaction is created for the amount.

**CompanyName**
Optional
max character: maximum of 100 chars
String , filterable , sortable
The name of the company associated with the person or organization.

**Balance**
Optional
Decimal , filterable , sortable
Specifies the open balance amount or the amount unpaid by the customer. For the create operation, this represents the opening balance for the customer. When returned in response to the query request it represents the current open balance (unpaid amount) for that customer. Write-on-create.

**ShipAddr**
Optional
PhysicalAddress
Default shipping address. If a physical address is updated from within the transaction object, the QuickBooks Online API flows individual address components differently into the Line elements of the transaction response then when the transaction was first created:

Line1 and Line2 elements are populated with the customer name and company name.
Original Line1 through Line 5 contents, City, SubDivisionCode, and PostalCode flow into Line3 through Line5as a free format strings.
Show more details
Show child attributes 

**PaymentMethodRef**
Optional
ReferenceType
Reference to a PaymentMethod associated with this Customer object. Query the PaymentMethod name list resource to determine the appropriate PaymentMethod object for this reference. Use PaymentMethod.Id and PaymentMethod.Name from that object for PaymentMethodRef.value and PaymentMethodRef.name, respectively.
Show child attributes 

**IsProject**
Optional
read only
minorVersion: 25
Boolean
If true, indicates this is a Project.

**Source**
Optional
minorVersion: 59
String
The Source type of the transactions created by QuickBooks Commerce. Valid values include: QBCommerce

**PrimaryTaxIdentifier**
Optional
minorVersion: 4
String
Also called Tax Reg. No in ( UK ) , ( CA ) , ( IN ) , ( AU ) represents the tax ID of the Person or Organization. This value is masked in responses, exposing only last five characters. For example, the ID of 123-45-6789 is returned as XXXXXX56789.

**GSTRegistrationType**
Optional
max character: maximum of 15 chars
minorVersion: 33
String
For the filing of GSTR, transactions need to be classified depending on the type of customer to whom the sale is done. To facilitate this, we have introduced a new field as 'GST registration type'. Possible values are listed below:
- GST_REG_REG GST registered- Regular. Customer who has a business which is registered under GST and has a GSTIN (doesn't include customers registered under composition scheme, as an SEZ or as EOU's, STP's EHTP's etc.).
- GST_REG_COMP GST registered-Composition. Customer who has a business which is registered under the composition scheme of GST and has a GSTIN.
- GST_UNREG GST unregistered. Customer who has a business which is not registered under GST and does not have a GSTIN.
- CONSUMER Consumer. Customer who is not registered under GST and is the final consumer of the service or product sold.
- OVERSEAS Overseas. Customer who has a business which is located out of India.
- SEZ SEZ. Customer who has a business which is registered under GST, has a GSTIN and is located in a SEZ or is a SEZ Developer.
- DEEMED Deemed exports- EOU's, STP's EHTP's etc. Customer who has a business which is registered under GST and falls in the category of companies (EOU's, STP's EHTP's etc.), to which supplies are made they are termed as deemed exports.

**PrintOnCheckName**
Optional
max character: maximum of 110 chars
String , filterable , sortable
Name of the person or organization as printed on a check. If not provided, this is populated from DisplayName. Constraints: Cannot be removed with sparse update.

**BillAddr**
Optional
PhysicalAddress
Default billing address. If a physical address is updated from within the transaction object, the QuickBooks Online API flows individual address components differently into the Line elements of the transaction response then when the transaction was first created:

Line1 and Line2 elements are populated with the customer name and company name.
Original Line1 through Line 5 contents, City, SubDivisionCode, and PostalCode flow into Line3 through Line5as a free format strings.
Show more details
Show child attributes 

**FullyQualifiedName**
read only
system defined
String , filterable , sortable
Fully qualified name of the object. The fully qualified name prepends the topmost parent, followed by each sub element separated by colons. Takes the form of Customer:Job:Sub-job. System generated. Limited to 5 levels.

**Level**
read only
system defined
Integer
Specifies the level of the hierarchy in which the entity is located. Zero specifies the top level of the hierarchy; anything above will be level with respect to the parent. Constraints:up to 5 levels

**TaxExemptionReasonId**
minorVersion: 10
Numeric Id
The tax exemption reason associated with this customer object. Applicable if automated sales tax is enabled (Preferences.TaxPrefs.PartnerTaxEnabled is set to true) for the company. Set TaxExemptionReasonId: to one of the following:

| Id | Reason |
|----|--------|
| 1 | Federal government |
| 2 | State government |
| 3 | Local government |
| 4 | Tribal government |
| 5 | Charitable organization |
| 6 | Religious organization |
| 7 | Educational organization |
| 8 | Hospital |
| 9 | Resale |
| 10 | Direct pay permit |
| 11 | Multiple points of use |
| 12 | Direct mail |
| 13 | Agricultural production |
| 14 | Industrial production / manufacturing |
| 15 | Foreign diplomat |

### SAMPLE OBJECT

```json
{
  "Customer": {
    "PrimaryEmailAddr": {
      "Address": "Surf@Intuit.com"
    }, 
    "SyncToken": "0", 
    "domain": "QBO", 
    "GivenName": "Bill", 
    "DisplayName": "Bill's Windsurf Shop", 
    "BillWithParent": false, 
    "FullyQualifiedName": "Bill's Windsurf Shop", 
    "CompanyName": "Bill's Windsurf Shop", 
    "FamilyName": "Lucchini", 
    "sparse": false, 
    "PrimaryPhone": {
      "FreeFormNumber": "(415) 444-6538"
    }, 
    "Active": true, 
    "Job": false, 
    "BalanceWithJobs": 85.0, 
    "BillAddr": {
      "City": "Half Moon Bay", 
      "Line1": "12 Ocean Dr.", 
      "PostalCode": "94213", 
      "Lat": "37.4307072", 
      "Long": "-122.4295234", 
      "CountrySubDivisionCode": "CA", 
      "Id": "3"
    }, 
    "PreferredDeliveryMethod": "Print", 
    "Taxable": false, 
    "PrintOnCheckName": "Bill's Windsurf Shop", 
    "Balance": 85.0, 
    "Id": "2", 
    "MetaData": {
      "CreateTime": "2014-09-11T16:49:28-07:00", 
      "LastUpdatedTime": "2014-09-18T12:56:01-07:00"
    }
  }, 
  "time": "2015-07-23T11:04:15.496-07:00"
}
```

## Create a customer

The DisplayName attribute or at least one of Title, GivenName, MiddleName, FamilyName, or Suffix attributes is required during object create.

### Request Body

The minimum elements to create a Customer are listed here.

### Returns

Returns the newly created Customer object.

### Request URL

```
POST /v3/company/<realmID>/customer
Content type:application/json
Production Base URL:https://quickbooks.api.intuit.com
Sandbox Base URL:https://sandbox-quickbooks.api.intuit.com
```

### Request Body

```json
{
  "FullyQualifiedName": "King Groceries", 
  "PrimaryEmailAddr": {
    "Address": "jdrew@myemail.com"
  }, 
  "DisplayName": "King's Groceries", 
  "Suffix": "Jr", 
  "Title": "Mr", 
  "MiddleName": "B", 
  "Notes": "Here are other details.", 
  "FamilyName": "King", 
  "PrimaryPhone": {
    "FreeFormNumber": "(555) 555-5555"
  }, 
  "CompanyName": "King Groceries", 
  "BillAddr": {
    "CountrySubDivisionCode": "CA", 
    "City": "Mountain View", 
    "PostalCode": "94042", 
    "Line1": "123 Main Street", 
    "Country": "USA"
  }, 
  "GivenName": "James"
}
```

### Returns

```json
{
  "Customer": {
    "domain": "QBO", 
    "PrimaryEmailAddr": {
      "Address": "jdrew@myemail.com"
    }, 
    "DisplayName": "King's Groceries", 
    "CurrencyRef": {
      "name": "United States Dollar", 
      "value": "USD"
    }, 
    "DefaultTaxCodeRef": {
      "value": "2"
    }, 
    "PreferredDeliveryMethod": "Print", 
    "GivenName": "James", 
    "FullyQualifiedName": "King's Groceries", 
    "BillWithParent": false, 
    "Title": "Mr", 
    "Job": false, 
    "BalanceWithJobs": 0, 
    "PrimaryPhone": {
      "FreeFormNumber": "(555) 555-5555"
    }, 
    "Taxable": true, 
    "MetaData": {
      "CreateTime": "2015-07-23T10:58:12-07:00", 
      "LastUpdatedTime": "2015-07-23T10:58:12-07:00"
    }, 
    "BillAddr": {
      "City": "Mountain View", 
      "Country": "USA", 
      "Line1": "123 Main Street", 
      "PostalCode": "94042", 
      "CountrySubDivisionCode": "CA", 
      "Id": "112"
    }, 
    "MiddleName": "B", 
    "Notes": "Here are other details.", 
    "Active": true, 
    "Balance": 0, 
    "SyncToken": "0", 
    "Suffix": "Jr", 
    "CompanyName": "King Groceries", 
    "FamilyName": "King", 
    "PrintOnCheckName": "King Groceries", 
    "sparse": false, 
    "Id": "67"
  }, 
  "time": "2015-07-23T10:58:12.099-07:00"
}
```

## Query a customer

### Returns

Returns the results of the query.

### Request URL

```
GET /v3/company/<realmID>/query?query=<selectStatement>
Content type:text/plain
Production Base URL:https://quickbooks.api.intuit.com
Sandbox Base URL:https://sandbox-quickbooks.api.intuit.com
```

### Sample Query

```
select * from Customer Where Metadata.LastUpdatedTime > '2015-03-01'
```

### Returns

```json
{
  "QueryResponse": {
    "Customer": [
      {
        "domain": "QBO", 
        "FamilyName": "Lauterbach", 
        "DisplayName": "Amy's Bird Sanctuary", 
        "DefaultTaxCodeRef": {
          "value": "2"
        }, 
        "PrimaryEmailAddr": {
          "Address": "Birds@Intuit.com"
        }, 
        "PreferredDeliveryMethod": "Print", 
        "GivenName": "Amy", 
        "FullyQualifiedName": "Amy's Bird Sanctuary", 
        "BillWithParent": false, 
        "Job": false, 
        "BalanceWithJobs": 274.0, 
        "PrimaryPhone": {
          "FreeFormNumber": "(650) 555-3311"
        }, 
        "Active": true, 
        "MetaData": {
          "CreateTime": "2014-09-11T16:48:43-07:00", 
          "LastUpdatedTime": "2015-07-01T10:14:15-07:00"
        }, 
        "BillAddr": {
          "City": "Bayshore", 
          "Line1": "4581 Finch St.", 
          "PostalCode": "94326", 
          "Lat": "INVALID", 
          "Long": "INVALID", 
          "CountrySubDivisionCode": "CA", 
          "Id": "2"
        }, 
        "MiddleName": "Michelle", 
        "Notes": "Note added via Update operation.", 
        "Taxable": true, 
        "Balance": 274.0, 
        "SyncToken": "5", 
        "CompanyName": "Amy's Bird Sanctuary", 
        "ShipAddr": {
          "City": "Bayshore", 
          "Line1": "4581 Finch St.", 
          "PostalCode": "94326", 
          "Lat": "INVALID", 
          "Long": "INVALID", 
          "CountrySubDivisionCode": "CA", 
          "Id": "109"
        }, 
        "PrintOnCheckName": "Amy's Bird Sanctuary", 
        "sparse": false, 
        "Id": "1"
      }, 
      {
        "domain": "QBO", 
        "PrimaryEmailAddr": {
          "Address": "Consulting@intuit.com"
        }, 
        "DisplayName": "Weiskopf Consulting", 
        "FamilyName": "Weiskopf", 
        "PreferredDeliveryMethod": "Print", 
        "GivenName": "Nicola", 
        "FullyQualifiedName": "Weiskopf Consulting", 
        "BillWithParent": false, 
        "Job": false, 
        "BalanceWithJobs": 390.0, 
        "PrimaryPhone": {
          "FreeFormNumber": "(650) 555-1423"
        }, 
        "Active": true, 
        "MetaData": {
          "CreateTime": "2014-09-11T17:29:04-07:00", 
          "LastUpdatedTime": "2015-06-24T15:54:02-07:00"
        }, 
        "BillAddr": {
          "City": "Bayshore", 
          "Line1": "45612 Main St.", 
          "PostalCode": "94326", 
          "Lat": "45.256574", 
          "Long": "-66.0943698", 
          "CountrySubDivisionCode": "CA", 
          "Id": "30"
        }, 
        "Taxable": false, 
        "Balance": 390.0, 
        "SyncToken": "0", 
        "CompanyName": "Weiskopf Consulting", 
        "ShipAddr": {
          "City": "Bayshore", 
          "Line1": "45612 Main St.", 
          "PostalCode": "94326", 
          "Lat": "45.256574", 
          "Long": "-66.0943698", 
          "CountrySubDivisionCode": "CA", 
          "Id": "30"
        }, 
        "PrintOnCheckName": "Weiskopf Consulting", 
        "sparse": false, 
        "Id": "29"
      }
    ], 
    "startPosition": 1, 
    "maxResults": 6
  }, 
  "time": "2015-07-23T11:02:25.149-07:00"
}
```

## Read a customer

Retrieves the details of a Customer object that has been previously created.

### Returns

Returns the Customer object.

### Request URL

```
GET /v3/company/<realmID>/customer/<customerId>
Production Base URL:https://quickbooks.api.intuit.com
Sandbox Base URL:https://sandbox-quickbooks.api.intuit.com
```

### Returns

```json
{
  "Customer": {
    "PrimaryEmailAddr": {
      "Address": "Surf@Intuit.com"
    }, 
    "SyncToken": "0", 
    "domain": "QBO", 
    "GivenName": "Bill", 
    "DisplayName": "Bill's Windsurf Shop", 
    "BillWithParent": false, 
    "FullyQualifiedName": "Bill's Windsurf Shop", 
    "CompanyName": "Bill's Windsurf Shop", 
    "FamilyName": "Lucchini", 
    "sparse": false, 
    "PrimaryPhone": {
      "FreeFormNumber": "(415) 444-6538"
    }, 
    "Active": true, 
    "Job": false, 
    "BalanceWithJobs": 85.0, 
    "BillAddr": {
      "City": "Half Moon Bay", 
      "Line1": "12 Ocean Dr.", 
      "PostalCode": "94213", 
      "Lat": "37.4307072", 
      "Long": "-122.4295234", 
      "CountrySubDivisionCode": "CA", 
      "Id": "3"
    }, 
    "PreferredDeliveryMethod": "Print", 
    "Taxable": false, 
    "PrintOnCheckName": "Bill's Windsurf Shop", 
    "Balance": 85.0, 
    "Id": "2", 
    "MetaData": {
      "CreateTime": "2014-09-11T16:49:28-07:00", 
      "LastUpdatedTime": "2014-09-18T12:56:01-07:00"
    }
  }, 
  "time": "2015-07-23T11:04:15.496-07:00"
}
```

## Full update a customer

Use this operation to update any of the writable fields of an existing Customer object. The request body must include all writable fields of the existing object as returned in a read response. Writable fields omitted from the request body are set to NULL. The ID of the object to update is specified in the request body.Add the query parameter, include=updateaccountontxns&minorversion=5, to the endpoint to automatically update the AR account on historical transactions (from soft close date forward) for this customer with that defined by the ARAccountRef attribute in the Customer object. Updates on soft closed transacitons will fail.

### Request Body

(Contains same attributes as create operation with Id and SyncToken required for update)

### Returns

The customer response body.

### Request URL

```
POST /v3/company/<realmID>/customer
Content type:application/json
Production Base URL:https://quickbooks.api.intuit.com
Sandbox Base URL:https://sandbox-quickbooks.api.intuit.com
```

## Sparse update a customer

Sparse updating provides the ability to update a subset of properties for a given object; only elements specified in the request are updated. Missing elements are left untouched. The ID of the object to update is specified in the request body.​

### Request Body

(Contains same attributes as create operation with Id and SyncToken required for update)

### Returns

The customer response body.

### Request URL

```
POST /v3/company/<realmID>/customer
Content type:application/json
Production Base URL:https://quickbooks.api.intuit.com
Sandbox Base URL:https://sandbox-quickbooks.api.intuit.com
```

### Request Body

```json
{
  "MiddleName": "Mark", 
  "SyncToken": "0", 
  "Id": "2", 
  "sparse": true
}
```

### Returns

```json
{
  "Customer": {
    "domain": "QBO", 
    "PrimaryEmailAddr": {
      "Address": "Surf@Intuit.com"
    }, 
    "DisplayName": "Bill's Windsurf Shop", 
    "PreferredDeliveryMethod": "Print", 
    "GivenName": "Bill", 
    "FullyQualifiedName": "Bill's Windsurf Shop", 
    "BillWithParent": false, 
    "Job": false, 
    "BalanceWithJobs": 85.0, 
    "PrimaryPhone": {
      "FreeFormNumber": "(415) 444-6538"
    }, 
    "Active": true, 
    "MetaData": {
      "CreateTime": "2014-09-11T16:49:28-07:00", 
      "LastUpdatedTime": "2015-07-23T11:07:55-07:00"
    }, 
    "BillAddr": {
      "City": "Half Moon Bay", 
      "Line1": "12 Ocean Dr.", 
      "PostalCode": "94213", 
      "Lat": "37.4307072", 
      "Long": "-122.4295234", 
      "CountrySubDivisionCode": "CA", 
      "Id": "3"
    }, 
    "MiddleName": "Mark", 
    "Taxable": false, 
    "Balance": 85.0, 
    "SyncToken": "1", 
    "CompanyName": "Bill's Windsurf Shop", 
    "FamilyName": "Lucchini", 
    "PrintOnCheckName": "Bill's Windsurf Shop", 
    "sparse": false, 
    "Id": "2"
  }, 
  "time": "2015-07-23T11:07:55.772-07:00"
}
```