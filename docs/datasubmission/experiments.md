# Template: **experiments**

| Name | Value |
| --- | --- |
| Template Type | single |
| Schema Version | 3.33 |
| Standard File Name | experiments.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Description | description | The experiment description is used to describe details of the experiment not captured in other columns. | The experiment description is used to describe details of the experiment not captured in other columns. |
| Measurement Technique | measurement_technique | The measurement technique describes the assay method. | Choose from a drop down list. |
| Name | name | The experiment name is a display name that is available when the data is shared, but it is not referenced by other data. | The experiment name is an alternate identifier that is visible when the sample is shared. |
| Protocol ID(s) | protocol_ids | Please enter either a protocol user defined ID or ImmPort accession. One or more identifiers can be entered per subject. Separate identifiers by semicolon (;). | Please enter either a protocol user defined ID or ImmPort accession. |
| Study ID | study_id | An experiment may be linked to a single study. | Please enter either a study user defined ID or ImmPort accession for the study in which the experiment occurs. |
| User Defined ID | user_defined_id | The experiment user defined ID is an identifier chosen by the data provider to refer to an experiment. This ID may be referenced by other data records (e.g. experiment sample, control sample, standard curve). The user defined ID is not shared. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| user_defined_id | USER_DEFINED_ID | experiment_accession | EXP | experiment_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| user_defined_id | PRIMARY | experiment | getAvailableUserDefinedIdsMap | experiment_accession | EXP | experiment_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| description | - | - | - | - | - | - | - | - | - | - | 
| measurement_technique | yes | - | lk_exp_measurement_tech | - | - | - | - | - | - | - | 
| name | yes | - | - | - | - | - | - | - | - | - | 
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

Table: experiment    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| description | varchar | 4000 | yes | - | - | - | - | 
| experiment_accession | varchar | 15 | - | - | - | - | - | 
| measurement_technique | varchar | 50 | - | - | - | - | - | 
| name | varchar | 500 | yes | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: experiment_2_protocol    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| experiment_accession | varchar | 15 | - | - | - | - | - | 
| protocol_accession | varchar | 15 | - | - | - | protocol_accessions | yes | 

Table: workspace_2_experiment    Type: workspace

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| experiment_accession | varchar | 15 | - | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-child-to-parent-accession | - | [experiment, accession-to-accession, getAvailableAccsToParentMap, experiment_accession, study_accession] | [] | - | - | - | 


### Controlled Vocabularies
| lk_exp_measurement_tech | lk_exp_measurement_tech | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 

