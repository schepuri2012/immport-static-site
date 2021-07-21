# Template: **hla_typing**

| Name | Value |
| --- | --- |
| Template Type | multiple |
| Schema Version | 3.33 |
| Standard File Name | HLA_Typing.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Ancestral Population | ancestral_population | ImmPort recommends using population names as defined by the http://www.allelefrequencies.net site. | ImmPort recommends using population names as defined by the http://www.allelefrequencies.net site. |
| Comments | comments | Comments captures additional descriptive information. | Comments captures additional descriptive information. |
| Expsample ID | expsample_id | The experiment sample identifier must be stored in ImmPort or in the experimentsamples.txt template. | Please enter either an experiment sample user defined ID or ImmPort accession. |
| HLA-A Allele 1 | hla-a.allele_1 |  |  |
| HLA-A Allele 2 | hla-a.allele_2 |  |  |
| HLA-B Allele 1 | hla-b.allele_1 |  |  |
| HLA-B Allele 2 | hla-b.allele_2 |  |  |
| HLA-C Allele 1 | hla-c.allele_1 |  |  |
| HLA-C Allele 2 | hla-c.allele_2 |  |  |
| HLA-DPA1 Allele 1 | hla-dpa1.allele_1 |  |  |
| HLA-DPA1 Allele 2 | hla-dpa1.allele_2 |  |  |
| HLA-DPB1 Allele 1 | hla-dpb1.allele_1 |  |  |
| HLA-DPB1 Allele 2 | hla-dpb1.allele_2 |  |  |
| HLA-DQA1 Allele 1 | hla-dqa1.allele_1 |  |  |
| HLA-DQA1 Allele 2 | hla-dqa1.allele_2 |  |  |
| HLA-DQB1 Allele 1 | hla-dqb1.allele_1 |  |  |
| HLA-DQB1 Allele 2 | hla-dqb1.allele_2 |  |  |
| HLA-DRB1 Allele 1 | hla-drb1.allele_1 |  |  |
| HLA-DRB1 Allele 2 | hla-drb1.allele_2 |  |  |
| HLA-DRB3 Allele 1 | hla-drb3.allele_1 |  |  |
| HLA-DRB3 Allele 2 | hla-drb3.allele_2 |  |  |
| HLA-DRB4 Allele 1 | hla-drb4.allele_1 |  |  |
| HLA-DRB4 Allele 2 | hla-drb4.allele_2 |  |  |
| HLA-DRB5 Allele 1 | hla-drb5.allele_1 |  |  |
| HLA-DRB5 Allele 2 | hla-drb5.allele_2 |  |  |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| result_set_id | KEY | result_set_id | - | hla_typing_result_rset_id_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| allele_1_list | - | - | - | - | - | - | yes | - | - | - | 
| allele_2_list | - | - | - | - | - | - | yes | - | - | - | 
| ancestral_population | yes | - | lk_ancestral_population | - | - | - | yes | - | - | - | 
| comments | - | - | - | - | - | - | - | - | - | - | 
| expsample_id | yes | - | - | - | - | - | - | - | - | - | 
| file_info_ids | - | - | - | - | - | - | yes | - | - | - | 
| global.result_id_sequence | - | - | - | - | - | yes | - | - | - | hla_typing_result_rslt_id_seq | 
| hla-a.allele_1 | - | - | - | - | - | - | - | - | - | - | 
| hla-a.allele_2 | - | - | - | - | - | - | - | - | - | - | 
| hla-b.allele_1 | - | - | - | - | - | - | - | - | - | - | 
| hla-b.allele_2 | - | - | - | - | - | - | - | - | - | - | 
| hla-c.allele_1 | - | - | - | - | - | - | - | - | - | - | 
| hla-c.allele_2 | - | - | - | - | - | - | - | - | - | - | 
| hla-dpa1.allele_1 | - | - | - | - | - | - | - | - | - | - | 
| hla-dpa1.allele_2 | - | - | - | - | - | - | - | - | - | - | 
| hla-dpb1.allele_1 | - | - | - | - | - | - | - | - | - | - | 
| hla-dpb1.allele_2 | - | - | - | - | - | - | - | - | - | - | 
| hla-dqa1.allele_1 | - | - | - | - | - | - | - | - | - | - | 
| hla-dqa1.allele_2 | - | - | - | - | - | - | - | - | - | - | 
| hla-dqb1.allele_1 | - | - | - | - | - | - | - | - | - | - | 
| hla-dqb1.allele_2 | - | - | - | - | - | - | - | - | - | - | 
| hla-drb1.allele_1 | - | - | - | - | - | - | - | - | - | - | 
| hla-drb1.allele_2 | - | - | - | - | - | - | - | - | - | - | 
| hla-drb3.allele_1 | - | - | - | - | - | - | - | - | - | - | 
| hla-drb3.allele_2 | - | - | - | - | - | - | - | - | - | - | 
| hla-drb4.allele_1 | - | - | - | - | - | - | - | - | - | - | 
| hla-drb4.allele_2 | - | - | - | - | - | - | - | - | - | - | 
| hla-drb5.allele_1 | - | - | - | - | - | - | - | - | - | - | 
| hla-drb5.allele_2 | - | - | - | - | - | - | - | - | - | - | 
| locus_name_list | - | - | lk_locus_name | - | - | - | yes | - | - | - | 
| max_components | - | - | - | - | - | - | - | yes | - | 3 | 
| result_id_list | - | - | - | - | - | - | yes | - | - | - | 
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

