## OffLine File(s) Upload Request with Authentication

An offline request is not normally used, unless the ZIP package is quite large, and may be uploaded later using something like Aspera or sending the data to ImmPort using an offline technique. This type of request basically reserves an Upload Ticket in the ImmPort system and then will wait until the large zip-file is moved into the folder on the ImmPort Upload machine, usually by the ImmPort team, for processing.

The following is an example of an offline request to upload a zip-file, where
several -F parameters are used.  Note that the packageName parameter needs to be
filled in with the name of the upload (file or directory--in this case a file
name).  The ticket returned should have a status of **Pending**.  However, since no file
(or directory) is provided, the ticket will not be acted upon until a file is
deposited on the server in the web drop zone.

!!! example "Shell Script - Offline Upload Request" 
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -X POST -H "Authorization: bearer $token" -F "workspaceId=REPLACE_WITH_WORKSPACE_ID" -F "packageName=Test.Fcm_Derived_Data.Comprehensive.zip" -F "uploadNotes=" -F "uploadPurpose=uploadData" -F "serverName=" https://immport-upload.niaid.nih.gov:8443/data/upload/type/offline
    ```

??? example "Results"
    ``` response
    {
      "uploadTicketNumber" : "testuser_20180523_19546",
      "uploadPurpose" : "uploadData",
      "workspaceId" : 999999,
      "status" : "Pending"
    }
    ```

The first line is a POST to the authentication URL
`https://auth.immport.org/auth/token` with the username and password to get an
authentication token. The fgrep command is used to search the response for a token
and then assign the value of the token to an environment variable named
**"token"**.

The second line is a POST on the URL
`https://immport-upload.niaid.nih.gov:8443/data/upload/type/offline`
with the -F parameterization. The authentication token (**"token"**) is passed
in the HTTP header as shown.  The following -F parameters need values:
workspaceId, and packageName, while uploadNotes, and serverName can have
optional values.  The value of **uploadPurpose** must be what is provided above
**as-is**.

The response will be JSON that provides the upload ticket number (used in
information enpoints), the upload purpose, the workspace_id, and the current
status of the upload request.

The above shell script or any code starting with #!/bin/bash can be copied to a
.sh file (e.g. offlineUploadZipFile.sh) and executed at the command prompt of
a terminal and the output can be directed to a file. (Please replace the
REPLACE_WITH_USERNAME with your username, and REPLACE_WITH_PASSWORD with your
password).

``` shell
./offlineUploadZipFile.sh > offlineUploadZipFile.json
```

## Zip-File Upload Request with Authentication

The following is an example of an online request to upload a zip-file, where
several -F parameters are used.  Note that packageName parameter must not have a
value.
!!! example "Shell Script - Upload Zip-File"
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -X POST -H "Authorization: bearer $token" -F "workspaceId=REPLACE_WITH_WORKSPACE_ID" -F "packageName=" -F "uploadNotes=" -F "uploadPurpose=uploadData" -F "serverName=" -F "file=@/home/tsmith/Downloads/Test.Fcm_Derived_Data.Comprehensive.zip" https://immport-upload.niaid.nih.gov:8443/data/upload/type/online
    ```

??? example "Results"
    ``` response
    {
      "uploadTicketNumber" : "testuser_20180523_19544",
      "uploadPurpose" : "uploadData",
      "workspaceId" : 999999,
      "status" : "Pending"
    }
    ```

The first line is a POST to the authentication URL
`https://auth.immport.org/auth/token` with the username and password to get an
authentication token. The fgrep command is used to search the response for a token
and then assign the value of the token to an environment variable named
**"token"**.

The second line is a POST on the URL
`https://immport-upload.niaid.nih.gov:8443/data/upload/type/online`
with the -F parameterization. The authentication token (**"token"**) is passed
in the HTTP header as shown.  The following -F parameters need values:
workspaceId and file (client-path to zip-file), while uploadNotes and serverName
can have optional values.  The parameter **packageName MUST NOT** have a value.
The value of **uploadPurpose** must be what is provided above **as-is**.

The response will be JSON that provides the upload ticket number (used in
information endpoints), the upload purpose, the workspace_id, and the current
status of the upload request.

The above shell script or any code starting with #!/bin/bash can be copied to a
.sh file (e.g. uploadZipFile.sh) and executed at the command prompt of
a terminal and the output can be directed to a file. (Please replace the
REPLACE_WITH_USERNAME with your username, and REPLACE_WITH_PASSWORD with your
password).

``` shell
./uploadZipFile.sh > uploadZipFile.json
```

## Single File Upload Request with Authentication

The following is an example of an online multiple file upload request with a
single file, where several -F parameters are used.  Note that **packageName**
parameter **MUST HAVE** a value.

!!! example "Shell Script - Upload Single File"
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -X POST -H "Authorization: bearer $token" -F "workspaceId=REPLACE_WITH_WORKSPACE_ID" -F "packageName=multiPartFilesUploadSingleFile" -F "uploadNotes=" -F "uploadPurpose=uploadData" -F "serverName=" -F "file=@/home/tsmith/Downloads/reagents.flow_cytometry.txt" https://immport-upload.niaid.nih.gov:8443/data/upload/type/online
    ```
??? example "Results"
    ``` response
    {
      "uploadTicketNumber" : "testuser_20180523_19552",
      "uploadPurpose" : "uploadData",
      "workspaceId" : 999999,
      "status" : "Pending"
    }
    ```

The first line is a POST to the authentication URL
`https://auth.immport.org/auth/token` with the username and password to get an
authentication token. The fgrep command is used to search the response for a token
and then assign the value of the token to an environment variable named
**"token"**.

The second line is a POST on the URL
`https://immport-upload.niaid.nih.gov:8443/data/upload/type/online`
with the -F parameterization. The authentication token (**"token"**) is passed
in the HTTP header as shown.  The following -F parameters need values:
workspaceId, packageName, and file (client-path to single file), while
uploadNotes and serverName can have optional values.  The parameter
**packageName MUST HAVE** a value.  The value of **uploadPurpose** must be what
is provided above **as-is**.

The response will be JSON that provides the upload ticket number (to be used in
information endpoints), the upload purpose, the workspace_id, and the current
status of the upload request.

The above shell script or any code starting with #!/bin/bash can be copied to a
.sh file (e.g. uploadSingleFile.sh )and executed at the command prompt of
a terminal and the output can be directed to a file. (Please replace the
REPLACE_WITH_USERNAME with your username, and REPLACE_WITH_PASSWORD with your
password).

``` shell
./uploadSingleFile.sh > uploadSingleFile.json
```

## Multiple Files Upload Request with Authentication

The following is an example of an online multiple file upload request with
multipe files, where several -F parameters are used.  Note that **packageName**
parameter **MUST HAVE** a value.

!!! example "Shell Script - Upload Multiple Files"
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -X POST -H "Authorization: bearer $token" -F "workspaceId=REPLACE_WITH_WORKSPACE_ID" -F "packageName=multiPartFilesUploadMultipleFiles" -F "uploadNotes=" -F "uploadPurpose=uploadData" -F "serverName=" -F "file=@/home/tsmith/Downloads/test_GE.MA.Affy_study_protocol.txt" -F "file=@/home/tsmith/Downloads/protocols.txt" -F "file=@/home/tsmith/Downloads/cn01adv.txt" -F "file=@/home/tsmith/Downloads/basic_study_design.txt" -F "file=@/home/tsmith/Downloads/MBAA_protocol.txt" https://immport-upload.niaid.nih.gov:8443/data/upload/type/online
    ```

??? example "Results"
    ``` response
    {
      "uploadTicketNumber" : "testuser_20180523_19553",
      "uploadPurpose" : "uploadData",
      "workspaceId" : 999999,
      "status" : "Pending"
    }
    ```

The first line is a POST to the authentication URL
`https://auth.immport.org/auth/token` with the username and password to get an
authentication token. The fgrep command is used search the response for a token
and then assign the value of the token to an environment variable named
**"token"**.

The second line is a POST on the URL
`https://immport-upload.niaid.nih.gov:8443/data/upload/type/online`
with the -F parameterization. The authentication token (**"token"**) is passed
in the HTTP header as shown.  The following -F parameters need values:
workspaceId, packageName, and files (client-path to multiple files), while
uploadNotes and serverName can have optional values.  The parameter
**packageName MUST HAVE** a value.  The value of **uploadPurpose** must be what
is provided above **as-is**.

The response will be JSON that provides the upload ticket number (to be used in
information endpoints), the upload purpose, the workspace_id, and the current
status of the upload request.

The above shell script or any code starting with #!/bin/bash can be copied to a
.sh file (e.g. uploadMultipleFiles.sh )and executed at the command prompt of
a terminal and the output can be directed to a file. (Please replace the
REPLACE_WITH_USERNAME with your username, and REPLACE_WITH_PASSWORD with your
password).

