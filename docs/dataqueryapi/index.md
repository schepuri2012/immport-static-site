The Data Query API provides programmatic access to the ImmPort Shared Data. 
The types of endpoints can be grouped into several general categories:

* Assay Result Data
* Controlled Vocabulary or Lookup Tables
* Study Metadata (Used by UI)
* Download Files

Many of the endpoints are password protected and require sending an ImmPort access token to use the endpoint, but several are open and do not require an ImmPort access token. Some of the endpoints support multiple filter critera's for narrowing down the returned data to specific information of interest. Most of the endpoints return data in JSON format, some also support returing the results in tab-separated text format. How to obtain an access tokem, filter criterias and file format topics will be discussed in more detail in the appropriate section.

The Python Examples under the Data Query API heading, includes several examples of how to use the API endpoints.

## Authentication
When an endpoint requires an access token, one can be obtained by sending a request to the authentication endpoint and including the ImmPort username and password.
!!! note ""
    https://auth.immport.org/auth/token

!!! example "Shell Command"
    ``` shell
    curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD"
    ```
??? example "Results"
    ```
    {
    "status" : 200,
    "token" : "Example-OiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2MjMzNTE5NDMsInVzZXJfbmFtZSI6ImNhbXBqbyIsImF1dGhvcml0aWVzIjpbIlJPTEVfVVNFUiIsIlJPTEVfQ1VSQVRJT05fVVNFUiIsIlJPTEVfQURNSU4iLCJST0xFX0lNTVBPUlRfREFUQV9NQU5BR0VNRU5UX0FETUlOIiwiUk9MRV9VU0VSX0FETUlOSVNUUkFUSU9OX0FETUlOIiwiUk9MRV9TSEFSSU5HX1VTRVIiLCJST0xFX0RBVEFfQlJPV1NFUl9BRE1JTiJdLCJqdGkiOiI1ZjFkMzQ3Mi03MWU5LTQ0ODUtYjQ2Zi0wM2E4MGY2Mjk4NDUiLCJjbGllbnRfaWQiOiJpbW1wb3J0LWF1dGgtdG9rZW4tY2xpZW50Iiwic2NvcGUiOlsiYnJvd3NlIiwiZG93bmxvYWQiXX0.PC9vinTYFffEMvD3UXrOq2X6DuQF_8I3HpfuzHw2EG-j8c9GufCChgRieLhmqJ8_K9ngLe_sHzvyWN6GOofUPDr5AQOGYDxurhDzWhLD58841uOQYEhbZtVF0FcO84Ybi1ld_Zgj0Rhauv2jjvZJj-vakANOndEQtsIVmMSKLcnJ93Zk8_Mxtt35yxphZOizbYMmbq8tOy40vGF4O8yHLGgJS-SEebD7shiE7DoWFW5urKvyU6szIa0sz_i1oUoBJLtVeb3pW_lpgkQ3xo4-lCBgK2SkEvdq5g-So5cUNKzW619Tcznjs68z88droOX3gqu3oHxO4Z5Do824_2lzeA"
    }
    ```

