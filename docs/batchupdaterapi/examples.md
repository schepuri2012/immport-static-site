## Batch Update Upload Request with Authentication

The following is an example of an batch update request to upload a file and
perform the requested updates, where several -F parameters are used.  Note that
**packageName** parameter **MUST NOT** have a value.

!!! example "Shell Script - Batch Update Upload Request"
    ```
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -X POST -H "Authorization: bearer $token" -F "workspaceId=REPLACE_WITH_WORKSPACE_ID" -F "packageName=" -F "uploadNotes=" -F "uploadPurpose=batchUpdateUpload" -F "serverName=" -F "file=@/home/tsmith/Downloads/UpdateValue.Reagent.txt" https://immport-upload.niaid.nih.gov:9443/data/batch/updater
    ```

??? example "Results"
    ``` response
    {
      "uploadTicketNumber" : "testuser_20180523_19555",
      "uploadPurpose" : "batchUpdateUpload",
      "workspaceId" : 999999,
      "status" : "Pending_Batch_Updater"
    }
    ```

The first line is a POST to the authentication URL
`https://auth.immport.org/auth/token` with the username and password to get an
authentication token. The fgrep command is used search the response for a token
and then assign the value of the token to an environment variable named
**"token"**.

The second line is a POST on the URL
`https://immport-upload.niaid.nih.gov:9443/data/batch/updater`
with the -F parameterization. The authentication token (**"token"**) is passed
in the HTTP header as shown.  The following -F parameters need values:
workspaceId and file (client-path to batch update file), while uploadNotes and
serverName can have optional values.  The parameter **packageName MUST NOT**
have a value.  The value of **uploadPurpose** must be what is provided above
**as-is**.

The response will be JSON that provides the upload ticket number (to used in
information endpoints), the upload purpose, the workspace_id, and the current status
of the upload request.

The above shell script or any code starting with #!/bin/bash can be copied to a
.sh file (e.g. uploadBatchFile.sh )and executed at the command prompt of
a terminal and the output can be directed to a file. (Please replace the
REPLACE_WITH_USERNAME with your username, and REPLACE_WITH_PASSWORD with your
password).

``` shell
./uploadBatchFile.sh > uploadBatchFile.json
```

## Batch Update Validation Request with Authentication

The following is an example of validation of a batch update file, where several -F
parameters are used.  Note that packageName parameter must not have a value.
Also, validation is a two endpoint (step) process.  The first step is to upload the
batch update file to the server and create the ticket, and the second is to request the
validation of the batch update file.  To obtain the validation report, the user must
obtain the database report (See Section **Database Report Request with
Authentication**) using the upload ticket number obtained from the validation
request.

!!! example "Shell Script - Batch Update Validation Request"
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -X POST -H "Authorization: bearer $token" -F "workspaceId=REPLACE_WITH_WORKSPACE_ID" -F "packageName=" -F "uploadNotes=" -F "uploadPurpose=batchUpdateValidate" -F "serverName=" -F "file=@/home/tsmith/Downloads/UpdateValue.Reagent.txt" https://immport-upload.niaid.nih.gov:9443/data/batch/updater
    ```

??? example "Results"
    ``` response
    {
      "uploadTicketNumber" : "testuser_20180523_19554",
      "uploadPurpose" : "batchUpdateValidate",
      "workspaceId" : 999999,
      "status" : "Pending_Batch_Updater_Validation"
    }
    ```

The first line is a POST to the authentication URL
`https://auth.immport.org/auth/token` with the username and password to get an
authentication token. The fgrep command is used search the response for a token
and then assign the value of the token to an environment variable named
**"token"**.

The second line is a POST on the URL
`https://immport-upload.niaid.nih.gov:9443/data/batch/updater`
with the -F parameterization. The authentication token (**"token"**) is passed
in the HTTP header as shown.  The following parameters need values: workspaceId
and file (client-path to batch update file), while uploadNotes and serverName
can have optional values.  The parameter **packageName MUST NOT** have a value.
The value of **uploadPurpose** must be what is provided above **as-is**.

The response will be a JSON that provides the upload ticket number (to used in
information endpoints), the upload purpose, the workspace_id, and the current status
of the validation request.

The above shell script or any code starting with #!/bin/bash can be copied to a
.sh file (e.g. validateUploadBatchFile.sh )and executed at the command prompt of a
terminal and the output can be directed to a file. (Please replace the
REPLACE_WITH_USERNAME with your username, and REPLACE_WITH_PASSWORD with your
password)

``` shell
./validateUploadBatchFile.sh > validateUploadBatchFile.json
```

## Validation of Upload Ticket with Authentication


