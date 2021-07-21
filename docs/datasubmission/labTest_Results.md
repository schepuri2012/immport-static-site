# Template: **labtest_results**

| Name | Value |
| --- | --- |
| Template Type | single |
| Schema Version | 3.33 |
| Standard File Name | labTest_Results.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Biosample ID | biosample_id | The biosample identifier must be stored in ImmPort or in the biosamples.txt template. A single biosample identifier is expected. | Please enter either a biological sample user defined ID or ImmPort accession. A single biological sample may be linked to an experiment sample. |
| Lab Test Panel ID | lab_test_panel_id | The lab test panel identifier must be stored in ImmPort or in the labTestPanels.txt template. The lab test panel serves as the parent entity to bind lab test results of a similar type together. | Please enter either a lab test panel user defined ID or ImmPort accession. |
| Name Reported | name_reported | The lab test name describes lab test. Please select a unit from the list provided if the name matches your name or enter a name if there is not an appropriate one provided. This name is visible when the panel is shared. | Please select a unit from the list provided if the name matches your name or enter a name if there is not an appropriate one provided. |
| Result Unit Reported | result_unit_reported | The lab test result unit describes the unit for the lab test value. | The lab test result unit describes the unit for the lab test value. |
| Result Value Reported | result_value_reported | The lab test result captures the assayed value for a sample and can include letters, numbers and greater than or less than symbols. | The lab test result captures the assayed value. |
| User Defined ID | user_defined_id | The lab test user defined ID is an identifier chosen by the data provider to refer the lab test. The user defined ID is not shared. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| user_defined_id | USER_DEFINED_ID | lab_test_accession | LT | lab_test_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| user_defined_id | PRIMARY | lab_test | getAvailableUserDefinedIdsMap | lab_test_accession | LT | lab_test_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| biosample_id | yes | - | - | - | - | - | - | - | - | - | 
| lab_test_panel_id | yes | - | - | - | - | - | - | - | - | - | 
| name_reported | yes | - | - | lk_lab_test_name | name_preferred | - | - | - | - | - | 
| result_unit_reported | yes | - | - | lk_unit_of_measure | result_unit_preferred | - | - | - | - | - | 
| result_value_preferred | - | - | - | - | - | - | - | - | float | - | 
| result_value_reported | yes | - | - | - | - | - | - | - | - | - | 
| user_defined_id | yes | - | - | - | - | - | - | - | - | - | 

### Foreign Key Information
FOREIGN KEY TYPE:	user-defined-id	Input column is a User Defined ID and the Output column is the Accession associated with User Defined ID in the given table if the input is a user defined ID

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | biosample_id | biosample_accession | biosample | getAvailableUserDefinedIdsMap | 

FOREIGN KEY TYPE:	accession	Input column is an Accession and the Output column is the Accession in the given table if the input is defined and an accession

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | biosample_id | biosample_accession | biosample | getAvailableAccsToParentMap | 

FOREIGN KEY TYPE:	accession-to-accession	Input column is an Accession and Output column is the parent Accession associated with the Accession in given table if the input column is defined and an accession

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | biosample_accession | biosample_study_accession | biosample | getAvailableAccsToParentMap | 

### Upload Table Information

Table: lab_test    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| biosample_accession | varchar | 15 | - | - | - | - | - | 
| lab_test_accession | varchar | 15 | - | - | - | - | - | 
| lab_test_panel_accession | varchar | 15 | - | - | - | - | - | 
| name_preferred | varchar | 40 | - | - | - | - | - | 
| name_reported | varchar | 125 | yes | - | - | - | - | 
| result_unit_preferred | varchar | 40 | - | - | - | - | - | 
| result_unit_reported | varchar | 40 | yes | - | - | - | - | 
| result_value_preferred | float | - | - | - | - | - | - | 
| result_value_reported | varchar | 250 | yes | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PostRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | values-equal | - | ['The study_accession for the biological sample is not same as for the lab test panel', 'lab_test_panel_study_accession', 'biosample_study_accession'] | 


### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| convert-to-float | - | [result_value_reported] | [result_value_preferred] | - | - | - | 


### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [lab_test_panel_study_accession] | [] | - | - | - | 


### Preferred Vocabularies

#### Column: name_reported Table: lk_lab_test_name

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | name_reported | name_preferred | name_preferred | 

#### Column: result_unit_reported Table: lk_unit_of_measure

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | result_unit_reported | result_unit_preferred | unit_of_measure_preferred | 


### Preferred Vocabulary Tables

#### lk_lab_test_name

| lk_lab_test_name | lk_lab_test_name | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name_preferred | description | link | id | 
|  | DATABASE COLUMNS | name | description | link | cdisc_lab_test_code | 

#### lk_unit_of_measure

| lk_unit_of_measure | lk_unit_of_measure | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | unit_of_measure_preferred | description | link | 
|  | DATABASE COLUMNS | name | description | link | 