``` shell
./uploadMultipleFiles.sh > uploadMultipleFiles.json
```

## Zip-file Upload for Validation with Authentication
The following is an example of validation of a zip-file, where several -F
parameters are used.  Note that packageName parameter must not have a value.
Also, validation is a two endpoint (step) process.  The first step is to upload
the zip-file to the server and create the ticket, and the second is to request
the validation of the zip-file.  To obtain the validation report, the user must
obtain the database report (See Section **Database Report Request with
Authentication**) using the upload ticket number obtained from the validation
request.


!!! example "Shell Script - Upload Zip-file for Validation"
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -X POST -H "Authorization: bearer $token" -F "workspaceId=REPLACE_WITH_WORKSPACE_ID" -F "packageName=" -F "uploadNotes=" -F "uploadPurpose=validateData" -F "serverName=" -F "file=@/home/tsmith/Downloads/Test.Fcm_Derived_Data.Comprehensive.zip" https://immport-upload.niaid.nih.gov:8443/data/upload/type/online
    ```

??? example "Results"
    ``` response
    {
      "uploadTicketNumber" : "testuser_20180523_19543",
      "uploadPurpose" : "validateData",
      "workspaceId" : 999999,
      "status" : "Pending_Validation"
    }
    ```

The first line is a POST to the authentication URL
`https://auth.immport.org/auth/token` with the username and password to get an
authentication token. The fgrep command is used search the response for a token
and then assign the value of the token to an environment variable named
**"token"**.

The second line is a POST on the URL
`https://immport-upload.niaid.nih.gov:8443/data/upload/type/online`
with the -F parameterization. The authentication token (**"token"**) is passed
in the HTTP header as shown.  The following parameters need values: workspaceId
and file (client-path to zip-file), while uploadNotes and serverName can have
optional values.  The parameter **packageName MUST NOT** have a value.  The
value of **uploadPurpose** must be what is provided above **as-is**.

The response will be JSON that provides the upload ticket number (to used in
information endpoints), the upload purpose, the workspace_id, and the current
status of the validation request.

The above shell script or any code starting with #!/bin/bash can be copied to a
.sh file (e.g. validateUploadZipFile.sh )and executed at the command prompt of a
terminal and the output can be directed to a file. (Please replace the
REPLACE_WITH_USERNAME with your username, and REPLACE_WITH_PASSWORD with your
password)

``` shell
./validateUploadZipFile.sh > validateUploadZipFile.json
```

## Validation of Upload Ticket with Authentication

!!! example "Shell Script - Request Upload Ticket Validation"
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -X POST -H "Authorization: bearer $token" -F "uploadTicketNumber=testuser_20180523_19543" https://immport-upload.niaid.nih.gov:8443/data/upload/validation
    ```

??? example "Results"
    ``` response
    {
      "uploadTicketNumber" : "testuser_20180523_19543",
      "status" : "Completed_Validation"
    }
    ```

The first line is a POST to the authentication URL
`https://auth.immport.org/auth/token` with the username and password to get an
authentication token. The fgrep command is used search the response for a token
and then assign the value of the token to an environment variable named
**"token"**.

The second line is a POST on the URL
`https://immport-upload.niaid.nih.gov:8443/data/upload/validation`
The authentication token (**"token"**) is passed in the HTTP header as shown.
The **-F parameter uploadTicketNumber** must contain the upload ticket number
obtained from the the upload request response above (**Upload Zip File to
Server**).

The response will be a JSON that provides the upload ticket number (to be used in
information endpoints) and the current status of the validation request.

The above shell script or any code starting with #!/bin/bash can be copied to a
.sh file (e.g. validateZipFile.sh )and executed at the command prompt of a
terminal and the output can be directed to a file. (Please replace the
REPLACE_WITH_USERNAME with your username, and REPLACE_WITH_PASSWORD with your
password)

``` shell
./validateZipFile.sh > validateZipFile.json
```

## Single File Upload for Validation Request with Authentication

The following is an example of validation of a single file, where several -F
parameters are used.  Note that **packageName** parameter **MUST HAVE** a value.
Also, validation is a two endpoint (step) process.  The first step is to upload
the zip-file to the server and create the ticket, and the second is to request
the validation of the zip-file (See SubSection **Validate Validation Request**
above).  To obtain the validation report, the user must obtain the database
report (See Section **Database Report Request with Authentication**) using the
upload ticket number obtained from the validation request.


!!! example "Shell Script - Single File Upload Validation"
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -X POST -H "Authorization: bearer $token" -F "workspaceId=REPLACE_WITH_WORKSPACE_ID" -F "packageName=multiPartFilesValidateOneFile" -F "uploadNotes=" -F "uploadPurpose=validateData" -F "serverName=" -F "file=@/home/tsmith/Downloads/reagents.flow_cytometry.txt" https://immport-upload.niaid.nih.gov:8443/data/upload/type/online
    ```

??? example "Results"
    ``` response
    {
      "uploadTicketNumber" : "testuser_20180523_19550",
      "uploadPurpose" : "validateData",
      "workspaceId" : 999999,
      "status" : "Pending_Validation"
    }
    ```

The first line is a POST to the authentication URL
`https://auth.immport.org/auth/token` with the username and password to get an
authentication token. The fgrep command is used search the response for a token
and then assign the value of the token to an environment variable named
**"token"**.

The second line is a POST on the URL
`https://immport-upload.niaid.nih.gov:8443/data/upload/type/online`
with the -F parameterization. The authentication token (**"token"**) is passed
in the HTTP header as shown.  The following parameters need values: workspaceId,
packageName and file (client-path to single file), while uploadNotes and
serverName can have optional values.  The parameter **packageName MUST HAVE** a
value.  The value of **uploadPurpose** must be what is provided above **as-is**.

The response will be JSON that provides the upload ticket number (to be used in
information endpoints), the upload purpose, the workspace_id, and the current status
of the validation request.

The above shell script or any code starting with #!/bin/bash can be copied to a
.sh file (e.g. validateUploadSingleFile.sh )and executed at the command prompt of a
terminal and the output can be directed to a file. (Please replace the
REPLACE_WITH_USERNAME with your username, and REPLACE_WITH_PASSWORD with your
password)

``` shell
./validateUploadSingleFile.sh > validateUploadSingleFile.json
```

## Mulitple File Upload for Validation Request with Authentication

The following is an example of validation of a multiple files, where several 
-F parameters are used.  Note that **packageName** parameter **MUST HAVE** a
value.  Also, validation is a two endpoint (step) process.  The first step is to
upload the zip-file to the server and create the ticket, and the second is to
request the validation of the zip-file (See SubSection **Validate Validation
Request** above).  To obtain the validation report, the user must obtain the
database report (See Section **Database Report Request with Authentication**)
using the upload ticket number obtained from the validation request.

!!! example "Shell Script - Multiple File Upload Validation"
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -X POST -H "Authorization: bearer $token" -F "workspaceId=REPLACE_WITH_WORKSPACE_ID" -F "packageName=multiPartFilesValidateMultipleFiles" -F "uploadNotes=" -F "uploadPurpose=validateData" -F "serverName=" -F "file=@/home/tsmith/Downloads/test_GE.MA.Affy_study_protocol.txt" -F "file=@/home/tsmith/Downloads/protocols.txt" -F "file=@/home/tsmith/Downloads/cn01adv.txt" -F "file=@/home/tsmith/Downloads/basic_study_design.txt" -F "file=@/home/tsmith/Downloads/MBAA_protocol.txt" https://immport-upload.niaid.nih.gov:8443/data/upload/type/online
    ```

??? example "Results"
    ``` response
    {
      "uploadTicketNumber" : "testuser_20180523_19551",
      "uploadPurpose" : "validateData",
      "workspaceId" : 999999,
      "status" : "Pending_Validation"
    }
    ```

The first line is a POST to the authentication URL
`https://auth.immport.org/auth/token` with the username and password to get an
authentication token. The fgrep command is used search the response for a token
and then assign the value of the token to an environment variable named
**"token"**.

The second line is a POST on the URL
`https://immport-upload.niaid.nih.gov:8443/data/upload/type/online`
with the -F parameterization. The authentication token (**"token"**) is passed
in the HTTP header as shown.  The following parameters need values: workspaceId,
packageName and file (client-path to each of multiple files), while uploadNotes
and serverName can have optional values.  The parameter **packageName MUST
HAVE** a value.  The value of **uploadPurpose** must be what is provided above
**as-is**.

The response will be JSON that provides the upload ticket number (to be used in
information endpoints), the upload purpose, the workspace_id, and the current
status of the validation request.

The above shell script or any code starting with #!/bin/bash can be copied to a
.sh file (e.g. validateUploadMultipleFiles.sh )and executed at the command
prompt of a terminal and the output can be directed to a file. (Please replace
the REPLACE_WITH_USERNAME with your username, and REPLACE_WITH_PASSWORD with
your password)

