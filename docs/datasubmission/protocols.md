# Template: **protocols**

| Name | Value |
| --- | --- |
| Template Type | single |
| Schema Version | 3.33 |
| Standard File Name | protocols.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Description | description | The summary is a brief description of the protocol's content. | The protocol summary describes the purpose of the protocol. |
| File Name | file_name | The protocol file name in this column must be an exact spelling match to a file in the ZIP archive that is uploaded. This includes the file extensions which may be hidden depending upon your computer's settings. The file size name limit is 240 characters. | The protocol file name is the document uploaded and linked to the protocol ID. The file name must be an exact spelling match including the file extension. The file size name limit is 240 characters. |
| Name | name | The protocol name is not referenced by other data records. | The protocol name is an alternate identifier that is visible when the protocol is shared. |
| Type | type | The protocol type uses a preferred list of terms to characterize the protocol's content. | The protocol type is chosen from a list of preferred terms. |
| User Defined ID | user_defined_id | The protocol user defined ID is an identifier chosen by the data provider to refer to a protocol document. This ID may be referenced by other data records (e.g. study). The user defined ID is not shared. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| user_defined_id | USER_DEFINED_ID | protocol_accession | PTL | protocol_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| user_defined_id | PRIMARY | protocol | getAvailableUserDefinedIdsMap | protocol_accession | PTL | protocol_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| description | - | - | - | - | - | - | - | - | - | - | 
| file_name | yes | - | - | - | - | - | - | - | - | - | 
| name | yes | - | - | - | - | - | - | - | - | - | 
| type | - | - | lk_protocol_type | - | - | - | - | - | - | - | 
| user_defined_id | yes | - | - | - | - | - | - | - | - | - | 

### Save File Information

| TABLE NAME | FILE NAME COLUMN | PATH COLUMN | 
|  --- | --- | --- |
| protocol | file_name | path | 

### Upload Table Information

Table: protocol    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| description | varchar | 4000 | yes | - | - | - | - | 
| file_name | varchar | 250 | yes | - | - | unique_file_name | - | 
| name | varchar | 250 | yes | - | - | - | - | 
| original_file_name | varchar | 250 | yes | - | - | - | - | 
| path | varchar | 4000 | - | - | - | - | - | 
| protocol_accession | varchar | 15 | - | - | - | - | - | 
| type | varchar | 100 | - | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: workspace_2_protocol    Type: workspace

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| protocol_accession | varchar | 15 | - | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [] | [type] | [Action = set, Value = Not Specified] | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	empty-value	type	-

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | - | [file_name] | [original_file_name] | - | - | - | 


### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| make-file-name-unique | - | [protocol_accession, file_name] | [unique_file_name] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| create-protocol-path-expression | - | [unique_file_name, original_file_name] | [path] | - | - | - | 


### Controlled Vocabularies
| lk_protocol_type | lk_protocol_type | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 

