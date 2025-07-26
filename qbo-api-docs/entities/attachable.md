# Attachable

This page covers the Attachable, Upload, and Download resources used for attachment management. Attachments are supplemental information linked to a transaction or Item object. They can be files, notes, or a combination of both.

In the case of file attachments, use an upload endpoint multipart request to upload the files to the QuickBooks attachment list and, optionally, to supply metadata for each via an attachable object. If meta data is not supplied with the upload request, the system creates it.

In the case of a note, use the create attachable endpoint.

## Business Rules

- An upload request may contain as many files as possible in a request, but the overall request size must not exceed 100 MB.
- An attachable record can either contain a note only, a file attachment only, or both.
- When using file FileName and Note attributes together, it's up to the app to manage how the note relates to the file name.

## The attachable object

### Attributes

- **Id** (read only, system defined, IdType, filterable, sortable) - Unique Identifier for an Intuit entity (object). Required for the update operation.

- **SyncToken** (read only, system defined, String) - Version number of the object. It is used to lock an object for use by one app at a time. As soon as an application modifies an object, its SyncToken is incremented. Attempts to modify an object specifying an older SyncToken fails. Only the latest version of the object is maintained by QuickBooks Online. Required for update.

- **FileName** (Conditionally required, max 1000 chars, String, filterable, sortable) - FileName of the attachment. Required for file attachments.

- **Note** (Conditionally required, max 2000 chars, String, filterable, sortable) - This note is either related to the attachment specified by FileName or is a standalone note. Required for standalone notes.

- **Category** (Optional, max 100 chars, String, filterable, sortable) - Category of the attachment. Valid values include (case sensitive): Contact Photo, Document, Image, Receipt, Signature, Sound, Other.

- **ContentType** (Optional, max 100 chars, String, filterable, sortable) - ContentType of the attachment. Returned for file attachments.

- **PlaceName** (Optional, max 2000 chars, String, filterable, sortable) - PlaceName from where the attachment was requested.

- **AttachableRef** (Optional, AttachableRef) - Specifies the transaction object to which this attachable file is to be linked.

- **Long** (Optional, max 100 chars, String, filterable, sortable) - Longitude from where the attachment was requested.

- **Tag** (Optional, max 2000 chars, String, filterable, sortable) - Tag name for the requested attachment.

- **Lat** (Optional, max 100 chars, String, filterable, sortable) - Latitude from where the attachment was requested.

- **MetaData** (Optional, ModificationMetaData) - Descriptive information about the entity. The MetaData values are set by Data Services and are read only for all applications.

- **FileAccessUri** (read only, system defined, String) - FullPath FileAccess URI of the attachment. Returned for file attachments.

- **Size** (read only, system defined, Decimal, filterable, sortable) - Size of the attachment. Returned for file attachments.

- **ThumbnailFileAccessUri** (read only, system defined, String) - FullPath FileAccess URI of the attachment thumbnail if the attachment file is of a content type with thumbnail support. Returned for file attachments.

- **TempDownloadUri** (read only, system defined, String) - TempDownload URI which can be directly downloaded by clients. Returned for file attachments.

- **ThumbnailTempDownloadUri** (read only, system defined, String, filterable, sortable) - Thumbnail TempDownload URI which can be directly downloaded by clients. This is only available if the attachment file is of a content type with thumbnail support. Returned for file attachments.

### Sample Object

```json
{
  "Attachable": {
    "SyncToken": "0", 
    "domain": "QBO", 
    "AttachableRef": [
      {
        "IncludeOnSend": false, 
        "EntityRef": {
          "type": "Invoice", 
          "value": "95"
        }
      }
    ], 
    "Note": "This is an attached note.", 
    "sparse": false, 
    "Id": "200900000000000008541", 
    "MetaData": {
      "CreateTime": "2015-11-17T11:05:15-08:00", 
      "LastUpdatedTime": "2015-11-17T11:05:15-08:00"
    }
  }, 
  "time": "2015-11-17T11:05:15.797-08:00"
}
```

## Operations

### Create a note attachment

Use this endpoint to attach a note to the an object. Adjust values in the AttachableRef element for your specific target object. The value for AttachableRef.EntityRef.value is the Id of the target object as returned in its response body when queried.

#### Request URL

```
POST /v3/company/<realmID>/attachable
Content type: application/json
Production Base URL: https://quickbooks.api.intuit.com
Sandbox Base URL: https://sandbox-quickbooks.api.intuit.com
```

#### Request Body

```json
{
  "Note": "This is an attached note.", 
  "AttachableRef": [
    {
      "IncludeOnSend": "false", 
      "EntityRef": {
        "type": "Invoice", 
        "value": "95"
      }
    }
  ]
}
```

### Delete an attachable

This operation deletes the attachable object specified in the request body. The request body must include the full payload of the attachable as returned in a read response.

#### Request URL

```
POST /v3/company/<realmID>/attachable?operation=delete
Content type: application/json
Production Base URL: https://quickbooks.api.intuit.com
Sandbox Base URL: https://sandbox-quickbooks.api.intuit.com
```

### Download an attachment

Retrieves a temporary download URL to the specified attchableID as returned in the attachable.Id attribute from a read response. The application uses this URL to then download the file as a separate step. The URL expires after 15 minutes, after which time the app may obtain another.

#### Request URL

```
GET /v3/company/<realmID>/download/<attachableId>
Content type: text/plain
Production Base URL: https://quickbooks.api.intuit.com
Sandbox Base URL: https://sandbox-quickbooks.api.intuit.com
```

### Query an attachable

The sample query returns the attachable ids for all attachments linked to the purchase object whose Id is 611. To formulate this query, you must first know the type of object and its object Id using the query endpoint for that resource.

#### Request URL

```
GET /v3/company/<realmID>/query?query=<selectStatement>
Content type: text/plain
Production Base URL: https://quickbooks.api.intuit.com
Sandbox Base URL: https://sandbox-quickbooks.api.intuit.com
```

#### Sample Query

```sql
select Id from attachable where 
AttachableRef.EntityRef.Type = 'purchase' and 
AttachableRef.EntityRef.value = '611'
```

### Read an attachable

Retrieves the details of an attachable item that has been previously created.

#### Request URL

```
GET /v3/company/<realmID>/attachable/<attachableId>
Production Base URL: https://quickbooks.api.intuit.com
Sandbox Base URL: https://sandbox-quickbooks.api.intuit.com
```

### Full update an attachable

Use this operation to update any of the writable fields of an existing attachable object. The request body must include all writable fields of the existing object as returned in a read response. Writable fields omitted from the request body are set to NULL. The ID of the object to update is specified in the request body.

#### Request URL

```
POST /v3/company/<realmID>/attachable
Content type: application/json
Production Base URL: https://quickbooks.api.intuit.com
Sandbox Base URL: https://sandbox-quickbooks.api.intuit.com
```

### Upload attachments

The upload endpoint allows the app to upload one or more attachments, with or without associated metadata, via a multipart/form-data request.

#### Request URL

```
POST /v3/company/<realmID>/upload
Content type: multipart/form-data
Production Base URL: https://quickbooks.api.intuit.com
Sandbox Base URL: https://sandbox-quickbooks.api.intuit.com
```

#### Request Body Example

```json
{
  "AttachableRef": [
    {
      "EntityRef": {
        "type": "Invoice", 
        "value": "95"
      }
    }
  ], 
  "ContentType": "image/jpg", 
  "FileName": "receipt_nov15.jpg"
}
```

## Supported File Types for Upload

Supported file types for uploading include various document, image, and media formats. Check the QuickBooks API documentation for the most up-to-date list of supported file types.