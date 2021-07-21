Posting uploads/validation and acquiring information about them in the Data
Upload API is accomplished by making calls to the API endpoints.

The HTTP URL that corresponds to the Data Upload API endpoint is specified as
follows:

``` shell
[-X POST] -H "Authorization: bearer $token" [-F Parameterization...] https://immport-upload.niaid.nih.gov:8443/data/upload...
```

The components of the endpoint may require a POST call `[-X POST]`, 
-F parameterization `[-F Parameterization..]`, or a completion of the endpoint
`...`.  All this information is presented in the table below. The authorization
token `-H "Authorization: bearer $token"` is described Section **Sample Request
with Authentication** below.  Each POST endpoint is parameterized using -F
parameterization, while non-POST endpoints have an inline parameter except for
the workspaces endpoint.

Each Data Upload API endpoint represents a specific batch upload action, for
example, data upload, data validation, documentation generation, etc.

In the Examples below, the **-F parameter uploadPurpose** where it appears below **MUST BE** as
provided and should **NOT** be modified.

| Endpoint      | POST | Description | HTTP URL     | -F Parameterization |
|---------------|------|-------------| -------------|---------------------|
| Documentation Generation | No | Generate documenation templates for a specific workspace (WORKSPACE_ID) | https://immport-upload.niaid.nih.gov:8443 /data/upload/documentation  /templates/WORKSPACE_ID | |
| OffLine File(s) Upload | Yes | Request for an off-line upload; creates upload registration in preparation for receipt of the file | https://immport-upload.niaid.nih.gov:8443 /data/upload/type/offline | -F "workspaceId=WORKSPACE_ID" -F "packageName=PACKAGE_NAME" -F "uploadNotes=UPLOAD_NOTES" -F "uploadPurpose=uploadData" -F "serverName=SERVER_NAME" |
| Zip-File Upload | Yes | Request upload of a zip-file; transfers file and creates upload registration and performs upload | https://immport-upload.niaid.nih.gov:8443  /data/upload/type/online | -F "workspaceId=WORKSPACE_ID" -F "packageName=" -F "uploadNotes=UPLOAD_NOTES" -F "uploadPurpose=uploadData" -F "serverName=SERVER_NAME" -F "file=@UPLOAD_ZIP_FILE_PATH_ON_CLIENT" |
| Multiple Files Upload (Single File) | Yes | Request upload of a single file; transfers file and creates upload registration and performs upload; Note that single file is specified with the following -F parameter, `-F "file=@UPLOAD_FILE_PATH_ON_CLIENT"` | https://immport-upload.niaid.nih.gov:8443  /data/upload/type/online | -F "workspaceId=WORKSPACE_ID" -F "packageName=PACKAGE_NAME" -F "uploadNotes=UPLOAD_NOTES" -F "uploadPurpose=uploadData" -F "serverName=SERVER_NAME" -F "file=@UPLOAD_FILE_PATH_ON_CLIENT" |
| Multiple Files Upload (Multiple Files) | Yes | Request upload of a several files; transfers files and creates upload registration and performs upload; Note that each file is specified with the following -F parameter, `-F "file=@UPLOAD_FILE_PATH_ON_CLIENT"` | https://immport-upload.niaid.nih.gov:8443  /data/upload/type/online | -F "workspaceId=WORKSPACE_ID" -F "packageName=PACKAGE_NAME" -F "uploadNotes=UPLOAD_NOTES" -F "uploadPurpose=uploadData" -F "serverName=SERVER_NAME" -F "file=@UPLOAD_FILE1_PATH_ON_CLIENT" -F "file=@UPLOAD_FILE_PATH_ON_CLIENT" ... |
| Zip-file Upload for Validation | Yes | Zip-file validation is a two step process where the zip-file is uploaded to the server and the upload registration generated and then the validation is requested (see Validation of a File) | https://immport-upload.niaid.nih.gov:8443 /data/upload/type/online | -F "workspaceId=WORKSPACE_ID" -F "packageName=" -F "uploadNotes=UPLOAD_NOTES" -F "uploadPurpose=uploadData" -F "serverName=SERVER_NAME" -F "file=@UPLOAD_ZIP_FILE_PATH_ON_CLIENT" |
| Mulitple File Upload for Validation (Single File) | Yes | Request a validation of a single file not as a zip-file package; Note that the single file is specified with the following -F parameter, `-F "file=@UPLOAD_FILE_PATH_ON_CLIENT"` | https://immport-upload.niaid.nih.gov:8443  /data/upload/type/online | -F "workspaceId=WORKSPACE_ID" -F "packageName=PACKAGE_NAME" -F "uploadNotes=UPLOAD_NOTES" -F "uploadPurpose=validateData" -F "serverName=SERVER_NAME" -F "file=@UPLOAD_FILE_PATH_ON_CLIENT" |
| Mulitple File Upload for Validation (Multiple Files) | Yes | Request upload of several files not as a zip-file package; Note that each file is specified with the following -F parameter, `-F "file=@UPLOAD_FILE_PATH_ON_CLIENT"` | https://immport-upload.niaid.nih.gov:8443 /data/upload/type/online | -F "workspaceId=WORKSPACE_ID" -F "packageName=PACKAGE_NAME" -F "uploadNotes=UPLOAD_NOTES" -F "uploadPurpose=validateData" -F "serverName=SERVER_NAME" -F "file=@UPLOAD_FILE1_PATH_ON_CLIENT" -F "file=@UPLOAD_FILE_PATH_ON_CLIENT" ... |
|Validation of Upload Ticket | Yes | Validaton of job that is identified by the upload ticket number; Note this endpoint uses the -F parameter, `-F "uploadTicketNumber=UPLOAD_TICKET_NUMBER"` | https://immport-upload.niaid.nih.gov:8443  /data/upload/validation | -F "uploadTicketNumber=UPLOAD_TICKET_NUMBER" |
| Status of Upload Ticket | No | Return the current status of an upload ticket (UPLOAD_TICKET_NUMBER) | https://immport-upload.niaid.nih.gov:8443 /data/upload/registration /UPLOAD_TICKET_NUMBER/status | |
| Summary Information on Upload Ticket | No | On completed jobs (either Completed or Rejected), provide the informaton on the upload ticket (UPLOAD_TICKET_NUMBER)| https://immport-upload.niaid.nih.gov:8443 /data/upload/registration /UPLOAD_TICKET_NUMBER/reports/summary | |
| Database Information on Upload Ticket | No | On completed jobs (Completed only) provide database information (UPLOAD_TICKET_NUMBER) | https://immport-upload.niaid.nih.gov:8443 /data/upload/registration  /UPLOAD_TICKET_NUMBER  /reports/database | |
| Set of Workspaces | No | Return the set of workspace(s) on which a user can perform and upload or validation | https://immport-upload.niaid.nih.gov:8443/workspaces | |