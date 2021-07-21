### Overview

The ImmPort File Download Tool is a ZIP package which contains two directories:

* bin
* aspera

The *bin* directory contains a bash shell script downloadImmportData.sh,
referred to as the File Download Tool is
designed to automate the authentication, authorization and downloading of files
from the <a href="https://browser.immport.org" target="_blank">
ImmPort Data Browser</a> web site. Details on how to use the
downloadImmPortData.sh tool are are available below.

In addition a Python file
immport_download.py file is included to demonstrate how you can use Python
to automate downloading files and using the Download and Query API.

The *aspera* directory contains software made available from [Aspera](http://asperasoft.com/). Aspera has developed software to transfer large files
at high rates of speeds, faster than normal FTP, and is used by many
scientific sites to support downloading of files.

### Download Tool

The File Download Tool distribution can be obtained from [HERE](https://downloads.immport.org/data/download/tool/immport-data-download-tool.zip). Then unzip the
contents of the zip package and cd to the immport-data-download-tool directory.

If you execute the bin/downloadImmPortData.sh script without any parameters
it will display useful information on the parameters available and other
options. (check the Response tab)

``` shell
unzip immport-data-download-tool.zip
cd immport-data-download-tool
./bin/downloadImmportData.sh
```
??? example "Download Tool Help"
    ```
    usage: downloadImmportData.sh username password file | --manifest-file=filename [ --verbose | --debug ]
           downloadImmportData.sh --clean

    where

      username = ImmPort username
      password = ImmPort password
      file     = Name of file or directory to be downloaded (e.g. /ALLSTUDIES/ALLSTUDIES-DR22_table_count.txt). If this parameter is not specified, then the --manifest-file option must be specified.
    
      --manifest-file=filename = A manifest file containing the list of files and directories to be downloaded. The filename can be either a text file or a JSON file.  If it is a text file, it must contain one file or directory name per line.  If it is a JSON file, it must have a .json file extension AND conform to the output of the ImmPort Shared Data Query API.  If this option is not specified, then parameter file must be specified.

      --verbose = run in verbose mode
      --debug   = run in debug mode (for troubleshooting purposes)
      --clean   = clean output, error, and log files
      --version = version of immport-data-download-tool
    ```

### Examples

####  Download a Result File
```shell
./bin/downloadImmportData.sh "REPLACE_WITH_USERNAME" "REPLACE_WITH_PASSWORD" "/SDY1/ResultFiles/Flow_cytometry_result/02054141.001.52628.fcs"
```
??? example "Review Download Result"
    ```
    USER> ls -lt SDY1/ResultFiles/Flow_cytometry_result
    total 240
    -rw-r--r-- 1 USER USER 242048 Apr 20  2017 02054141.001.52628.fcs

    USER> ls -lt log
    total 64
    -rw-rw---- 2 USER USER 31303 Jun 14 15:13 aspera-scp-transfer.0.log
    -rw-rw---- 2 USER USER 31303 Jun 14 15:13 aspera-scp-transfer.log

    ```


#### Download Multiple Files using a Manifest File

Manifest File
```
SDY1/ResultFiles/Flow_cytometry_result/02054141.001.52628.fcs
SDY1/ResultFiles/Flow_cytometry_result/02054142.001.52644.fcs
SDY1/ResultFiles/Flow_cytometry_result/02054151.001.52646.fcs 
```

``` shell
./bin/downloadImmportData.sh "REPLACE_WITH_USERNAME" "REPLACE_WITH_PASSWORD" --manifest-file=manifest.txt
```

#### Create JSON Manifest File - Download Files
For this example, we will create a Shell script to run multiple commands. The first 2 commands execute a query against the filePath endpoint to create a manifest file in JSON format. This manifest file is then used a input to the dowload tool.

``` shell
#!/bin/bash

#
# Get an ImmPort token to access the ImmPort Shared Data Query API
#
export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1 | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

#
# Create a JSON file containing the output of the ImmPort Shared Data Query API
#
curl -k -H "Authorization: bearer $token" "https://api.immport.org/data/query/result/filePath?studyAccession=SDY208" > manifest.json

#
# Call the Download Tool and pass the JSON file created above as the manifest file
#
./bin/downloadImmportData.sh "REPLACE_WITH_USERNAME" "REPLACE_WITH_PASSWORD" --manifest-file=manifest.json
```

The file contents of the JSON file created by the filePath API is quite verbose. The downloadImmPortData.sh knows how to parse this JSON output and removes duplicate file names before downloading the files. Below is an example of a stripped down version of a JSON manifest file, duplicate file names removed automatically.
??? example "Sample Stripped Down JSON Manifest"
    ```
    [
      {
        "filePath" : "/SDY208/ResultFiles/Virus_neutralization_result/Virus_Neutralization_Results.388647.txt"
      },
      {
        "filePath" : "/SDY208/ResultFiles/Virus_neutralization_result/Virus_Neutralization_Results.388647.txt"
      },
      {
        "filePath" : "/SDY208/ResultFiles/Virus_neutralization_result/Virus_Neutralization_Results.388647.txt"
      },
      {
        "filePath" : "/SDY208/ResultFiles/Virus_neutralization_result/Virus_Neutralization_Results.388647.txt"
      },
      {
        "filePath" : "/SDY208/ResultFiles/Image_Histology_result/DK11-M-Histo.388650.pdf"
      },
      {
        "filePath" : "/SDY208/ResultFiles/Image_Histology_result/DK11-M-Histo.388650.pdf"
      },
      {
        "filePath" : "/SDY208/ResultFiles/Image_Histology_result/DK11-M-Histo.388650.pdf"
      },
      {
        "filePath" : "/SDY208/ResultFiles/Image_Histology_result/DK11-M-Histo.388650.pdf"
      }
    ]
    ```