Table: hla_typing_result    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| allele_1 | varchar | 250 | yes | - | - | allele_1_list | yes | 
| allele_2 | varchar | 250 | yes | - | - | allele_2_list | yes | 
| ancestral_population | varchar | 250 | - | - | - | - | - | 
| comments | varchar | 500 | yes | - | - | - | - | 
| experiment_accession | varchar | 15 | - | - | - | - | - | 
| expsample_accession | varchar | 15 | - | - | - | - | - | 
| file_info_id | integer | - | - | - | - | result_file_info_id | - | 
| locus_name | varchar | 25 | - | - | - | locus_name_list | yes | 
| result_id | integer | - | - | - | - | result_id_list | yes | 
| result_set_id | integer | - | - | - | - | - | - | 

Table: expsample_2_file_info    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| expsample_accession | varchar | 15 | - | - | - | - | - | 
| file_info_id | integer | - | - | - | - | file_info_ids | yes | 
| result_schema | varchar | 50 | - | - | - | result_schemas | yes | 

### PreRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | at-least-one-nonempty | Provided Below | ['hla-a.allele_1', 'hla-a.allele_2', 'hla-b.allele_1', 'hla-b.allele_2', 'hla-c.allele_1', 'hla-c.allele_2', 'hla-dpa1.allele_1', 'hla-dpa1.allele_2', 'hla-dpb1.allele_1', 'hla-dpb1.allele_2', 'hla-dqa1.allele_1', 'hla-dqa1.allele_2', 'hla-dqb1.allele_1', 'hla-dqb1.allele_2', 'hla-drb1.allele_1', 'hla-drb1.allele_2', 'hla-drb3.allele_1', 'hla-drb3.allele_2', 'hla-drb4.allele_1', 'hla-drb4.allele_2', 'hla-drb5.allele_1', 'hla-drb5.allele_2'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		not-empty-value	expsample_id	-

### PostRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | check-result-schema-for-accession | - | ['expsample', 'expsample_accession', 'rs_result_schema', 'getEntityToResultSchemaMap'] | 


### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-hla-loci | - | [hla-a.allele_1, hla-a.allele_2, hla-b.allele_1, hla-b.allele_2, hla-c.allele_1, hla-c.allele_2, hla-dpa1.allele_1, hla-dpa1.allele_2, hla-dpb1.allele_1, hla-dpb1.allele_2, hla-dqa1.allele_1, hla-dqa1.allele_2, hla-dqb1.allele_1, hla-dqb1.allele_2, hla-drb1.allele_1, hla-drb1.allele_2, hla-drb3.allele_1, hla-drb3.allele_2, hla-drb4.allele_1, hla-drb4.allele_2, hla-drb5.allele_1, hla-drb5.allele_2] | [locus_name_list, allele_1_list, allele_2_list] | - | - | - | 


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
| assign-result-id | - | [locus_name_list, global.result_id_sequence] | [result_id_list] | - | - | - | 


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

### Controlled Vocabularies
| lk_ancestral_population | lk_ancestral_population | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 
| lk_locus_name | lk_locus_name | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 