!!! example "Shell Script - Check Validation of Batch Upload Ticket" 
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -H "Authorization: bearer $token" -F "uploadTicketNumber=testuser_20180523_19554" https://immport-upload.niaid.nih.gov:9443/data/batch/updater/validation
    ```

??? example "Results"
    ``` response
    {
      "uploadTicketNumber" : "testuser_20180523_19554",
      "status" : "Completed_Batch_Updater_Validation"
    }
    ```

The first line is a POST to the authentication URL
`https://auth.immport.org/auth/token` with the username and password to get an
authentication token. The fgrep command is used search the response for a token
and then assign the value of the token to an environment variable named
**"token"**.

The second line is a POST on the URL
`https://immport-upload.niaid.nih.gov:9443/data/batch/updater/validation`
The authentication token (**"token"**) is passed in the HTTP header as shown.
The **-F parameter uploadTicketNumber** must contain the upload ticket number
obtained from the the upload request response above (**Validation of Upload
Ticket with Authentication**).

The response will be JSON that provides the upload ticket number (to used in
information endpoints) and the current status of the validation request.

The above shell script or any code starting with #!/bin/bash can be copied to a
.sh file (e.g. validateFile.sh )and executed at the command prompt of a
terminal and the output can be directed to a file. (Please replace the
REPLACE_WITH_USERNAME with your username, and REPLACE_WITH_PASSWORD with your
password)

``` shell
./validateFile.sh > validateFile.json
```

## Status of Upload Ticket with Authentication

The following is an example of a request for status of an batch updater ticket
number where an inline parameter (UPLOAD_TICKET_NUMBER) is used.

!!! example "Shell Script - Check Status of Batch Upload Ticket" 
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -H "Authorization: bearer $token" https://immport-upload.niaid.nih.gov:9443/data/batch/updater/registration/testuser_20180523_19555/status
    ```

??? example "Results"
    ``` response
    {
      "uploadTicketNumber" : "testuser_20180523_19555",
      "status" : "Completed_Batch_Updater"
    }
    ```

The first line is a POST to the authentication URL
`https://auth.immport.org/auth/token` with the username and password to get an
authentication token. The fgrep command is used search the response for a token
and then assign the value of the token to an environment variable named
**"token"**.

The second line is an inline Non-POST URL
`https://immport-upload.niaid.nih.gov:9443/data/batch/updater/registration/testuser_20180523_19554/status`
with the inline parameterization, UPLOAD_TICKET_NUMBER. The authentication token
(**"token"**) is passed in the HTTP header as shown.

The response will be JSON that provides the current status of the request.

The above shell script or any code starting with #!/bin/bash can be copied to a
.sh file (e.g. uploadStatus.sh )and executed at the command prompt of
a terminal and the output can be directed to a file. (Please replace the
REPLACE_WITH_USERNAME with your username, and REPLACE_WITH_PASSWORD with your
password).

``` shell
./uploadStatus.sh > uploadStatus.json
```

## Validation Summary Information on Upload Ticket Request with Authentication

The following is an example of a request for summary report status of a batch
update validation using an upload ticket number, where an inline parameter
(UPLOAD_TICKET_NUMBER) is used.

!!! example "Shell Script - Validation Summary Information for Batch Upload Ticket" 
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -H "Authorization: bearer $token" https://immport-upload.niaid.nih.gov:9443/data/batch/updater/registration/testuser_20180523_19554/reports/summary
    ```

??? example "Results"
    ``` response
    {
      "summary" : {
        "uploadRegistrationId" : 19554,
        "workspaceName" : "Test Creation Scripts I",
        "fileName" : "UpdateValue.Reagent.txt",
        "status" : "Completed_Batch_Updater_Validation",
        "uploadTicketNumber" : "testuser_20180523_19554",
        "dateCreated" : "2018-05-23",
        "createdBy" : "testuser",
        "uploadMethod" : "Secure Web",
        "uploadRegistrationResults" : [ {
          "uploadRegistrationResultId" : 1101379,
          "description" : "server name:",
          "errorMessage" : null,
          "fileName" : "UpdateValue.Reagent.txt",
          "lineNumber" : null,
          "status" : "Completed_Batch_Updater_Validation",
          "uploadTicketNumber" : "testuser_20180523_19554",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        } ]
      },
      "uploadTicketNumber" : "testuser_20180523_19554",
      "type" : "summary"
    }
    ```

## Summary Report on Upload Ticket Request with Authentication
The following is an example of a request for summary report status of a batch
update upload using an upload ticket number, where an inline parameter
(UPLOAD_TICKET_NUMBER) is used.

!!! example "Shell Script - Summary Report Information for Batch Upload Ticket" 
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -H "Authorization: bearer $token" https://immport-upload.niaid.nih.gov:9443/data/batch/updater/registration/testuser_20180523_19555/reports/summary
    ```

