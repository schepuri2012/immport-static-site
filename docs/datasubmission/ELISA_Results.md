# Template: **elisa_results**

| Name | Value |
| --- | --- |
| Template Type | multiple |
| Schema Version | 3.33 |
| Standard File Name | ELISA_Results.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Analyte Reported | analyte_reported | The analyte describes what is being measured in an assay. The list of values displays common immunology terms on the left and their preferred term on the right, separated by a semi-colon. Please select a name from the list provided if the name matches your name or enter a name if there is not an appropriate one provided. This name is visible when the result is shared. | The analyte is the target (e.g protein, DNA, RNA) that is being assayed by the reagent. The list of values displays common immunology terms on the left and their preferred term on the right, separated by a semi-colon. Please select a name from the list provided if the name matches your name or enter a name if there is not an appropriate one provided. This name is visible when the result is shared. |
| Comments | comments | Unstructured text to further describe the result. | Unstructured text to further describe the result. |
| Expsample ID | expsample_id | The experiment sample identifier must be stored in ImmPort or in the experimentsamples.txt template. | Please enter either an experiment sample user defined ID or ImmPort accession. |
| Unit Reported | unit_reported | The analyte's concentration unit. | The analyte's concentration unit. |
| Value Reported | value_reported | The analyte's concentration value. | The analyte's concentration value. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| result_id | KEY | result_id | - | elisa_result_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| analyte_reported | yes | - | - | lk_analyte | analyte_preferred | - | - | - | - | - | 
| comments | - | - | - | - | - | - | - | - | - | - | 
| expsample_id | yes | - | - | - | - | - | - | - | - | - | 
| file_info_ids | - | - | - | - | - | - | yes | - | - | - | 
| immunology_symbol | - | - | - | lk_analyte | immunology_symbol | - | - | - | - | - | 
| max_components | - | - | - | - | - | - | - | yes | - | 3 | 
| result_schemas | - | - | - | - | - | - | yes | - | - | - | 
| short_label | - | - | - | lk_analyte | short_label | - | - | - | - | - | 
| unit_reported | yes | - | - | lk_concentration_unit | unit_preferred | - | - | - | - | - | 
| value_preferred | - | - | - | - | - | - | - | - | float | - | 
| value_reported | yes | - | - | - | - | - | - | - | - | - | 

### Foreign Key Information
FOREIGN KEY TYPE:	user-defined-id	Input column is a User Defined ID and the Output column is the Accession associated with User Defined ID in the given table if the input is a user defined ID

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | expsample_id | expsample_accession | expsample | getAvailableUserDefinedIdsMap | 

FOREIGN KEY TYPE:	accession	Input column is an Accession and the Output column is the Accession in the given table if the input is defined and an accession

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | expsample_id | expsample_accession | expsample | getAvailableAccsToParentMap | 

FOREIGN KEY TYPE:	accession-to-accession	Input column is an Accession and Output column is the parent Accession associated with the Accession in given table if the input column is defined and an accession

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | experiment_accession | study_accession | experiment | getAvailableAccsToParentMap | 

### Upload Table Information

Table: elisa_result    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| analyte_preferred | varchar | 15 | - | - | - | - | - | 
| analyte_reported | varchar | 100 | yes | - | - | - | - | 
| comments | varchar | 500 | yes | - | - | - | - | 
| experiment_accession | varchar | 15 | - | - | - | - | - | 
| expsample_accession | varchar | 15 | - | - | - | - | - | 
| file_info_id | integer | - | - | - | - | result_file_info_id | - | 
| result_id | integer | - | - | - | - | - | - | 
| unit_preferred | varchar | 50 | - | - | - | - | - | 
| unit_reported | varchar | 200 | yes | - | - | - | - | 
| value_preferred | float | - | - | - | - | - | - | 
| value_reported | varchar | 50 | yes | - | - | - | - | 

Table: expsample_2_file_info    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| expsample_accession | varchar | 15 | - | - | - | - | - | 
| file_info_id | integer | - | - | - | - | file_info_ids | yes | 
| result_schema | varchar | 50 | - | - | - | result_schemas | yes | 

### PostRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | check-result-schema-for-accession | - | ['expsample', 'expsample_accession', 'rs_result_schema', 'getEntityToResultSchemaMap'] | 


### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-semi-colon-if-needed | - | [analyte_reported, max_components, left] | [analyte_reported] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| break-into-components | - | [analyte_reported] | [immunology_symbol, short_label, analyte_reported] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| convert-to-float | - | [value_reported] | [value_preferred] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-template-file-name | - | [] | [result_file_name] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-file-info-ids | - | [result_file_name] | [result_file_info_id] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-file-info | - | [result_file_name, result] | [result_schema] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| get-result-schema-result | - | [] | [rs_result_schema] | - | - | - | 


### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| convert-concentration-and-round | Provided Below | [unit_preferred, value_preferred] | [unit_preferred, value_preferred] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	not-empty-value	analyte_preferred	-
	not-empty-value	unit_preferred	-
	not-empty-value	value_preferred	-

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-accession-to-file-info-for-result | Provided Below | [expsample_accession, result_file_info_id] | [file_info_id] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	not-empty-value	expsample_accession	-

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-data-to-lists | Provided Below | [file_info_id, result_schema] | [file_info_ids, result_schemas] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	not-empty-value	file_info_id	-

### Preferred Vocabularies

#### Column: analyte_reported Table: lk_analyte

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | immunology_symbol | immunology_symbol | immunology_symbol | 
|  | short_label | short_label | short_label | 
|  | analyte_reported | analyte_preferred | analyte_preferred | 

#### Column: unit_reported Table: lk_concentration_unit

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | unit_reported | unit_preferred | concentration_unit_preferred | 


### Preferred Vocabulary Tables

#### lk_analyte

| lk_analyte | lk_analyte | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | analyte_preferred | immunology_symbol | official_gene_name | id | gene_symbol | description | short_label | link | 
|  | DATABASE COLUMNS | analyte_accession | immunology_symbol | official_gene_name | gene_id | gene_symbol | protein_ontology_name | protein_ontology_short_label | link | 

#### lk_concentration_unit

| lk_concentration_unit | lk_unit_of_measure | database | type in ('concentration','Not_Specified') | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | concentration_unit_preferred | description | link | 
|  | DATABASE COLUMNS | name | description | link | 