The token returned is a JWT token. (You can go to the [JWT token URL](http://jwt.calebb.net/) and enter the token returned from the above call. This will display the types of information contained in the token. The token has information about the username, roles, permissions for the user.

The token must be used to initiate a API request within 60 seconds.  After 60 seconds the token will be invalid and the user will need to get a new token. But once the GET endpoint call is initiated then the token will be valid throughout the entire api request call and does not become invalid until the response is returned.
 
## Sample API call using Shell Commands
In the following example, an authentication token is saved as an environment variable (token) and passed to the HTTP header in the curl command to retrieve ELISA results data.

The first line is a POST to the authentication URL `https://auth.immport.org/auth/token`
with the username and password to get an authentication token. The fgrep command
is used search the response for a token and then assign the value of the token
to an environment variable named **"token"**.

The second line is a GET on the URL `https://api.immport.org/data/query/result/elisa` with the filter parameter `studyAccession=SDY2,SDY4`. The authentication token (**"token"**) is passed in the HTTP header as shown.

The response will return ELISA result data that belongs to study accessions SDY2 and SDY4 (Check the Results tab below). The default format of the response is JSON. The response will be an array of the specific result type or file path data. The filter conditions are always combined using the **AND** operator.

The above shell script or any code starting with #!/bin/bash can be copied to a .sh file (e.g. elisadata.sh )and executed at the command prompt of a terminal and the output can be directed to a file. (Please replace the REPLACE_WITH_USERNAME with your username and REPLACE_WITH_PASSWORD with your password.)

``` shell
#!/bin/bash

export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1  | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

curl -k -H "Authorization: bearer $token" "https://api.immport.org/data/query/result/elisa?studyAccession=SDY2,SDY4"

```

??? example "Results"
    ```
    [ {
      "resultId" : 89390,
      "ageEvent" : "Age at enrollment",
      "ageEventSpecify" : null,
      "ageUnit" : "Years",
      "ancestralPopulation" : null,
      "analytePreferred" : null,
      "analyteReported" : "VZVQual",
      "armAccession" : "ARM235",
      "armName" : "Healthy controls",
      "biosampleAccession" : "BS476749",
      "biosampleType" : "Other",
      "biosampleSubtype" : null,
      "clinical" : "Y",
      "comments" : "negative qualitative result",
      "ethnicity" : "Not Hispanic or Latino",
      "experimentAccession" : "EXP8311",
      "expsampleAccession" : "ES474813",
      "gender" : "Male",
      "maxSubjectAge" : 1.00,
      "measurementTechnique" : "ELISA",
      "minSubjectAge" : 1.00,
      "plannedVisitAccession" : "PV1518",
      "race" : "White",
      "raceSpecify" : null,
      "repositoryAccession" : null,
      "repositoryName" : null,
      "species" : "Homo sapiens",
      "strain" : null,
      "studyAccession" : "SDY2",
      "studyTitle" : "Immune Response to Varicella Vaccination in Subjects with Atopic Dermatitis Compared to Nonatopic Controls",
      "studyTimeCollected" : 1.00,
      "studyTimeCollectedUnit" : "Days",
      "subjectAccession" : "SUB106751",
      "subjectPhenotype" : "non atopic dermititis",
      "unitPreferred" : null,
      "unitReported" : "-1: neg 1: pos",
      "valuePreferred" : -1.0,
      "valueReported" : "-1",
      "treatmentAccession" : null,
      "studyTimeT0EventSpecify" : null,
      "studyTimeT0Event" : "Not Specified"
    }, {
      "resultId" : 89391,
      "ageEvent" : "Age at enrollment",
      "ageEventSpecify" : null,
      "ageUnit" : "Years",
      "ancestralPopulation" : null,
      "analytePreferred" : null,
      "analyteReported" : "VZVQual",
      "armAccession" : "ARM235",
      "armName" : "Healthy controls",
      "biosampleAccession" : "BS476750",
      "biosampleType" : "Other",
      "biosampleSubtype" : null,
      "clinical" : "Y",
      "comments" : "negative qualitative result",
      "ethnicity" : "Not Hispanic or Latino",
      "experimentAccession" : "EXP8311",
      "expsampleAccession" : "ES474814",
      "gender" : "Female",
      "maxSubjectAge" : 1.00,
      "measurementTechnique" : "ELISA",
      "minSubjectAge" : 1.00,
      "plannedVisitAccession" : "PV1518",
      "race" : "White",
      "raceSpecify" : null,
      "repositoryAccession" : null,
      "repositoryName" : null,
      "species" : "Homo sapiens",
      "strain" : null,
      "studyAccession" : "SDY2",
      "studyTitle" : "Immune Response to Varicella Vaccination in Subjects with Atopic Dermatitis Compared to Nonatopic Controls",
      "studyTimeCollected" : 1.00,
      "studyTimeCollectedUnit" : "Days",
      "subjectAccession" : "SUB106784",
      "subjectPhenotype" : "non atopic dermititis",
      "unitPreferred" : null,
      "unitReported" : "-1: neg 1: pos",
      "valuePreferred" : -1.0,
      "valueReported" : "-1",
      "treatmentAccession" : null,
      "studyTimeT0EventSpecify" : null,
      "studyTimeT0Event" : "Not Specified"
    },........   
    ```

## Tools for communicating with the ImmPort Data Query API

Many third-party tools can be used for communicating with the API and for
visualizing API calls.
1G
Examples of tools for communicating with the API:

| Tool        | Type     |
| ------------- |-------------|
| [Curl](http://curl.haxx.se/docs/manpage.html) 		| Command line tool |
| [HTTPie](http://httpie.org) 	| Command line tool |
| [Postman REST Client](http://www.getpostman.com/) 														| App for Google Chrome and OS X |
| [DHC REST Client](http://restlet.com/products/dhc/)           | Google Chrome extension |
| [Google Chrome](http://www.google.com/chrome/) 	  | Google Chrome web browser 