??? example "Results"
    ``` response
    {
      "summary" : {
        "uploadRegistrationId" : 19555,
        "workspaceName" : "Test Creation Scripts I",
        "fileName" : "UpdateValue.Reagent.txt",
        "status" : "Completed_Batch_Updater",
        "uploadTicketNumber" : "testuser_20180523_19555",
        "dateCreated" : "2018-05-23",
        "createdBy" : "testuser",
        "uploadMethod" : "Secure Web",
        "uploadRegistrationResults" : [ {
          "uploadRegistrationResultId" : 1101380,
          "description" : "server name:",
          "errorMessage" : null,
          "fileName" : "UpdateValue.Reagent.txt",
          "lineNumber" : null,
          "status" : "Registered_Batch_Updater",
          "uploadTicketNumber" : "testuser_20180523_19555",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101381,
          "description" : null,
          "errorMessage" : null,
          "fileName" : "UpdateValue.Reagent.txt",
          "lineNumber" : 0,
          "status" : "Started_Batch_Updater",
          "uploadTicketNumber" : "testuser_20180523_19555",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101382,
          "description" : "Size:2180 bytes",
          "errorMessage" : null,
          "fileName" : "testuser_20180523_19555___UpdateValue.Reagent.txt",
          "lineNumber" : 0,
          "status" : "Parsing",
          "uploadTicketNumber" : "testuser_20180523_19555",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101383,
          "description" : "The header was read as follows: [data_columns => analyte_preferred~analyte_reported, format => update_value, key_columns => reagent_accession, table_name => reagent]",
          "errorMessage" : null,
          "fileName" : "testuser_20180523_19555___UpdateValue.Reagent.txt",
          "lineNumber" : 71,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19555",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101384,
          "description" : "The data_columns are [analyte_preferred, analyte_reported].",
          "errorMessage" : null,
          "fileName" : "testuser_20180523_19555___UpdateValue.Reagent.txt",
          "lineNumber" : 71,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19555",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101385,
          "description" : "Parsing the line with primaryKey [reagent_accession] whose value is [ESR20973].",
          "errorMessage" : null,
          "fileName" : "testuser_20180523_19555___UpdateValue.Reagent.txt",
          "lineNumber" : 73,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19555",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101386,
          "description" : "Parsing the line with dataColumns [analyte_preferred, analyte_reported] whose values are [ANA40, CD27].",
          "errorMessage" : null,
          "fileName" : "testuser_20180523_19555___UpdateValue.Reagent.txt",
          "lineNumber" : 73,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19555",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101387,
          "description" : "Size:2180 bytes",
          "errorMessage" : null,
          "fileName" : "testuser_20180523_19555___UpdateValue.Reagent.txt",
          "lineNumber" : 0,
          "status" : "Parsed",
          "uploadTicketNumber" : "testuser_20180523_19555",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101388,
          "description" : null,
          "errorMessage" : null,
          "fileName" : "UpdateValue.Reagent.txt",
          "lineNumber" : 0,
          "status" : "Completed_Batch_Updater",
          "uploadTicketNumber" : "testuser_20180523_19555",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        } ]
      },
      "uploadTicketNumber" : "testuser_20180523_19555",
      "type" : "summary"
    }
    ```

The first line is a POST to the authentication URL
`https://auth.immport.org/auth/token` with the username and password to get an
authentication token. The fgrep command is used search the response for a token
and then assign the value of the token to an environment variable named
**"token"**.

The second line is an inline Non-POST URL
`https://immport-upload.niaid.nih.gov:9443/data/batch/updater/registration/testuser_20180523_19554/reports/summary`
with the inline parameterization, UPLOAD_TICKET_NUMBER. The authentication token
(**"token"**) is passed in the HTTP header as shown.

The response will be JSON that provides the summary of the upload request.

The above shell script or any code starting with #!/bin/bash can be copied to a
.sh file (e.g. uploadSummaryReport.sh )and executed at the command prompt of
a terminal and the output can be directed to a file. (Please replace the
REPLACE_WITH_USERNAME with your username, and REPLACE_WITH_PASSWORD with your
password).

``` shell
./uploadSummaryReport.sh > uploadSummaryReport.json
```

## Database Information on Upload Ticket Request with Authentication

The following is an example of a request for the database report for an
validation using an upload ticket number where an inline parameter
(UPLOAD_TICKET_NUMBER) is used.