``` shell
./validateUploadMultipleFiles.sh > validateUploadMultipleFiles.json
```

## Status of Upload Ticket with Authentication

The following is an example of a request for status of an upload ticket number
where an inline parameter (UPLOAD_TICKET_NUMBER) is used.

!!! example "Shell Script - Status of Upload Ticket"
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -H "Authorization: bearer $token" https://immport-upload.niaid.nih.gov:8443/data/upload/registration/testuser_20180523_19544/status
    ```

??? example "Results"
    ``` response
    {
      "uploadTicketNumber" : "testuser_20180523_19544",
      "status" : "Completed"
    }
    ```

The first line is a POST to the authentication URL
`https://auth.immport.org/auth/token` with the username and password to get an
authentication token. The fgrep command is used search the response for a token
and then assign the value of the token to an environment variable named
**"token"**.

The second line is an inline Non-POST URL
`/data/upload/registration/testuser_20180523_19544/status`
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
## Summary Information on Upload Ticket Request with Authentication

The following is an example of a request for summary report status of a
validation using an upload ticket number, where an inline parameter
(UPLOAD_TICKET_NUMBER) is used.

!!! example "Shell Script - Summary Information for Upload Ticket"
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -H "Authorization: bearer $token" https://immport-upload.niaid.nih.gov:8443/data/upload/registration/testuser_20180523_19543/reports/summary
    ```

??? example "Results"
    ``` response
    {
      "summary" : {
        "uploadRegistrationId" : 19543,
        "workspaceName" : "Test Creation Scripts I",
        "fileName" : "Test.Fcm_Derived_Data.Comprehensive.zip",
        "status" : "Completed_Validation",
        "uploadTicketNumber" : "testuser_20180523_19543",
        "dateCreated" : "2018-05-23",
        "createdBy" : "testuser",
        "uploadMethod" : "Secure Web",
        "uploadRegistrationResults" : [ {
          "uploadRegistrationResultId" : 1101351,
          "description" : "server name:client-server",
          "errorMessage" : null,
          "fileName" : "Test.Fcm_Derived_Data.Comprehensive.zip",
          "lineNumber" : null,
          "status" : "Completed_Validation",
          "uploadTicketNumber" : "testuser_20180523_19543",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        } ]
      },
      "uploadTicketNumber" : "testuser_20180523_19543",
      "type" : "summary"
    }
    ```

The following is an example of a request for summary report status of an upload
using an upload ticket number, where an inline parameter (UPLOAD_TICKET_NUMBER)
is used.

!!! example "Shell Script - Summary Report for Upload Ticket"
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -H "Authorization: bearer $token" https://immport-upload.niaid.nih.gov:8443/data/upload/registration/testuser_20180523_19544/reports/summary
    ```

