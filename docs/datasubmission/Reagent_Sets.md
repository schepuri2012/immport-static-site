# Template: **reagent_sets**

| Name | Value |
| --- | --- |
| Template Type | single |
| Schema Version | 3.33 |
| Standard File Name | Reagent_Sets.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Description | description | The assay reagent description provides further details on the nature and purpose of the reagent. | A supplemental description of the assay reagent that expands on its Name and User Defined ID. |
| Name | name | The reagent name is not referenced by other data records. | The reagent name is an alternate ID that is shared. |
| Reagent ID(s) | reagent_ids | The individual reagents are defined in assay specific reagent templates (e.g. flow cytometry, ELISA). The data provider may define a set or panel of reagents used in a single assay (e.g a panel of fluorochrome conjugated monoclonal antibodies). | Provide a list of individual reagents that comprise the reagent set. Separate the individual reagent IDs with a semi-colon. |
| Type | type | The reagent set type indicates the assay type with which the reagent set is used. | Choose from a list of preferred assay types. |
| User Defined ID | user_defined_id | The reagent user defined ID is an identifier chosen by the data provider to refer to an assay reagent. The nature of the assay reagent is assay specific and may be an array, an antibody or a typing kit. This ID may be referenced by other data records (e.g. experiment sample). The user defined ID is not shared. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| user_defined_id | USER_DEFINED_ID | reagent_accession | ESR | reagent_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| user_defined_id | PRIMARY | reagent | getAvailableUserDefinedIdsMap | reagent_accession | ESR | reagent_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| description | yes | - | - | - | - | - | - | - | - | - | 
| is_set | - | - | - | - | - | - | - | yes | - | Y | 
| name | yes | - | - | - | - | - | - | - | - | - | 
| reagent_accessions | - | - | - | - | - | - | yes | - | - | - | 
| reagent_ids | yes | - | - | - | - | - | yes | - | - | - | 
| type | yes | - | lk_reagent_type | - | - | - | - | - | - | - | 
| user_defined_id | yes | - | - | - | - | - | - | - | - | - | 

### Foreign Key Information
FOREIGN KEY TYPE:	user-defined-id	Input column is a User Defined ID and the Output column is the Accession associated with User Defined ID in the given table if the input is a user defined ID

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | reagent_ids | reagent_accessions | reagent | getAvailableUserDefinedIdsMap | 

FOREIGN KEY TYPE:	accession	Input column is an Accession and the Output column is the Accession in the given table if the input is defined and an accession

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | reagent_ids | reagent_accessions | reagent | getAvailableAccsToParentMap | 

### Upload Table Information

Table: reagent    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| analyte_preferred | varchar | 15 | - | - | - | - | - | 
| analyte_reported | varchar | 200 | - | - | - | - | - | 
| antibody_registry_id | varchar | 250 | - | - | - | - | - | 
| catalog_number | varchar | 250 | - | - | - | - | - | 
| clone_name | varchar | 200 | - | - | - | - | - | 
| contact | varchar | 1000 | - | - | - | - | - | 
| description | varchar | 4000 | yes | - | - | - | - | 
| is_set | varchar | 1 | - | - | - | - | - | 
| lot_number | varchar | 250 | - | - | - | - | - | 
| manufacturer | varchar | 100 | - | - | - | - | - | 
| name | varchar | 200 | yes | - | - | - | - | 
| reagent_accession | varchar | 15 | - | - | - | - | - | 
| reporter_name | varchar | 200 | - | - | - | - | - | 
| type | varchar | 50 | - | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | - | - | 
| weblink | varchar | 250 | - | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: reagent_set_2_reagent    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| reagent_accession | varchar | 15 | - | - | - | reagent_accessions | yes | 
| reagent_set_accession | varchar | 15 | - | - | - | reagent_accession | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: workspace_2_reagent    Type: workspace

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| reagent_accession | varchar | 15 | - | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PostRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | LIST INPUT COLUMNS | LIST TABLE NAME | LIST VALIDATION QUERY NAME | 
|  --- | --- | --- | --- | --- | --- | --- |
| list type | not-equal-to-value | - | ['reagent_accessions'] | [] | reagent | getReagentSetAccNums | 


### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-reagents-to-reagent-set | - | [reagent_accessions, reagent_accession] | [] | - | - | - | 


### Controlled Vocabularies
| lk_reagent_type | lk_reagent_type | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 

