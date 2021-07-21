# Template: **labtestpanels**

| Name | Value |
| --- | --- |
| Template Type | single |
| Schema Version | 3.33 |
| Standard File Name | labTestPanels.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Name Reported | name_reported | The lab panel name describes a lab test panel. Please select a preferred value from the list provided if the name matches your name or enter a name if there is not an appropriate one provided. This name is visible when the panel is shared. | The lab panel name describes a lab test panel. Please select a preferred value from the list provided if the name matches your name or enter a name if there is not an appropriate one provided. This name is visible when the panel is shared. |
| Protocol ID(s) | protocol_ids | Please enter either a protocol user defined ID or ImmPort accession. One or more identifiers can be entered per subject. Separate identifiers by semicolon (;). | Please enter either a protocol user defined ID or ImmPort accession. |
| Study ID | study_id | A lab test panel may be linked to a single study. | Please enter either a study user defined ID or ImmPort accession for the study in which the lab test panel occurs. |
| User Defined ID | user_defined_id | The lab test panel user defined ID is an identifier chosen by the data provider to refer to lab panel. This ID may be referenced by other data records (e.g. lab test). The user defined ID is not shared. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| user_defined_id | USER_DEFINED_ID | lab_test_panel_accession | LP | lab_test_panel_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| user_defined_id | PRIMARY | lab_test_panel | getAvailableUserDefinedIdsMap | lab_test_panel_accession | LP | lab_test_panel_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| name_reported | yes | - | - | lk_lab_test_panel_name | name_preferred | - | - | - | - | - | 
| protocol_accessions | - | - | - | - | - | - | yes | - | - | - | 
| protocol_ids | yes | - | - | - | - | - | yes | - | - | - | 
| study_id | yes | - | - | - | - | - | - | - | - | - | 
| user_defined_id | yes | - | - | - | - | - | - | - | - | - | 

### Foreign Key Information
FOREIGN KEY TYPE:	user-defined-id	Input column is a User Defined ID and the Output column is the Accession associated with User Defined ID in the given table if the input is a user defined ID

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | protocol_ids | protocol_accessions | protocol | getAvailableUserDefinedIdsMap | 

FOREIGN KEY TYPE:	accession	Input column is an Accession and the Output column is the Accession in the given table if the input is defined and an accession

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | protocol_ids | protocol_accessions | protocol | getAvailableAccsToParentMap | 

### Upload Table Information

Table: lab_test_panel    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| lab_test_panel_accession | varchar | 15 | - | - | - | - | - | 
| name_preferred | varchar | 125 | - | - | - | - | - | 
| name_reported | varchar | 125 | yes | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: lab_test_panel_2_protocol    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| lab_test_panel_accession | varchar | 15 | - | - | - | - | - | 
| protocol_accession | varchar | 15 | - | - | - | protocol_accessions | yes | 

Table: workspace_2_lab_test_panel    Type: workspace

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| lab_test_panel_accession | varchar | 15 | - | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-child-to-parent-accession | - | [lab_test_panel, accession-to-accession, getAvailableAccsToParentMap, lab_test_panel_accession, study_accession] | [] | - | - | - | 


### Preferred Vocabularies

#### Column: name_reported Table: lk_lab_test_panel_name

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | name_reported | name_preferred | name_preferred | 


### Preferred Vocabulary Tables

#### lk_lab_test_panel_name

| lk_lab_test_panel_name | lk_lab_test_panel_name | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name_preferred | description | link | 
|  | DATABASE COLUMNS | name | description | link | 


