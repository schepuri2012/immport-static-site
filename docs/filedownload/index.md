## Prerequiste

Access to all shared ImmPort data via the API or Download tool
requires you to become a registered user, registration is simple and you can
register
[here](https://immport-user-admin.niaid.nih.gov:8443/registrationuser/registration) .
Because access is limited to registered users, the File Download and Data Query
API methods require an authorization token to be used as part of the request.
The File Download Tool hides this complexity, but you need to be aware
of the need to obtain a access token when using the File Download Tool and API's.

## Aspera Software

The ImmPort files are hosted using IBM Aspera software, which was developed using the FASP protocol, which supports very fast file transfer speeds. More information on Aspera is available [here](https://www.ibm.com/products/aspera).  ImmPort software uses The Aspera Command-Line Interface (ASCP) when transfering files to and from Aspera, more information on this tool is available [here](https://www.ibm.com/docs/en/aci/3.9.20). To use the ImmPort API and Download tool, requires the installation of Aspera executables on the users machine. Executables for the Aspera client are included in the download package for the ImmPort Download tool, which will be discussed in the Tool section.