??? example "Results"
    ``` response
    {
      "summary" : {
        "uploadRegistrationId" : 19544,
        "workspaceName" : "Test Creation Scripts I",
        "fileName" : "Test.Fcm_Derived_Data.Comprehensive.zip",
        "status" : "Completed",
        "uploadTicketNumber" : "testuser_20180523_19544",
        "dateCreated" : "2018-05-23",
        "createdBy" : "testuser",
        "uploadMethod" : "Secure Web",
        "uploadRegistrationResults" : [ {
          "uploadRegistrationResultId" : 1101260,
          "description" : "server name:client-server",
          "errorMessage" : null,
          "fileName" : "Test.Fcm_Derived_Data.Comprehensive.zip",
          "lineNumber" : null,
          "status" : "Registered",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101261,
          "description" : null,
          "errorMessage" : null,
          "fileName" : "testuser_20180523_19544___Test.Fcm_Derived_Data.Comprehensive.zip",
          "lineNumber" : null,
          "status" : "Started",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101262,
          "description" : "Template: protocols.txt, Size:748 bytes",
          "errorMessage" : null,
          "fileName" : "protocols.txt",
          "lineNumber" : null,
          "status" : "Parsing",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101263,
          "description" : "Validation Level = Standard",
          "errorMessage" : null,
          "fileName" : "protocols.txt",
          "lineNumber" : null,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101264,
          "description" : "Size:748 bytes",
          "errorMessage" : null,
          "fileName" : "protocols.txt",
          "lineNumber" : 3,
          "status" : "Stored in:file_info",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101265,
          "description" : "Size:48046 bytes",
          "errorMessage" : null,
          "fileName" : "Splenic_B_cell_isolation.pdf",
          "lineNumber" : 4,
          "status" : "Stored in:protocols",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101266,
          "description" : "Size:13743 bytes",
          "errorMessage" : null,
          "fileName" : "Culture_conditions.pdf",
          "lineNumber" : 5,
          "status" : "Stored in:protocols",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101267,
          "description" : "Size:18944 bytes",
          "errorMessage" : null,
          "fileName" : "FlowCytometryProtocol.xls",
          "lineNumber" : 6,
          "status" : "Stored in:protocols",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101268,
          "description" : "Size:30 bytes",
          "errorMessage" : null,
          "fileName" : "example animal study protocol.txt",
          "lineNumber" : 7,
          "status" : "Stored in:protocols",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101269,
          "description" : "Template: protocols.txt, Size:748 bytes",
          "errorMessage" : null,
          "fileName" : "protocols.txt",
          "lineNumber" : null,
          "status" : "Parsed",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101270,
          "description" : "Template: reagents.flow_cytometry.txt, Size:1157 bytes",
          "errorMessage" : null,
          "fileName" : "reagents.flow_cytometry.txt",
          "lineNumber" : null,
          "status" : "Parsing",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101271,
          "description" : "Validation Level = Standard",
          "errorMessage" : null,
          "fileName" : "reagents.flow_cytometry.txt",
          "lineNumber" : null,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101272,
          "description" : "Size:1157 bytes",
          "errorMessage" : null,
          "fileName" : "reagents.flow_cytometry.txt",
          "lineNumber" : 3,
          "status" : "Stored in:file_info",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101273,
          "description" : "Template: reagents.flow_cytometry.txt, Size:1157 bytes",
          "errorMessage" : null,
          "fileName" : "reagents.flow_cytometry.txt",
          "lineNumber" : null,
          "status" : "Parsed",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101274,
          "description" : "Template: reagent_sets.txt, Size:458 bytes",
          "errorMessage" : null,
          "fileName" : "reagent_sets.txt",
          "lineNumber" : null,
          "status" : "Parsing",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101275,
          "description" : "Validation Level = Standard",
          "errorMessage" : null,
          "fileName" : "reagent_sets.txt",
          "lineNumber" : null,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101276,
          "description" : "Size:458 bytes",
          "errorMessage" : null,
          "fileName" : "reagent_sets.txt",
          "lineNumber" : 3,
          "status" : "Stored in:file_info",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101277,
          "description" : "Template: reagent_sets.txt, Size:458 bytes",
          "errorMessage" : null,
          "fileName" : "reagent_sets.txt",
          "lineNumber" : null,
          "status" : "Parsed",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101278,
          "description" : "Template: treatments.txt, Size:420 bytes",
          "errorMessage" : null,
          "fileName" : "treatments.txt",
          "lineNumber" : null,
          "status" : "Parsing",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101279,
          "description" : "Validation Level = Standard",
          "errorMessage" : null,
          "fileName" : "treatments.txt",
          "lineNumber" : null,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101280,
          "description" : "Size:420 bytes",
          "errorMessage" : null,
          "fileName" : "treatments.txt",
          "lineNumber" : 3,
          "status" : "Stored in:file_info",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101281,
          "description" : "Template: treatments.txt, Size:420 bytes",
          "errorMessage" : null,
          "fileName" : "treatments.txt",
          "lineNumber" : null,
          "status" : "Parsed",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101282,
          "description" : "Template: basic_study_design.txt, Size:1877 bytes",
          "errorMessage" : null,
          "fileName" : "basic_study_design.txt",
          "lineNumber" : null,
          "status" : "Parsing",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101283,
          "description" : "Validation Level = Standard",
          "errorMessage" : null,
          "fileName" : "basic_study_design.txt",
          "lineNumber" : null,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101284,
          "description" : "Size:1877 bytes",
          "errorMessage" : null,
          "fileName" : "basic_study_design.txt",
          "lineNumber" : 3,
          "status" : "Stored in:file_info",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101285,
          "description" : "Size:92 bytes",
          "errorMessage" : null,
          "fileName" : "Information_1.txt",
          "lineNumber" : 46,
          "status" : "Stored in:study_file",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101286,
          "description" : "Template: basic_study_design.txt, Size:1877 bytes",
          "errorMessage" : null,
          "fileName" : "basic_study_design.txt",
          "lineNumber" : null,
          "status" : "Parsed",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101287,
          "description" : "Template: subjectsanimal.txt, Size:889 bytes",
          "errorMessage" : null,
          "fileName" : "subjectsAnimal.txt",
          "lineNumber" : null,
          "status" : "Parsing",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101288,
          "description" : "Validation Level = Standard",
          "errorMessage" : null,
          "fileName" : "subjectsAnimal.txt",
          "lineNumber" : null,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101289,
          "description" : "Size:889 bytes",
          "errorMessage" : null,
          "fileName" : "subjectsAnimal.txt",
          "lineNumber" : 3,
          "status" : "Stored in:file_info",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101290,
          "description" : "Template: subjectsanimal.txt, Size:889 bytes",
          "errorMessage" : null,
          "fileName" : "subjectsAnimal.txt",
          "lineNumber" : null,
          "status" : "Parsed",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101291,
          "description" : "Template: biosamples.txt, Size:1547 bytes",
          "errorMessage" : null,
          "fileName" : "bioSamples.txt",
          "lineNumber" : null,
          "status" : "Parsing",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101292,
          "description" : "Validation Level = Standard",
          "errorMessage" : null,
          "fileName" : "bioSamples.txt",
          "lineNumber" : null,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101293,
          "description" : "Size:1547 bytes",
          "errorMessage" : null,
          "fileName" : "bioSamples.txt",
          "lineNumber" : 3,
          "status" : "Stored in:file_info",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101294,
          "description" : "Template: biosamples.txt, Size:1547 bytes",
          "errorMessage" : null,
          "fileName" : "bioSamples.txt",
          "lineNumber" : null,
          "status" : "Parsed",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101295,
          "description" : "Template: experiments.txt, Size:545 bytes",
          "errorMessage" : null,
          "fileName" : "experiments.txt",
          "lineNumber" : null,
          "status" : "Parsing",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101296,
          "description" : "Validation Level = Standard",
          "errorMessage" : null,
          "fileName" : "experiments.txt",
          "lineNumber" : null,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101297,
          "description" : "Size:545 bytes",
          "errorMessage" : null,
          "fileName" : "experiments.txt",
          "lineNumber" : 3,
          "status" : "Stored in:file_info",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101298,
          "description" : "Template: experiments.txt, Size:545 bytes",
          "errorMessage" : null,
          "fileName" : "experiments.txt",
          "lineNumber" : null,
          "status" : "Parsed",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101299,
          "description" : "Template: experimentsamples.flow_cytometry.txt, Size:1038 bytes",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : null,
          "status" : "Parsing",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101300,
          "description" : "Validation Level = Standard",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : null,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101301,
          "description" : "Size:1038 bytes",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 2,
          "status" : "Stored in:file_info",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101302,
          "description" : "The combined status for expsample_id (FlowCyt ES 101806_1) and table expsample has values:  expsample_required (yes), expsample_user_defined_id (FlowCyt ES 101806_1), and expsample_accession ().",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 3,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101303,
          "description" : "The combined status for biosample_id (Splenic_B-cells_untreated) and table biosample has values:  biosample_required (no), biosample_user_defined_id (Splenic_B-cells_untreated), and biosample_accession (BS935311).",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 3,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101304,
          "description" : "The combined status for experiment_id (FlowCyt Expt) and table experiment has values:  experiment_required (no), experiment_user_defined_id (FlowCyt Expt), and experiment_accession (EXP15457).",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 3,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101305,
          "description" : "The parent accession biosample_study_accession (SDY1897) was set using the table biosample and biosample_accession (BS935311).",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 3,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101306,
          "description" : "The parent accession experiment_study_accession (SDY1897) was set using the table experiment and experiment_accession (EXP15457).",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 3,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101307,
          "description" : "The value in experiment_study_accession (SDY1897) is assigned to study_accession.",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 3,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101308,
          "description" : "Size:201530 bytes",
          "errorMessage" : null,
          "fileName" : "Specimen_001_Tube_001.fcs",
          "lineNumber" : 6,
          "status" : "Stored in:file_info",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101309,
          "description" : "Size:10446 bytes",
          "errorMessage" : null,
          "fileName" : "FCM_derived_data.txt",
          "lineNumber" : 6,
          "status" : "Stored in:file_info",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101310,
          "description" : "Size:201631 bytes",
          "errorMessage" : null,
          "fileName" : "CompensationTube_001.fcs",
          "lineNumber" : 6,
          "status" : "Stored in:file_info",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101311,
          "description" : "Size:201631 bytes",
          "errorMessage" : null,
          "fileName" : "CompensationTube_002.fcs",
          "lineNumber" : 6,
          "status" : "Stored in:file_info",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101312,
          "description" : "The combined status for expsample_id (FlowCyt ES 101806_2) and table expsample has values:  expsample_required (yes), expsample_user_defined_id (FlowCyt ES 101806_2), and expsample_accession ().",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 4,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101313,
          "description" : "The combined status for biosample_id (Splenic_B-cells_treated_with_BAFF) and table biosample has values:  biosample_required (no), biosample_user_defined_id (Splenic_B-cells_treated_with_BAFF), and biosample_accession (BS935312).",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 4,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101314,
          "description" : "The combined status for experiment_id (FlowCyt Expt) and table experiment has values:  experiment_required (no), experiment_user_defined_id (FlowCyt Expt), and experiment_accession (EXP15457).",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 4,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101315,
          "description" : "The parent accession biosample_study_accession (SDY1897) was set using the table biosample and biosample_accession (BS935312).",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 4,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101316,
          "description" : "The parent accession experiment_study_accession (SDY1897) was set using the table experiment and experiment_accession (EXP15457).",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 4,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101317,
          "description" : "The value in experiment_study_accession (SDY1897) is assigned to study_accession.",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 4,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101318,
          "description" : "Size:201530 bytes",
          "errorMessage" : null,
          "fileName" : "Specimen_001_Tube_002.fcs",
          "lineNumber" : 6,
          "status" : "Stored in:file_info",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101319,
          "description" : "The combined status for expsample_id (FlowCyt ES 101806_3) and table expsample has values:  expsample_required (yes), expsample_user_defined_id (FlowCyt ES 101806_3), and expsample_accession ().",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 5,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101320,
          "description" : "The combined status for biosample_id (Splenic_B-cells_treated_with_Anti-IgM) and table biosample has values:  biosample_required (no), biosample_user_defined_id (Splenic_B-cells_treated_with_Anti-IgM), and biosample_accession (BS935313).",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 5,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101321,
          "description" : "The combined status for experiment_id (FlowCyt Expt) and table experiment has values:  experiment_required (no), experiment_user_defined_id (FlowCyt Expt), and experiment_accession (EXP15457).",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 5,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101322,
          "description" : "The parent accession biosample_study_accession (SDY1897) was set using the table biosample and biosample_accession (BS935313).",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 5,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101323,
          "description" : "The parent accession experiment_study_accession (SDY1897) was set using the table experiment and experiment_accession (EXP15457).",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 5,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101324,
          "description" : "The value in experiment_study_accession (SDY1897) is assigned to study_accession.",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 5,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101325,
          "description" : "Size:201529 bytes",
          "errorMessage" : null,
          "fileName" : "Specimen_001_Tube_003.fcs",
          "lineNumber" : 6,
          "status" : "Stored in:file_info",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101326,
          "description" : "The combined status for expsample_id (FlowCyt ES 101806_4) and table expsample has values:  expsample_required (yes), expsample_user_defined_id (FlowCyt ES 101806_4), and expsample_accession ().",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 6,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101327,
          "description" : "The combined status for biosample_id (Splenic_B-cells_treated_with_BAFF_and_anti-IgM) and table biosample has values:  biosample_required (no), biosample_user_defined_id (Splenic_B-cells_treated_with_BAFF_and_anti-IgM), and biosample_accession (BS935314).",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 6,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101328,
          "description" : "The combined status for experiment_id (FlowCyt Expt) and table experiment has values:  experiment_required (no), experiment_user_defined_id (FlowCyt Expt), and experiment_accession (EXP15457).",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 6,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101329,
          "description" : "The parent accession biosample_study_accession (SDY1897) was set using the table biosample and biosample_accession (BS935314).",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 6,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101330,
          "description" : "The parent accession experiment_study_accession (SDY1897) was set using the table experiment and experiment_accession (EXP15457).",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 6,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101331,
          "description" : "The value in experiment_study_accession (SDY1897) is assigned to study_accession.",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : 6,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101332,
          "description" : "Size:201529 bytes",
          "errorMessage" : null,
          "fileName" : "Specimen_001_Tube_004.fcs",
          "lineNumber" : 6,
          "status" : "Stored in:file_info",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101333,
          "description" : "Template: experimentsamples.flow_cytometry.txt, Size:1038 bytes",
          "errorMessage" : null,
          "fileName" : "experimentSamples.Flow_Cytometry.txt",
          "lineNumber" : null,
          "status" : "Parsed",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101334,
          "description" : "Template: fcm_derived_data.txt, Size:10446 bytes",
          "errorMessage" : null,
          "fileName" : "FCM_derived_data.txt",
          "lineNumber" : null,
          "status" : "Parsing",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101335,
          "description" : "Validation Level = Standard",
          "errorMessage" : null,
          "fileName" : "FCM_derived_data.txt",
          "lineNumber" : null,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101336,
          "description" : "Size:1149 bytes",
          "errorMessage" : null,
          "fileName" : "FCM_derived_data.workspace.txt",
          "lineNumber" : 75,
          "status" : "Stored in:file_info",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101337,
          "description" : "\"Gating Definition Reported\" field with value \"CD14+, HLA-DRhi CD16+\" has a preferred value \"CD14+, HLADRhi, CD16+\" and the preferred value is assigned to the population_defnition_preferred field",
          "errorMessage" : null,
          "fileName" : "FCM_derived_data.txt",
          "lineNumber" : 4,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101338,
          "description" : "\"Gating Definition Reported\" field with value \"CD14lo, HLA-DR+, CD16+\" has a preferred value \"CD14lo, HLADR+, CD16+\" and the preferred value is assigned to the population_defnition_preferred field",
          "errorMessage" : null,
          "fileName" : "FCM_derived_data.txt",
          "lineNumber" : 5,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101339,
          "description" : "\"Gating Definition Reported\" field with value \"CD25high CD127LO\" has a preferred value \"IL2RAhigh, CD127LO\" and the preferred value is assigned to the population_defnition_preferred field",
          "errorMessage" : null,
          "fileName" : "FCM_derived_data.txt",
          "lineNumber" : 6,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101340,
          "description" : "\"Gating Definition Reported\" field with value \"CD14-CD56+CD3++\" has a preferred value \"CD14-, CD56+, CD3++\" and the preferred value is assigned to the population_defnition_preferred field",
          "errorMessage" : null,
          "fileName" : "FCM_derived_data.txt",
          "lineNumber" : 36,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101341,
          "description" : "\"Gating Definition Reported\" field with value \"CD27++CD38++\" has a preferred value \"CD27++, CD38++\" and the preferred value is assigned to the population_defnition_preferred field",
          "errorMessage" : null,
          "fileName" : "FCM_derived_data.txt",
          "lineNumber" : 37,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101342,
          "description" : "\"Gating Definition Reported\" field with value \"CD3-CD14-CD19+IgD-CD20-CD27+CD38++\" has a preferred value \"CD3-, CD14-, CD19+, IgD-, CD20-, CD27+, CD38++\" and the preferred value is assigned to the population_defnition_preferred field",
          "errorMessage" : null,
          "fileName" : "FCM_derived_data.txt",
          "lineNumber" : 39,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101343,
          "description" : "\"Gating Definition Reported\" field with value \"CD45RA+ Naive\" has a preferred value \"CD45RA+\" and the preferred value is assigned to the population_defnition_preferred field",
          "errorMessage" : null,
          "fileName" : "FCM_derived_data.txt",
          "lineNumber" : 53,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101344,
          "description" : "\"Gating Definition Reported\" field with value \"CD16+ neutrophil\" has a preferred value \"CD16+\" and the preferred value is assigned to the population_defnition_preferred field",
          "errorMessage" : null,
          "fileName" : "FCM_derived_data.txt",
          "lineNumber" : 55,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101345,
          "description" : "\"Gating Definition Reported\" field with value \"CD16+ granulocyte\" has a preferred value \"CD16+\" and the preferred value is assigned to the population_defnition_preferred field",
          "errorMessage" : null,
          "fileName" : "FCM_derived_data.txt",
          "lineNumber" : 56,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101346,
          "description" : "\"Gating Definition Reported\" field with value \"CD16+, CD62L- granulocyte\" has a preferred value \"CD16+, CD62L-\" and the preferred value is assigned to the population_defnition_preferred field",
          "errorMessage" : null,
          "fileName" : "FCM_derived_data.txt",
          "lineNumber" : 57,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101347,
          "description" : "\"Gating Definition Reported\" field with value \"CD14nCD16n_pmo\" has a preferred value \"CD14-, CD16-\" and the preferred value is assigned to the population_defnition_preferred field",
          "errorMessage" : null,
          "fileName" : "FCM_derived_data.txt",
          "lineNumber" : 64,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101348,
          "description" : "\"Gating Definition Reported\" field with value \"CD14pCD16n_pmo\" has a preferred value \"CD14+, CD16-\" and the preferred value is assigned to the population_defnition_preferred field",
          "errorMessage" : null,
          "fileName" : "FCM_derived_data.txt",
          "lineNumber" : 67,
          "status" : "Information",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101349,
          "description" : "Template: fcm_derived_data.txt, Size:10446 bytes",
          "errorMessage" : null,
          "fileName" : "FCM_derived_data.txt",
          "lineNumber" : null,
          "status" : "Parsed",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        }, {
          "uploadRegistrationResultId" : 1101350,
          "description" : null,
          "errorMessage" : null,
          "fileName" : "testuser_20180523_19544___Test.Fcm_Derived_Data.Comprehensive.zip",
          "lineNumber" : null,
          "status" : "Completed",
          "uploadTicketNumber" : "testuser_20180523_19544",
          "dateCreated" : "2018-05-23",
          "createdBy" : "testuser",
          "dateLastUpdated" : "2018-05-23",
          "lastUpdatedBy" : "testuser"
        } ]
      },
      "uploadTicketNumber" : "testuser_20180523_19544",
      "type" : "summary"
    }
    ```

