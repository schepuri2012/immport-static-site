Posting updates/validation and acquiring information about them in the Data
Batch Updater API is accomplished by making endpoints to the API endpoints.

The HTTP URL that corresponds to the Data Batch Updater API endpoint is
specified as follows:

``` shell
[-X POST] -H "Authorization: bearer $token" [-F Parameterization...] https://immport-upload.niaid.nih.gov:9443/data/batch/updater...
```

The components of the endpoint may require a POST endpoint `[-X POST]`,
-F parameterization `[-F Parameterization..]`, or a completion of the endpoint
`...`.  All this information is presented in the table below. The authorization
token `-H "Authorization: bearer $token"` is described Section **Sample Request
with Authentication** below.  Each POST endpoint is parameterized using -F
parameterization, while non-POST endpoints have an inline parameter except for
the workspaces endpoint.

Each Data Batch Updater API endpoint represents a specific batch updater action,
for example, data batch update, data batch update validation, documentation
generation, etc.

In the Examples below, the value **REPLACE_WITH_USERNAME** will be **testuser**.
Also, the **-F parameter uploadPurpose** where it appears below **MUST BE** as
provided and should **NOT** be modified.

| Endpoint      | POST | Description | HTTP URL     | -F Parameterization |
|---------------|------|-------------| -------------|---------------------|
| Documentation Generation | No | Generate documenation templates | https://immport-upload.niaid.nih.gov:9443/data/batch/updater/documentation/templates | |
| Batch Update Upload | Yes | Request upload of a zip-file; transfers file and creates upload registration and performs batch update requested | https://immport-upload.niaid.nih.gov:9443/data/batch/updater | -F "workspaceId=WORKSPACE_ID" -F "packageName=" -F "uploadNotes=UPLOAD_NOTES" -F "uploadPurpose=batchUpdateUpload" -F "serverName=SERVER_NAME" -F "file=@UPLOAD_BATCH_UPDATER_FILE_PATH_ON_CLIENT" |
| Batch Update Upload for Validation | Yes | Batch update validation is a two step process where the batch update file is uploaded to the server and the upload registration generated (this endpoint), and then the validation is requested (see Validation of Upload Ticket endpoint) | https://immport-upload.niaid.nih.gov:9443/data/batch/updater | -F "workspaceId=WORKSPACE_ID" -F "packageName=" -F "uploadNotes=UPLOAD_NOTES" -F "uploadPurpose=batchUpdateValidate" -F "serverName=SERVER_NAME" -F "file=@UPLOAD_BATCH_UPDATER_FILE_PATH_ON_CLIENT" |
|Validation of Upload Ticket | Yes | Validaton a batch updater file that is identified by the upload ticket number; Note this endpoint uses the -F paramter, `-F "uploadTicketNumber=UPLOAD_TICKET_NUMBER"` | https://immport-upload.niaid.nih.gov:9443/data/batch/updater/validation | -F "uploadTicketNumber=UPLOAD_TICKET_NUMBER" |
| Status of Upload Ticket | No | Return the current status of an upload ticket (UPLOAD_TICKET_NUMBER) | https://immport-upload.niaid.nih.gov:9443/data/batch/updater/registration/UPLOAD_TICKET_NUMBER/status | |
| Summary Information on Upload Ticket | No | On completed jobs (either Completed or Rejected), provide the informaton on the upload ticket (UPLOAD_TICKET_NUMBER) | https://immport-upload.niaid.nih.gov:9443/data/batch/updater/registration/UPLOAD_TICKET_NUMBER/summary | |
| Database Information on Upload Ticket | No | On completed jobs (Completed only) provide database information (UPLOAD_TICKET_NUMBER) | https://immport-upload.niaid.nih.gov:9443/data/batch/updater/registration/UPLOAD_TICKET_NUMBER/database | |
| Set of Workspaces | No | Return the set of workspace(s) on which a user can perform and upload or validation | https://immport-upload.niaid.nih.gov:9443/workspaces | |
