If you are familiar with Python, the following functions may be useful when using the ImmPort File Download API. The code below is an example of a small utility package that could be imported into your programs to use when accessing the API. 

In the examples following the Python function definitions block, we will be using these 3 functions to retrieve content using the File Download API.



### Python Helper Functions
!!! example "Python Helper Functions"
    ``` python
    import sys
    import os
    import shutil
    import subprocess
    import requests
    import json
    import platform
    import pandas as pd
    from io import StringIO

    #
    # These Variables are used inside the functions
    # below. Reducing some of parameters that need to
    # passed to each function.
    #
    # For the functions to work, they assume the Aspera directory 
    # included in the Download Tool zip file have been placed
    # in the ../common/aspera directory.
    #
    API_ENDPOINT_BASE_URL = "https://api.immport.org"
    DATA_QUERY_URL = API_ENDPOINT_BASE_URL + "/data/query"
    IMMPORT_TOKEN_URL = "https://auth.immport.org/auth/token"
    ASPERA_BIN_DIR = "../common/aspera/cli/bin"
    ASPERA_TOKEN_URL = API_ENDPOINT_BASE_URL + "/data/download/token"
    ASPERA_PRIVATE_KEY_FILE = "../common/aspera/cli/etc/asperaweb_id_dsa.openssh"
    ASPERA_USERNAME = "databrowser"
    ASPERA_SERVER = "aspera-immport.niaid.nih.gov"


    def request_immport_token(username, password):
        '''Request an ImmPort token

           :param username: ImmPort user name.
           :param password: ImmPort user password.

           return immport_token
        '''
        r = requests.post(IMMPORT_TOKEN_URL,
                      data={'username': username, 'password': password})
        if r.status_code == 200:
            return r.json()['token']
        else:
            return None

    def request_aspera_token(file_path, immport_token):
        '''Request an Aspera token

           param file_path: Path to the file on the ImmPort Databrowswer site.
           param immport_token: Token obtained from ImmPort authentication.
    
           return aspera_token
        '''
        headers = {
            'Authorization': "bearer " + immport_token,
            'Content-Type': "application/json"
        }

        payload = '{ "paths" : [ "' + file_path + '" ] }'
        r = requests.post(ASPERA_TOKEN_URL, headers=headers, data=payload)
        if r.status_code == 200:
            return r.json()['token']
        else:
            return None
    
    def api_file_download(username, password, file_path, output_directory):
        '''Download a file by first checking ImmPort user credentials,
           checking the file_path exists, retrieving an Aspera token, then
           executing the Aspera command line program to retrieve the file.

           :param username: ImmPort username.
           :param password: ImmPort user password.
           :param file_path: Path to the file on the ImmPort DataBrowser site.
           :param output_directory: Location of the file system to place the
                                the downloaded file.

           return: None
        '''
        immport_token = request_immport_token(username, password)
        if immport_token is None:
            print("ERROR: Credentials incorrect for ImmPort, unable to retrieve token")
            return None
        aspera_token = request_aspera_token(file_path, immport_token)
        if aspera_token is None:
            print("ERROR: Unable to obtain Aspera token")
            return None
    
        #
        # Determine the correct executable for the operating system.
        # Currently support Linux 32/64 and Apple/Darwin.
        #
        os_name = platform.system()
        command = ""
        if os_name == "Linux":
            hardware_name = platform.machine()
            if hardware_name == "x86_64":
                command = ASPERA_BIN_DIR + "/linux/ascp"
            else:
                command = ASPERA_BIN_DIR + "/linux32/ascp"
        elif os_name == "Darwin":
            command = ASPERA_BIN_DIR + "/osx/ascp"
        else:
            print("ERROR: Unsupported operatin system: " + os_name)
            return None

        command += " -v -L " + output_directory + " -i " + \
            ASPERA_PRIVATE_KEY_FILE + " -O 33001 -P 33001 -W "

        command += '"' + aspera_token + '" --user ' + ASPERA_USERNAME + ' -p '
        command += ASPERA_SERVER + ":'" + file_path + "' " + output_directory
        subprocess.call(command, shell=True)
        return "Success"
    ```

### Examples
#### Download a Result File
!!! example "Python - Retrieve Result File"
    ``` python
    if os.path.exists("output"):
        shutil.rmtree("output")
    os.mkdir("output")
    api_file_download(USERNAME, PASSWORD, 'SDY1/ResultFiles/Flow_cytometry_result/02054141.001.52628.fcs', "output")
    os.system("ls -lt output")
    ```

??? example "Results"
    ```
    02054141.001.52628.fcs                        100%  236KB             --:--    
    Completed: 236K bytes transferred in 0 seconds
     (3548K bits/sec), in 1 file.
    total 264
    -rw-rw---- 2 user user   9948 Jun 15 08:56 aspera-scp-transfer.0.log
    -rw-rw---- 2 user user   9948 Jun 15 08:56 aspera-scp-transfer.log
    -rw-r--r-- 1 user user 242048 Apr 20  2017 02054141.001.52628.fcs
    ```

#### Download Multiple Files
!!! example "Python - Download Multiple Files"
    ``` python
    if os.path.exists("output"):
        shutil.rmtree("output")
    os.mkdir("output")
    file_paths = [
        'SDY1/ResultFiles/Flow_cytometry_result/02054141.001.52628.fcs',
        'SDY1/ResultFiles/Flow_cytometry_result/02054142.001.52644.fcs',
        'SDY1/ResultFiles/Flow_cytometry_result/02054151.001.52646.fcs' 
    ]
    for file_path in file_paths:
        api_file_download(USERNAME, PASSWORD, file_path, "output")
    os.system("ls -lt output")
    ```

??? example "Results"
    ```
    02054141.001.52628.fcs                          100%  236KB             --:--    
    Completed: 236K bytes transferred in 0 seconds
     (4319K bits/sec), in 1 file.
    02054142.001.52644.fcs                          100% 1487KB             --:--    
    Completed: 1487K bytes transferred in 0 seconds
     (13984K bits/sec), in 1 file.
    02054151.001.52646.fcs                          100%  236KB             --:--    
    Completed: 236K bytes transferred in 0 seconds
     (4637K bits/sec), in 1 file.
    total 2032
    -rw-rw---- 2 user user   29864 Jun 15 09:40 aspera-scp-transfer.0.log
    -rw-rw---- 2 user user   29864 Jun 15 09:40 aspera-scp-transfer.log
    -rw-r--r-- 1 user user 1523228 Apr 20  2017 02054142.001.52644.fcs
    -rw-r--r-- 1 user user  242048 Apr 20  2017 02054151.001.52646.fcs
    -rw-r--r-- 1 user user  242048 Apr 20  2017 02054141.001.52628.fcs   
    ```