The first line is a POST to the authentication URL
`https://auth.immport.org/auth/token` with the username and password to get an
authentication token. The fgrep command is used search the response for a token
and then assign the value of the token to an environment variable named
**"token"**.

The second line is an inline Non-POST URL
`https://immport-upload.niaid.nih.gov:8443/data/upload/registration/testuser_20180522_19504/reports/summary`
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

The following is an example of a request for the database report for a
validation using an upload ticket number where an inline parameter
(UPLOAD_TICKET_NUMBER) is used.

!!! example "Shell Script - Database Information for Upload Ticket"
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -H "Authorization: bearer $token" https://immport-upload.niaid.nih.gov:8443/data/upload/registration/testuser_20180523_19543/reports/database
    ```

??? example "Results"
    ``` response
    {
      "database" : "The validation report is based on ImmPort workspace (workspace_id = 999999).\nThe validation report was generated on 2018-05-23-14:22:48.\nThe data package file submitted was /home/immport/data/immport-data-upload-server/webupload_drop_zone/testuser_20180523_19543___Test.Fcm_Derived_Data.Comprehensive.zip.\n\nFile Name\tLine Number\tStatus\tError Message\tDescription\nprotocols.txt\t\tParsing\t\tTemplate: protocols.txt, Size:748 bytes\nprotocols.txt\t\tInformation\t\tValidation Level = Standard\nprotocols.txt\t3\tStored in:file_info\t\tSize:748 bytes\nSplenic_B_cell_isolation.pdf\t4\tStored in:protocols\t\tSize:48046 bytes\nCulture_conditions.pdf\t5\tStored in:protocols\t\tSize:13743 bytes\nFlowCytometryProtocol.xls\t6\tStored in:protocols\t\tSize:18944 bytes\nexample animal study protocol.txt\t7\tStored in:protocols\t\tSize:30 bytes\nprotocols.txt\t\tParsed\t\tTemplate: protocols.txt, Size:748 bytes\nreagents.flow_cytometry.txt\t\tParsing\t\tTemplate: reagents.flow_cytometry.txt, Size:1157 bytes\nreagents.flow_cytometry.txt\t\tInformation\t\tValidation Level = Standard\nreagents.flow_cytometry.txt\t3\tStored in:file_info\t\tSize:1157 bytes\nreagents.flow_cytometry.txt\t\tParsed\t\tTemplate: reagents.flow_cytometry.txt, Size:1157 bytes\nreagent_sets.txt\t\tParsing\t\tTemplate: reagent_sets.txt, Size:458 bytes\nreagent_sets.txt\t\tInformation\t\tValidation Level = Standard\nreagent_sets.txt\t3\tStored in:file_info\t\tSize:458 bytes\nreagent_sets.txt\t\tParsed\t\tTemplate: reagent_sets.txt, Size:458 bytes\ntreatments.txt\t\tParsing\t\tTemplate: treatments.txt, Size:420 bytes\ntreatments.txt\t\tInformation\t\tValidation Level = Standard\ntreatments.txt\t3\tStored in:file_info\t\tSize:420 bytes\ntreatments.txt\t\tParsed\t\tTemplate: treatments.txt, Size:420 bytes\nbasic_study_design.txt\t\tParsing\t\tTemplate: basic_study_design.txt, Size:1877 bytes\nbasic_study_design.txt\t\tInformation\t\tValidation Level = Standard\nbasic_study_design.txt\t3\tStored in:file_info\t\tSize:1877 bytes\nInformation_1.txt\t46\tStored in:study_file\t\tSize:92 bytes\nbasic_study_design.txt\t\tParsed\t\tTemplate: basic_study_design.txt, Size:1877 bytes\nsubjectsAnimal.txt\t\tParsing\t\tTemplate: subjectsanimal.txt, Size:889 bytes\nsubjectsAnimal.txt\t\tInformation\t\tValidation Level = Standard\nsubjectsAnimal.txt\t3\tStored in:file_info\t\tSize:889 bytes\nsubjectsAnimal.txt\t\tParsed\t\tTemplate: subjectsanimal.txt, Size:889 bytes\nbioSamples.txt\t\tParsing\t\tTemplate: biosamples.txt, Size:1547 bytes\nbioSamples.txt\t\tInformation\t\tValidation Level = Standard\nbioSamples.txt\t3\tStored in:file_info\t\tSize:1547 bytes\nbioSamples.txt\t\tParsed\t\tTemplate: biosamples.txt, Size:1547 bytes\nexperiments.txt\t\tParsing\t\tTemplate: experiments.txt, Size:545 bytes\nexperiments.txt\t\tInformation\t\tValidation Level = Standard\nexperiments.txt\t3\tStored in:file_info\t\tSize:545 bytes\nexperiments.txt\t\tParsed\t\tTemplate: experiments.txt, Size:545 bytes\nexperimentSamples.Flow_Cytometry.txt\t\tParsing\t\tTemplate: experimentsamples.flow_cytometry.txt, Size:1038 bytes\nexperimentSamples.Flow_Cytometry.txt\t\tInformation\t\tValidation Level = Standard\nexperimentSamples.Flow_Cytometry.txt\t2\tStored in:file_info\t\tSize:1038 bytes\nexperimentSamples.Flow_Cytometry.txt\t3\tInformation\t\tThe combined status for expsample_id (FlowCyt ES 101806_1) and table expsample has values:  expsample_required (yes), expsample_user_defined_id (FlowCyt ES 101806_1), and expsample_accession ().\nexperimentSamples.Flow_Cytometry.txt\t3\tInformation\t\tThe combined status for biosample_id (Splenic_B-cells_untreated) and table biosample has values:  biosample_required (no), biosample_user_defined_id (Splenic_B-cells_untreated), and biosample_accession (BS1000000071).\nexperimentSamples.Flow_Cytometry.txt\t3\tInformation\t\tThe combined status for experiment_id (FlowCyt Expt) and table experiment has values:  experiment_required (no), experiment_user_defined_id (FlowCyt Expt), and experiment_accession (EXP1000000080).\nexperimentSamples.Flow_Cytometry.txt\t3\tInformation\t\tThe parent accession biosample_study_accession (SDY1000000045) was set using the table biosample and biosample_accession (BS1000000071).\nexperimentSamples.Flow_Cytometry.txt\t3\tInformation\t\tThe parent accession experiment_study_accession (SDY1000000045) was set using the table experiment and experiment_accession (EXP1000000080).\nexperimentSamples.Flow_Cytometry.txt\t3\tInformation\t\tThe value in experiment_study_accession (SDY1000000045) is assigned to study_accession.\nSpecimen_001_Tube_001.fcs\t6\tStored in:file_info\t\tSize:201530 bytes\nFCM_derived_data.txt\t6\tStored in:file_info\t\tSize:10446 bytes\nCompensationTube_001.fcs\t6\tStored in:file_info\t\tSize:201631 bytes\nCompensationTube_002.fcs\t6\tStored in:file_info\t\tSize:201631 bytes\nexperimentSamples.Flow_Cytometry.txt\t4\tInformation\t\tThe combined status for expsample_id (FlowCyt ES 101806_2) and table expsample has values:  expsample_required (yes), expsample_user_defined_id (FlowCyt ES 101806_2), and expsample_accession ().\nexperimentSamples.Flow_Cytometry.txt\t4\tInformation\t\tThe combined status for biosample_id (Splenic_B-cells_treated_with_BAFF) and table biosample has values:  biosample_required (no), biosample_user_defined_id (Splenic_B-cells_treated_with_BAFF), and biosample_accession (BS1000000072).\nexperimentSamples.Flow_Cytometry.txt\t4\tInformation\t\tThe combined status for experiment_id (FlowCyt Expt) and table experiment has values:  experiment_required (no), experiment_user_defined_id (FlowCyt Expt), and experiment_accession (EXP1000000080).\nexperimentSamples.Flow_Cytometry.txt\t4\tInformation\t\tThe parent accession biosample_study_accession (SDY1000000045) was set using the table biosample and biosample_accession (BS1000000072).\nexperimentSamples.Flow_Cytometry.txt\t4\tInformation\t\tThe parent accession experiment_study_accession (SDY1000000045) was set using the table experiment and experiment_accession (EXP1000000080).\nexperimentSamples.Flow_Cytometry.txt\t4\tInformation\t\tThe value in experiment_study_accession (SDY1000000045) is assigned to study_accession.\nSpecimen_001_Tube_002.fcs\t6\tStored in:file_info\t\tSize:201530 bytes\nexperimentSamples.Flow_Cytometry.txt\t5\tInformation\t\tThe combined status for expsample_id (FlowCyt ES 101806_3) and table expsample has values:  expsample_required (yes), expsample_user_defined_id (FlowCyt ES 101806_3), and expsample_accession ().\nexperimentSamples.Flow_Cytometry.txt\t5\tInformation\t\tThe combined status for biosample_id (Splenic_B-cells_treated_with_Anti-IgM) and table biosample has values:  biosample_required (no), biosample_user_defined_id (Splenic_B-cells_treated_with_Anti-IgM), and biosample_accession (BS1000000073).\nexperimentSamples.Flow_Cytometry.txt\t5\tInformation\t\tThe combined status for experiment_id (FlowCyt Expt) and table experiment has values:  experiment_required (no), experiment_user_defined_id (FlowCyt Expt), and experiment_accession (EXP1000000080).\nexperimentSamples.Flow_Cytometry.txt\t5\tInformation\t\tThe parent accession biosample_study_accession (SDY1000000045) was set using the table biosample and biosample_accession (BS1000000073).\nexperimentSamples.Flow_Cytometry.txt\t5\tInformation\t\tThe parent accession experiment_study_accession (SDY1000000045) was set using the table experiment and experiment_accession (EXP1000000080).\nexperimentSamples.Flow_Cytometry.txt\t5\tInformation\t\tThe value in experiment_study_accession (SDY1000000045) is assigned to study_accession.\nSpecimen_001_Tube_003.fcs\t6\tStored in:file_info\t\tSize:201529 bytes\nexperimentSamples.Flow_Cytometry.txt\t6\tInformation\t\tThe combined status for expsample_id (FlowCyt ES 101806_4) and table expsample has values:  expsample_required (yes), expsample_user_defined_id (FlowCyt ES 101806_4), and expsample_accession ().\nexperimentSamples.Flow_Cytometry.txt\t6\tInformation\t\tThe combined status for biosample_id (Splenic_B-cells_treated_with_BAFF_and_anti-IgM) and table biosample has values:  biosample_required (no), biosample_user_defined_id (Splenic_B-cells_treated_with_BAFF_and_anti-IgM), and biosample_accession (BS1000000074).\nexperimentSamples.Flow_Cytometry.txt\t6\tInformation\t\tThe combined status for experiment_id (FlowCyt Expt) and table experiment has values:  experiment_required (no), experiment_user_defined_id (FlowCyt Expt), and experiment_accession (EXP1000000080).\nexperimentSamples.Flow_Cytometry.txt\t6\tInformation\t\tThe parent accession biosample_study_accession (SDY1000000045) was set using the table biosample and biosample_accession (BS1000000074).\nexperimentSamples.Flow_Cytometry.txt\t6\tInformation\t\tThe parent accession experiment_study_accession (SDY1000000045) was set using the table experiment and experiment_accession (EXP1000000080).\nexperimentSamples.Flow_Cytometry.txt\t6\tInformation\t\tThe value in experiment_study_accession (SDY1000000045) is assigned to study_accession.\nSpecimen_001_Tube_004.fcs\t6\tStored in:file_info\t\tSize:201529 bytes\nexperimentSamples.Flow_Cytometry.txt\t\tParsed\t\tTemplate: experimentsamples.flow_cytometry.txt, Size:1038 bytes\nFCM_derived_data.txt\t\tParsing\t\tTemplate: fcm_derived_data.txt, Size:10446 bytes\nFCM_derived_data.txt\t\tInformation\t\tValidation Level = Standard\nFCM_derived_data.workspace.txt\t75\tStored in:file_info\t\tSize:1149 bytes\nFCM_derived_data.txt\t4\tInformation\t\t\"Gating Definition Reported\" field with value \"CD14+, HLA-DRhi CD16+\" has a preferred value \"CD14+, HLADRhi, CD16+\" and the preferred value is assigned to the population_defnition_preferred field\nFCM_derived_data.txt\t5\tInformation\t\t\"Gating Definition Reported\" field with value \"CD14lo, HLA-DR+, CD16+\" has a preferred value \"CD14lo, HLADR+, CD16+\" and the preferred value is assigned to the population_defnition_preferred field\nFCM_derived_data.txt\t6\tInformation\t\t\"Gating Definition Reported\" field with value \"CD25high CD127LO\" has a preferred value \"IL2RAhigh, CD127LO\" and the preferred value is assigned to the population_defnition_preferred field\nFCM_derived_data.txt\t36\tInformation\t\t\"Gating Definition Reported\" field with value \"CD14-CD56+CD3++\" has a preferred value \"CD14-, CD56+, CD3++\" and the preferred value is assigned to the population_defnition_preferred field\nFCM_derived_data.txt\t37\tInformation\t\t\"Gating Definition Reported\" field with value \"CD27++CD38++\" has a preferred value \"CD27++, CD38++\" and the preferred value is assigned to the population_defnition_preferred field\nFCM_derived_data.txt\t39\tInformation\t\t\"Gating Definition Reported\" field with value \"CD3-CD14-CD19+IgD-CD20-CD27+CD38++\" has a preferred value \"CD3-, CD14-, CD19+, IgD-, CD20-, CD27+, CD38++\" and the preferred value is assigned to the population_defnition_preferred field\nFCM_derived_data.txt\t53\tInformation\t\t\"Gating Definition Reported\" field with value \"CD45RA+ Naive\" has a preferred value \"CD45RA+\" and the preferred value is assigned to the population_defnition_preferred field\nFCM_derived_data.txt\t55\tInformation\t\t\"Gating Definition Reported\" field with value \"CD16+ neutrophil\" has a preferred value \"CD16+\" and the preferred value is assigned to the population_defnition_preferred field\nFCM_derived_data.txt\t56\tInformation\t\t\"Gating Definition Reported\" field with value \"CD16+ granulocyte\" has a preferred value \"CD16+\" and the preferred value is assigned to the population_defnition_preferred field\nFCM_derived_data.txt\t57\tInformation\t\t\"Gating Definition Reported\" field with value \"CD16+, CD62L- granulocyte\" has a preferred value \"CD16+, CD62L-\" and the preferred value is assigned to the population_defnition_preferred field\nFCM_derived_data.txt\t64\tInformation\t\t\"Gating Definition Reported\" field with value \"CD14nCD16n_pmo\" has a preferred value \"CD14-, CD16-\" and the preferred value is assigned to the population_defnition_preferred field\nFCM_derived_data.txt\t67\tInformation\t\t\"Gating Definition Reported\" field with value \"CD14pCD16n_pmo\" has a preferred value \"CD14+, CD16-\" and the preferred value is assigned to the population_defnition_preferred field\nFCM_derived_data.txt\t\tParsed\t\tTemplate: fcm_derived_data.txt, Size:10446 bytes\nnobody_20180523_1000000001___testuser_20180523_19543___Test.Fcm_Derived_Data.Comprehensive.zip\t\tCompleted\t\t\n",
      "uploadTicketNumber" : "testuser_20180523_19543",
      "type" : "database"
    }
