All requests to the Batch Updater API require authentication. The Batch Updater API
uses tokens for authentication.

Users can obtain tokens by posting to the ImmPort Authentication URL
`https://auth.immport.org/auth/token` with a username and password.

This can be done by executing the following curl command:

!!! example "Shell Command"
    ``` shell

    curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD"

    ```

??? example "Results"
    ```
    {
      "status" : 200,
      "token" : "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXV............"
    }
    ```
The token returned is a JWT token. (You can go to the [JWT token
URL](http://jwt.calebb.net/) and enter the token got from the above endpoint. This
will give the information that the token contains. The token has information
about the username, roles, permissions for the user.

The token must be used to initiate a API request within 60 secs.  After 60 secs
the token will be invalid and the user will need to get a new token. But once
the GET endpoint is initiated then the token will be valid throughout the entire api
request endpoint and does not become invalid until the response is returned.

## Using the Authentication Token

All API requests require authentication. They must include the authentication
token as an **Authorization: bearer** in the custom HTTP header.

In the following example, an authentication token is saved as an environment
variable (token) and passed to the HTTP header in the curl command to get back
the generated documentation specific to a workspace.

The following is an example of a request to the documentation generation endpoint
with a single parameter (WORKSPACE_ID=REPLACE_WITH_WORKSPACE_ID).

!!! example "Shell Script - Retrieve Templates"
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -H "Authorization: bearer $token" https://immport-upload.niaid.nih.gov:9443/data/batch/updater/documentation/templates
    ```

??? example "Results"
    ```
    templates.zip 
    ```

The first line is a POST to the authentication URL
`https://auth.immport.org/auth/token` with the username and password to get an
authentication token. The fgrep command is used search the response for a token
and then assign the value of the token to an environment variable named
**"token"**.

The second line is a Non-POST endpoint on the URL
`https://immport-upload.niaid.nih.gov:9443/data/batch/updater/documentation/templates/REPLACE_WITH_WORKSPACE_ID`
with the parameter **REPLACE_WITH_WORKSPACE_ID**. The authentication token (**"token"**) is passed
in the HTTP header as shown.

The response will return zip-file containing the template documentation specific
to workspace whose workspace_id = REPLACE_WITH_WORKSPACE_ID.

The above shell script or any code starting with #!/bin/bash can be copied to a
.sh file (e.g. documentationGeneration.sh )and executed at the command prompt of
a terminal and the output can be directed to a file. (Please replace the
REPLACE_WITH_USERNAME with your username and REPLACE_WITH_PASSWORD with your
password.)

``` shell
./documentationGeneration.sh > ImmportBatchUpdaterTemplates.zip
```