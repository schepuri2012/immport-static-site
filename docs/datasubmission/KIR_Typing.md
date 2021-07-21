# Template: **kir_typing**

| Name | Value |
| --- | --- |
| Template Type | multiple |
| Schema Version | 3.33 |
| Standard File Name | KIR_Typing.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Allele 1 | allele_1 |  |  |
| Allele 2 | allele_2 |  |  |
| Comments | comments |  |  |
| Expsample ID | expsample_id | The experiment sample identifier must be stored in ImmPort or in the experimentsamples.txt template. | Please enter either an experiment sample user defined ID or ImmPort accession. |
| KIR Haplotype | kir_haplotype |  |  |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| result_id | KEY | result_id | - | kir_typing_result_rslt_id_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| allele_1 | - | - | - | - | - | - | - | - | - | - | 
| allele_2 | - | - | - | - | - | - | - | - | - | - | 
| comments | - | - | - | - | - | - | - | - | - | - | 
| expsample_id | yes | - | - | - | - | - | - | - | - | - | 
| file_info_ids | - | - | - | - | - | - | yes | - | - | - | 
| kir_haplotype | yes | - | - | - | - | - | - | - | - | - | 
| max_components | - | - | - | - | - | - | - | yes | - | 3 | 
| result_schemas | - | - | - | - | - | - | yes | - | - | - | 

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

Table: kir_typing_result    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| allele_1 | varchar | 250 | yes | - | - | - | - | 
| allele_2 | varchar | 250 | yes | - | - | - | - | 
| comments | varchar | 500 | yes | - | - | - | - | 
| experiment_accession | varchar | 15 | - | - | - | - | - | 
| expsample_accession | varchar | 15 | - | - | - | - | - | 
| file_info_id | integer | - | - | - | - | result_file_info_id | - | 
| kir_haplotype | varchar | 250 | yes | - | - | - | - | 
| result_id | integer | - | - | - | - | - | - | 

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