```

The following is an example of a request for the database report for an upload
using an upload ticket number where an inline parameter (UPLOAD_TICKET_NUMBER)
is used.

!!! example "Shell Script - Database Information for Upload Ticket"
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -H "Authorization: bearer $token" https://immport-upload.niaid.nih.gov:8443/data/upload/registration/testuser_20180523_19544/reports/database
    ```
??? example "Results"
    ``` response
    {
      "database" : "EXPERIMENT DATA UPLOAD REPORT\r\n=============================\r\n\r\nREPORT DATE:                 23-MAY-2018 09:50:02\r\nWORKSPACE_ID:                999999 NAME Test Creation Scripts I\r\nSUBMISSION TICKET NUMBER:    testuser_20180523_19544\r\nSUBMITTER:                   user, test s\r\nSUBMITTER USERNAME:          testuser\r\nSUBMISSION DATE/TIME:        23-MAY-2018 01:45:45 PM\r\nUPLOAD PACKAGE ZIP FILENAME: Test.Fcm_Derived_Data.Comprehensive.zip\r\nUPLOAD PACKAGE ZIP FILESIZE: 902979\r\nUPLOAD METHOD:               Secure Web\r\n\r\n\r\n\r\nFILENAME: experiments.txt    Total records: 1\r\n-------------------------------------------------------------\r\nUSER_DEFINED_ID\tEXPERIMENT_ACCESSION\tNAME\tMEASUREMENT_TECHNIQUE\tDESCRIPTION\r\nFlowCyt Expt\tEXP15457\tAnnexin+6 color staining 10/18/06\tFlow Cytometry\tComparison of survival and differentiati\r\n\r\n\r\nFILENAME: experimentSamples.Flow_Cytometry.txt    Total records: 4\r\n-------------------------------------------------------------\r\nUSER_DEFINED_ID\tEXPSAMPLE_ACCESSION\tNAME\tRESULT_SCHEMA\tUSER_DEFINED_ID:EXPERIMENT_ACCESSION\r\nFlowCyt ES 101806_1\tES1089595\t-\tFCM\tFlowCyt Expt:EXP15457\r\nFlowCyt ES 101806_2\tES1089596\t-\tFCM\tFlowCyt Expt:EXP15457\r\nFlowCyt ES 101806_3\tES1089597\t-\tFCM\tFlowCyt Expt:EXP15457\r\nFlowCyt ES 101806_4\tES1089598\t-\tFCM\tFlowCyt Expt:EXP15457\r\n\r\n\r\nFILENAME: bioSamples.txt    Total records: 5\r\n-------------------------------------------------------------\r\nUSER_DEFINED_ID\tBIOSAMPLE_ACCESSION\tNAME\tDESCRIPTION\tTYPE\tSUBTYPE\r\nSplenic_B-cells\tBS935310\tSplenic B-cells\tB cells from spleen of C57BL/6 WT mice\tRed Blood Cell\tB cells\r\nSplenic_B-cells_untreated\tBS935311\tSplenic_B-cells_untreated\tB cells cultured in media alone for 48hr\tRed Blood Cell\tB cells\r\nSplenic_B-cells_treated_with_BAFF\tBS935312\tSplenic_B-cells_treated_with_BAFF\tB cells cultured in media + BAFF for 48h\tRed Blood Cell\tB cells\r\nSplenic_B-cells_treated_with_Anti-IgM\tBS935313\tSplenic_B-cells_treated_with_Anti-IgM\tB cells cultured in media + anti-IgM for\tRed Blood Cell\tB cells\r\nSplenic_B-cells_treated_with_BAFF_and_anti-IgM\tBS935314\tSplenic_B-cells_treated_with_BAFF_and_anti-IgM\tB cells cultured in media + BAFF + anti-\tRed Blood Cell\tB cells\r\n\r\n\r\nFILENAME: subjectsAnimal.txt    Total records: 4\r\n-------------------------------------------------------------\r\nUSER_DEFINED_ID\tSUBJECT_ACCESSION\tDESCRIPTION\tGENDER\tSPECIES\r\ncontrol 1\tSUB182413\t-\tFemale\tMus musculus\r\nvaccinated 1\tSUB182414\t-\tMale\tMus musculus\r\ncontrol 2\tSUB182415\t-\tFemale\tMus musculus\r\nvaccinated 2\tSUB182416\t-\tMale\tMus musculus\r\n\r\n\r\nFILENAME: protocols.txt    Total records: 4\r\n-------------------------------------------------------------\r\nUSER_DEFINED_ID\tPROTOCOL_ACCESSION\tFILE_NAME\tPATH\r\nFlowCyt Protocol\tPTL10549\tFlowCytometryProtocol.xls\tworkspace/999999/protocol/FlowCytometryProtocol.PTL10549.xls\r\nexample animal study protocol\tPTL10550\texample animal study protocol.txt\tworkspace/999999/protocol/example animal study protocol.PTL10550.txt\r\nFlowCyt Splenic B cell isolation\tPTL10547\tSplenic_B_cell_isolation.pdf\tworkspace/999999/protocol/Splenic_B_cell_isolation.PTL10547.pdf\r\nFlowCyt Culture conditions\tPTL10548\tCulture_conditions.pdf\tworkspace/999999/protocol/Culture_conditions.PTL10548.pdf\r\n\r\n\r\nFILENAME: basic_study_design.txt    Total records: 1\r\n-------------------------------------------------------------\r\nSTUDY_FILE_ACCESSION\tFILE_NAME\tPATH\r\nSFL20719\tInformation_1.txt\tworkspace/999999/study/SDY1897/study_file/Information_1.txt\r\n\r\n\r\nFILENAME: --None--    Total records: 0\r\n-------------------------------------------------------------\r\nSCHEMATIC_ACCESSION\tFILE_NAME\tPATH\r\n\r\n\r\nFILENAME: reagents.flow_cytometry.txt\r\n    Total Reagent records:           8\r\n    Total Reagent records (Non-Set): 7\r\n    Total Reagent records (Set)    : 1\r\n    Reagent Set information detail : 1 Set(s) containing 7 items\r\n    Total Analyte records created  : 7\r\n-------------------------------------------------------------\r\nUSER_DEFINED_ID\tREAGENT_ACCESSION\tIS_SET\tname\r\nFlowCyt Annexin V FITC\tESR20959\tN\tAnnexin V\r\nFlowCyt anti CD24 PE\tESR20960\tN\tanti-CD24 antibody\r\nFlowCyt anti IgD bio SA PerCP\tESR20961\tN\tanti-IgD antibody\r\nFlowCyt anti AA4.1 APC\tESR20962\tN\tanti-AA4.1 antibody\r\nFlowCyt anti CD23 PE Cy7\tESR20963\tN\tanti-CD23 antibody\r\nFlowCyt anti CD23 PE CP\tESR20964\tN\tanti-CD19 antibody\r\nFlowCyt anti CD21 Pac blue\tESR20965\tN\tanti-CD21 antibody\r\nFlowCyt Self-made Staining cocktail\tESR20966\tY\thome made reagent\r\n\r\n\r\nLIST OF FILENAME(S) IN PACKAGE      Total Files: 22\r\n-------------------------------------------------------------\r\nFILE_STATUS\tFILE_SIZE (BYTES)\tFILE_NAME\tPATH\r\nParsed\t10446\tFCM_derived_data.txt\tworkspace/999999/file_info/template/FCM_derived_data.636567.txt\r\nParsed\t1877\tbasic_study_design.txt\tworkspace/999999/file_info/template/basic_study_design.636561.txt\r\nParsed\t1547\tbioSamples.txt\tworkspace/999999/file_info/template/bioSamples.636563.txt\r\nParsed\t1038\texperimentSamples.Flow_Cytometry.txt\tworkspace/999999/file_info/template/experimentSamples.Flow_Cytometry.636565.txt\r\nParsed\t545\texperiments.txt\tworkspace/999999/file_info/template/experiments.636564.txt\r\nParsed\t748\tprotocols.txt\tworkspace/999999/file_info/template/protocols.636557.txt\r\nParsed\t458\treagent_sets.txt\tworkspace/999999/file_info/template/reagent_sets.636559.txt\r\nParsed\t1157\treagents.flow_cytometry.txt\tworkspace/999999/file_info/template/reagents.flow_cytometry.636558.txt\r\nParsed\t889\tsubjectsAnimal.txt\tworkspace/999999/file_info/template/subjectsAnimal.636562.txt\r\nParsed\t420\ttreatments.txt\tworkspace/999999/file_info/template/treatments.636560.txt\r\nStored in:file_info\t201631\tCompensationTube_001.fcs\tworkspace/999999/study/SDY1897/file_info/60/8/CompensationTube_001.636568.fcs\r\nStored in:file_info\t201631\tCompensationTube_002.fcs\tworkspace/999999/study/SDY1897/file_info/60/9/CompensationTube_002.636569.fcs\r\nStored in:file_info\t1149\tFCM_derived_data.workspace.txt\tworkspace/999999/study/SDY1897/file_info/70/3/FCM_derived_data.workspace.636573.txt\r\nStored in:file_info\t201530\tSpecimen_001_Tube_001.fcs\tworkspace/999999/study/SDY1897/file_info/60/6/Specimen_001_Tube_001.636566.fcs\r\nStored in:file_info\t201530\tSpecimen_001_Tube_002.fcs\tworkspace/999999/study/SDY1897/file_info/70/0/Specimen_001_Tube_002.636570.fcs\r\nStored in:file_info\t201529\tSpecimen_001_Tube_003.fcs\tworkspace/999999/study/SDY1897/file_info/70/1/Specimen_001_Tube_003.636571.fcs\r\nStored in:file_info\t201529\tSpecimen_001_Tube_004.fcs\tworkspace/999999/study/SDY1897/file_info/70/2/Specimen_001_Tube_004.636572.fcs\r\nStored in:protocols\t0\tCulture_conditions.pdf\t-\r\nStored in:protocols\t0\tFlowCytometryProtocol.xls\t-\r\nStored in:protocols\t0\tSplenic_B_cell_isolation.pdf\t-\r\nStored in:protocols\t0\texample animal study protocol.txt\t-\r\nStored in:study_file\t0\tInformation_1.txt\t-\r\n\r\nCount Report (uploadTicketNumber = testuser_20180523_19544):\r\n\r\nupload_registration = 1\r\nupload_registration_result = 91\r\n\r\nWorkspace_2_* Counts\r\nworkspace_2_assessment_panel = 0\r\nworkspace_2_biosample = 5\r\nworkspace_2_control_sample = 0\r\nworkspace_2_experiment = 1\r\nworkspace_2_expsample = 4\r\nworkspace_2_file_info = 17\r\nworkspace_2_lab_test_panel = 0\r\nworkspace_2_protocol = 4\r\nworkspace_2_reagent = 8\r\nworkspace_2_standard_curve = 0\r\nworkspace_2_study = 1\r\nworkspace_2_subject = 4\r\nworkspace_2_treatment = 4\r\n\r\nNon-Study Table Counts\r\nprotocol = 4\r\nreagent = 8\r\nreagent_set_2_reagent = 7\r\ntreatment = 4\r\n\r\nStudy Table Counts\r\nstudy = 1\r\nstudy_2_panel = 8\r\nstudy_2_protocol = 1\r\ncontract_grant_2_study = 0\r\narm_or_cohort = 2\r\ninclusion_exclusion = 2\r\nperiod = 1\r\nplanned_visit = 1\r\nstudy_file = 1\r\nstudy_image = 0\r\nstudy_link = 1\r\nstudy_personnel = 1\r\nstudy_pubmed = 1\r\nadverse_event = 0\r\nassessment_panel = 0\r\nassessment_2_file_info = 0\r\nassessment_component = 0\r\nintervention = 0\r\nlab_test_panel = 0\r\nlab_test_panel_2_protocol = 0\r\nlab_test = 0\r\n\r\nStudy Meta-Data Table Counts\r\nsubject = 4\r\narm_2_subject = 4\r\nbiosample = 5\r\nbiosample_2_treatment = 1\r\nexperiment = 1\r\nexperiment_2_protocol = 3\r\nfile_info = 17\r\nexpsample = 4\r\nexpsample_mbaa_detail = 0\r\nexpsample_public_repository = 0\r\nimmune_exposure = 0\r\nexpsample_2_biosample = 4\r\nexpsample_2_file_info = 14\r\nexpsample_2_reagent = 32\r\nexpsample_2_treatment = 4\r\ncontrol_sample = 0\r\ncontrol_sample_2_file_info = 0\r\nstandard_curve = 0\r\nstandard_curve_2_file_info = 0\r\nfcs_header = 4\r\nfcs_header_marker = 40\r\nfcs_analyzed_result_marker = 383\r\n\r\nResult Table Counts\r\nmbaa_result = 0\r\nfcs_analyzed_result = 73\r\nelisa_result = 0\r\nelispot_result = 0\r\nhai_result = 0\r\nhla_typing_result = 0\r\nkir_typing_result = 0\r\nneut_ab_titer_result = 0\r\npcr_result = 0\r\nrna_seq_result = 0\r\n\r\nOther Non-Upload Table Counts\r\nplanned_visit_2_arm = 0\r\nprotocol_deviation = 0\r\nfcs_header_marker_2_reagent = 0\r\nreference_range = 0\r\nreported_early_termination = 0\r\nstudy_categorization = 0\r\nstudy_data_release = 0\r\nstudy_glossary = 0\r\nsubject_measure_definition = 0\r\nsubject_measure_result = 0\r\n",
      "uploadTicketNumber" : "testuser_20180523_19544",
      "type" : "database"
    }
    ```

The first line is a POST to the authentication URL
`https://auth.immport.org/auth/token` with the username and password to get an
authentication token. The fgrep command is used search the response for a token
and then assign the value of the token to an environment variable named
**"token"**.

The second line is an inline Non-POST URL
`https://immport-upload.niaid.nih.gov:8443/data/upload/registration/testuser_20180522_19504/reports/database`
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

    curl -k -H "Authorization: bearer $token" https://immport-upload.niaid.nih.gov:8443/workspaces
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
`https://immport-upload.niaid.nih.gov:8443/workspaces`
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