!!! example "Shell Script - Database Information for Batch Upload Ticket" 
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -H "Authorization: bearer $token" https://immport-upload.niaid.nih.gov:9443/data/batch/updater/registration/testuser_20180523_19554/reports/database
    ```

??? example "Results"
    ``` response
    {
      "database" : "********************************************* Batch Updater Job Report *********************************************\n\nThe validation report is based on ImmPort workspace (workspace_id = 999999).\nThe validation report was generated on 2018-05-23-21:02:43.\nThe data package file submitted was /home/immport/data/immport-data-upload-server/webupload_drop_zone/testuser_20180523_19554___UpdateValue.Reagent.txt.\n\nLine Number\tStatus\tError Message\tDescription\n0\tParsing\t\tSize:2180 bytes\n71\tInformation\t\tThe header was read as follows: [data_columns => analyte_preferred~analyte_reported, format => update_value, key_columns => reagent_accession, table_name => reagent]\n71\tInformation\t\tThe data_columns are [analyte_preferred, analyte_reported].\n73\tInformation\t\tParsing the line with primaryKey [reagent_accession] whose value is [ESR20973].\n73\tInformation\t\tParsing the line with dataColumns [analyte_preferred, analyte_reported] whose values are [ANA40, CD27].\n0\tParsed\t\tSize:2180 bytes\n0\tCompleted_Batch_Updater\t\t\n\n******************************************** Database Submission Report *********************************************\n\nThe Database Submission Report is Empty.\n",
      "uploadTicketNumber" : "testuser_20180523_19554",
      "type" : "database"
    }
    ```

The first line is a POST to the authentication URL
`https://auth.immport.org/auth/token` with the username and password to get an
authentication token. The fgrep command is used search the response for a token
and then assign the value of the token to an environment variable named
**"token"**.

The second line is an inline Non-POST URL
`https://immport-upload.niaid.nih.gov:9443/data/batch/updater/registration/testuser_20180523_19554/reports/database`
with the inline parameterization UPLOAD_TICKET_NUMBER. The authentication token
(**"token"**) is passed in the HTTP header as shown.

The response will be JSON that provides the database report of the upload request.

The above shell script or any code starting with #!/bin/bash can be copied to a
.sh file (e.g. uploadDatabaseport.sh )and executed at the command prompt of
a terminal and the output can be directed to a file. (Please replace the
REPLACE_WITH_USERNAME with your username, and REPLACE_WITH_PASSWORD with your
password).

``` shell
./uploadDatabaseport.sh > uploadDatabaseport.json
```

## Set of Workspaces Request with Authentication

The following is an example of a request for the set of workspace upon which the
user can upload and validate data.

!!! example "Shell Script - Workspaces for a User" 
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -H "Authorization: bearer $token" https://immport-upload.niaid.nih.gov:9443/workspaces
    ```

??? example "Results"
    ``` response
    {
      "workspaces" : [ {
        "workspaceId" : 999999,
        "name" : "Test Creation Scripts I",
        "type" : "PW",
        "category" : "LSR",
        "dateCreated" : 1524159239000,
        "dateLastUpdated" : 1524159239000,
        "createdBy" : "tsmith",
        "lastUpdatedBy" : "SYSTEM"
      }, {
        "workspaceId" : 999996,
        "name" : "Test Creation Scripts III",
        "type" : "PW",
        "category" : "LSR",
        "dateCreated" : 1524158615000,
        "dateLastUpdated" : 1524158615000,
        "createdBy" : "tsmith",
        "lastUpdatedBy" : "SYSTEM"
      }, {
        "workspaceId" : 999998,
        "name" : "Test Creation Scripts III",
        "type" : "PW",
        "category" : "LSR",
        "dateCreated" : 1524159474000,
        "dateLastUpdated" : 1524159474000,
        "createdBy" : "tsmith",
        "lastUpdatedBy" : "SYSTEM"
      }, {
        "workspaceId" : 5768,
        "name" : "Test Workspace for user testuser",
        "type" : "PW",
        "category" : "TEST",
        "dateCreated" : 1516303125000,
        "dateLastUpdated" : 1516303125000,
        "createdBy" : "testadmin",
        "lastUpdatedBy" : "testadmin"
      }, {
        "workspaceId" : 5787,
        "name" : "test assessments",
        "type" : "PW",
        "category" : "TEST",
        "dateCreated" : 1519228020000,
        "dateLastUpdated" : 1519228020000,
        "createdBy" : "pattybe",
        "lastUpdatedBy" : "pattybe"
      } ]
    }
    ```

The first line is a POST to the authentication URL
`https://auth.immport.org/auth/token` with the username and password to get an
authentication token. The fgrep command is used search the response for a token
and then assign the value of the token to an environment variable named
**"token"**.

The second line is a Non-POST URL
`https://immport-upload.niaid.nih.gov:9443/workspaces`
The authentication token (**"token"**) is passed in the HTTP header as shown.

The response will be JSON that provides the list of workspaces upon which a user may upload and validate.

The above shell script or any code starting with #!/bin/bash can be copied to a
.sh file (e.g. workspaces.sh )and executed at the command prompt of
a terminal and the output can be directed to a file. (Please replace the
REPLACE_WITH_USERNAME with your username, and REPLACE_WITH_PASSWORD with your
password).

``` shell
./workspaces.sh > workspaces.json
```
