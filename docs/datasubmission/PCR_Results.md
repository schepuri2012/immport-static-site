# Template: **pcr_results**

| Name | Value |
| --- | --- |
| Template Type | multiple |
| Schema Version | 3.33 |
| Standard File Name | PCR_Results.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Comments | comments | Comments captures additional descriptive information. | Comments captures additional descriptive information. |
| Expsample ID | expsample_id | The experiment sample identifier must be stored in ImmPort or in the experimentsamples.txt template. | Please enter either an experiment sample user defined ID or ImmPort accession. |
| Gene ID | gene_id | The NCBI Gene ID for the gene being assayed. A number is expected. | A number is expected. |
| Gene Name | gene_name | The NCBI Gene name for the gene being assayed. | The NCBI Gene name for the gene being assayed. |
| Gene Symbol Name | gene_symbol_name | The NCBI Gene symbol for the gene being assayed. Please select a gene symbol from the list provided if the gene symbol matches your symbol or enter a symbol if there is not an appropriate one provided. This symbol is visible when the result is shared. If the gene symbol is a NCBI Gene Symbol that is provided in the list, then the columns 'Gene Name' and 'Gene ID' will also be overwritten by the gene name and Entrez Gene ID provided by NCBI. | The NCBI Gene symbol for the gene being assayed. Please select a gene symbol from the list provided if the gene symbol matches your symbol or enter a symbol if there is not an appropriate one provided. This symbol is visible when the result is shared. |
| Other Gene Accession | other_gene_accession | Additional identifier(s) for the gene being assayed. | Additional identifier(s) for the gene being assayed. |
| Unit Reported | unit_reported | The unit for the Expression Value Of Target Nucleic ACID. Please select a unit from the list provided if the unit matches your unit or enter a unit if there is not an appropriate one provided. | The unit for the Expression Value Of Target Nucleic ACID. Please select a unit from the list provided if the unit matches your unit or enter a unit if there is not an appropriate one provided. |
| Value Reported | value_reported | This value could be absolute or relative. For example, an absolute expression value could be 6 ng RNA/mg intestine. In this case, 6 should be entered in the 'Expression value of target RNA' column, while ng RNA/ mg intestine is in the 'Expression unit of target RNA' column. A relative expression value, like signal versus GAPDH, could be 2.07. In this case, 2.07 should be in the 'Expression value of target RNA' column, while relative to GAPDH is in the 'Expression unit of target RNA' column. | A number is expected. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| result_id | KEY | result_id | - | pcr_result_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| comments | - | - | - | - | - | - | - | - | - | - | 
| expsample_id | yes | - | - | - | - | - | - | - | - | - | 
| file_info_ids | - | - | - | - | - | - | yes | - | - | - | 
| gene_id | - | - | - | - | - | - | - | - | - | - | 
| gene_name | - | - | - | - | - | - | - | - | - | - | 
| gene_symbol_name | yes | - | - | - | - | - | - | - | - | - | 
| gene_symbol_reported | - | - | - | lk_analyte | gene_symbol_preferred | - | - | - | - | - | 
| immunology_symbol | - | - | - | lk_analyte | immunology_symbol | - | - | - | - | - | 
| max_components | - | - | - | - | - | - | - | yes | - | 3 | 
| other_gene_accession | - | - | - | - | - | - | - | - | - | - | 
| result_schemas | - | - | - | - | - | - | yes | - | - | - | 
| short_label | - | - | - | lk_analyte | short_label | - | - | - | - | - | 
| unit_reported | yes | - | - | lk_pcr_expression_unit | unit_preferred | - | - | - | - | - | 
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

Table: pcr_result    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| comments | varchar | 500 | yes | - | - | - | - | 
| experiment_accession | varchar | 15 | - | - | - | - | - | 
| expsample_accession | varchar | 15 | - | - | - | - | - | 
| file_info_id | integer | - | - | - | - | result_file_info_id | - | 
| gene_id | varchar | 10 | yes | - | - | - | - | 
| gene_name | varchar | 4000 | yes | - | - | - | - | 
| gene_symbol_preferred | varchar | 15 | - | - | - | - | - | 
| gene_symbol_reported | varchar | 100 | yes | - | - | - | - | 
| other_gene_accession | varchar | 250 | yes | - | - | - | - | 
| result_id | integer | - | - | - | - | - | - | 
| unit_preferred | varchar | 200 | - | - | - | - | - | 
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
| add-semi-colon-if-needed | - | [gene_symbol_name, max_components, left] | [gene_symbol_name] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| break-into-components | - | [gene_symbol_name] | [immunology_symbol, short_label, gene_symbol_reported] | - | - | - | 


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

#### Column: gene_symbol_name Table: lk_analyte

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | immunology_symbol | immunology_symbol | immunology_symbol | 
|  | short_label | short_label | short_label | 
|  | gene_symbol_reported | gene_symbol_preferred | analyte_preferred | 
|  |  | ANCILLARY DATA | 
|  |  | DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  |  | gene_id | id | 
|  |  | gene_name | official_gene_name | 

#### Column: unit_reported Table: lk_pcr_expression_unit

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | unit_reported | unit_preferred | expression_unit_preferred | 


### Preferred Vocabulary Tables

#### lk_analyte

| lk_analyte | lk_analyte | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | analyte_preferred | immunology_symbol | official_gene_name | id | gene_symbol | description | short_label | link | 
|  | DATABASE COLUMNS | analyte_accession | immunology_symbol | official_gene_name | gene_id | gene_symbol | protein_ontology_name | protein_ontology_short_label | link | 

#### lk_pcr_expression_unit

| lk_pcr_expression_unit | lk_unit_of_measure | database | type in ('PCR','Not_Specified') | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | expression_unit_preferred | description | link | 
|  | DATABASE COLUMNS | name | description | link | 


