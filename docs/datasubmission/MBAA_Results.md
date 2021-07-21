# Template: **mbaa_results**

| Name | Value |
| --- | --- |
| Template Type | single |
| Schema Version | 3.33 |
| Standard File Name | MBAA_Results.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Analyte Reported | analyte_reported | The analyte describes what is being measured in an assay. The list of values displays common immunology gene symbol and gene symbol terms on the left and their preferred term on the right, each component separated by a semi-colon. Please select a name from the list provided if the name matches your name or enter a name if there is not an appropriate one provided. This name is visible when the result is shared. | The analyte is the target (e.g protein, DNA, RNA) that is being assayed by the reagent. The list of values displays common immunology gene symbol and gene symbol terms on the left and their preferred term on the right, each component separated by a semi-colon. Please select a name from the list provided if the name matches your name or enter a name if there is not an appropriate one provided. This name is visible when the result is shared. |
| Assay Group ID | assay_group_id | The assay group ID represents a collection of plates or arrays. This ID may be used to link collections of standard curves, control samples, and experiment samples results. | The assay group ID represents a collection of plates or arrays. This ID may be used to link collections of standard curves, control samples, and experiment samples results. |
| Assay ID | assay_id | The assay ID represents the plate or array ID where standard curves, control samples, and experiment samples were collected and assayed. This ID will be used to link standard curves, control samples, and experiment samples results. | The assay ID represents the plate or array ID where standard curves, control samples, and experiment samples were collected and assayed. This ID will be used to link standard curves, control samples, and experiment samples results. |
| Comments | comments | Additional descriptive information. | Additional descriptive information. |
| Concentration Unit Reported | concentration_unit_reported | The concentration unit of the standard curve sample or calculated from the MFI using the standard curve | The concentration unit of the standard curve sample or calculated from the MFI using the standard curve. |
| Concentration Value Reported | concentration_value_reported | The reported concentration value of the standard curve sample or calculated from the MFI using the standard curve. | A number is expected. |
| MFI | mfi | Mean Fluorescence Intensity | Mean Fluorescence Intensity |
| MFI Coordinate | mfi_coordinate | The position on the assay plate. | The position on the assay plate. |
| Source ID | source_id | The source ID is defined in the corresponding ImmPort template. | The source ID for the assay result is either an experiment sample, a control sample, or a standard curve. |
| Source Type | source_type | The source type is either an experiment sample, control sample or standard curve. | Please choose from the drop down list. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| result_id | KEY | result_id | - | mbaa_result_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| analyte_reported | yes | - | - | lk_analyte | analyte_preferred | - | - | - | - | - | 
| assay_group_id | - | - | - | - | - | - | - | - | - | - | 
| assay_id | yes | - | - | - | - | - | - | - | - | - | 
| comments | - | - | - | - | - | - | - | - | - | - | 
| concentration_unit_reported | yes | - | - | lk_concentration_unit | concentration_unit_preferred | - | - | - | - | - | 
| concentration_value_reported | yes | - | - | - | - | - | - | - | - | - | 
| file_info_ids | - | - | - | - | - | - | yes | - | - | - | 
| global.assay_info_for_expsample_query | - | - | - | - | - | yes | - | - | - | getAssayInfoExpsample | 
| global.assay_info_query | - | - | - | - | - | yes | - | - | - | getAssayInfo | 
| immunology_symbol | - | - | - | lk_analyte | immunology_symbol | - | - | - | - | - | 
| max_components | - | - | - | - | - | - | - | yes | - | 3 | 
| mfi | yes | - | - | - | - | - | - | - | - | - | 
| mfi_coordinate | - | - | - | - | - | - | - | - | - | - | 
| result_schemas | - | - | - | - | - | - | yes | - | - | - | 
| short_label | - | - | - | lk_analyte | short_label | - | - | - | - | - | 
| source_id | - | - | - | - | - | - | - | - | - | - | 
| source_type | yes | - | lk_source_type | - | - | - | - | - | - | - | 

### Foreign Key Information
FOREIGN KEY TYPE:	accession-to-accession	Input column is an Accession and Output column is the parent Accession associated with the Accession in given table if the input column is defined and an accession

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | experiment_accession | study_accession | experiment | getAvailableAccsToParentMap | 

### Upload Table Information

Table: mbaa_result    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| analyte_preferred | varchar | 15 | - | - | - | - | - | 
| analyte_reported | varchar | 100 | yes | - | - | - | - | 
| assay_group_id | varchar | 100 | - | - | - | - | - | 
| assay_id | varchar | 100 | - | - | - | - | - | 
| comments | varchar | 500 | yes | - | - | - | - | 
| concentration_unit_preferred | varchar | 50 | - | - | - | - | - | 
| concentration_unit_reported | varchar | 100 | yes | - | - | - | - | 
| concentration_value_preferred | float | - | - | - | - | - | - | 
| concentration_value_reported | varchar | 100 | yes | - | - | - | - | 
| experiment_accession | varchar | 15 | - | - | - | - | - | 
| file_info_id | integer | - | - | - | - | result_file_info_id | - | 
| mfi | varchar | 100 | yes | - | - | - | - | 
| mfi_coordinate | varchar | 100 | yes | - | - | - | - | 
| result_id | integer | - | - | - | - | - | - | 
| source_accession | varchar | 15 | - | - | - | - | - | 
| source_type | varchar | 30 | - | - | - | - | - | 

Table: control_sample_2_file_info    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| control_sample_accession | varchar | 15 | - | - | - | - | - | 
| file_info_id | integer | - | - | - | - | control_sample_file_info_id | yes | 
| result_schema | varchar | 50 | - | - | - | - | - | 

Table: expsample_2_file_info    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| expsample_accession | varchar | 15 | - | - | - | - | - | 
| file_info_id | integer | - | - | - | - | file_info_ids | yes | 
| result_schema | varchar | 50 | - | - | - | result_schemas | yes | 

Table: standard_curve_2_file_info    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| file_info_id | integer | - | - | - | - | standard_curve_file_info_id | yes | 
| result_schema | varchar | 50 | - | - | - | - | - | 
| standard_curve_accession | varchar | 15 | - | - | - | - | - | 

### PostRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | not-empty-value | - | ['source_accession'] | 


| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | values-equal | - | ['Value in result is not value in the EXPSAMPLE, CONTROL SAMPLE, or STANDARD CURVE', 'assay_id', 'source.assay_id'] | 


| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | values-equal | Provided Below | ['Value in result is not value in the EXPSAMPLE, CONTROL SAMPLE, or STANDARD CURVE', 'assay_group_id', 'source.assay_group_id'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		not-empty-value	source.assay_group_id	-

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | check-result-schema-for-accession | Provided Below | ['expsample', 'expsample_accession', 'rs_result_schema', 'getEntityToResultSchemaMap'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		case-insensitive-equals	source_type	'expsample'

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | check-result-schema-for-accession | Provided Below | ['control_sample', 'control_sample_accession', 'rs_result_schema', 'getEntityToResultSchemaMap'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		case-insensitive-equals	source_type	'control sample'

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | check-result-schema-for-accession | Provided Below | ['standard_curve', 'standard_curve_accession', 'rs_result_schema', 'getEntityToResultSchemaMap'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		case-insensitive-equals	source_type	'standard curve'

### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-assay-info | Provided Below | [source_id, source_type, global.assay_info_for_expsample_query] | [source_accession, experiment_accession, source.assay_group_id, source.assay_id] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	source_type	'expsample'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-assay-info | Provided Below | [source_id, source_type, global.assay_info_query] | [source_accession, experiment_accession, source.assay_group_id, source.assay_id] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	source_type	'control sample'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-assay-info | Provided Below | [source_id, source_type, global.assay_info_query] | [source_accession, experiment_accession, source.assay_group_id, source.assay_id] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	source_type	'standard curve'

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
| add-semi-colon-if-needed | - | [analyte_reported, max_components, left] | [analyte_reported] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| break-into-components | - | [analyte_reported] | [immunology_symbol, short_label, analyte_reported] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| get-result-schema-result | - | [] | [rs_result_schema] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [source_accession] | [expsample_accession] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	source_type	'expsample'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [source_accession] | [control_sample_accession] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	source_type	'control sample'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [source_accession] | [standard_curve_accession] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	source_type	'standard curve'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| convert-to-float | - | [concentration_value_reported] | [concentration_value_preferred] | - | - | - | 


### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-accession-to-file-info-for-result | Provided Below | [control_sample_accession, result_file_info_id] | [control_sample_file_info_id] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	not-empty-value	control_sample_accession	-

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-accession-to-file-info-for-result | Provided Below | [standard_curve_accession, result_file_info_id] | [standard_curve_file_info_id] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	not-empty-value	standard_curve_accession	-

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

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| convert-concentration-and-round | Provided Below | [concentration_unit_preferred, concentration_value_preferred] | [concentration_unit_preferred, concentration_value_preferred] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	not-empty-value	analyte_preferred	-
	not-empty-value	concentration_unit_preferred	-
	not-empty-value	concentration_value_preferred	-

### Controlled Vocabularies
| lk_source_type | lk_source_type | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | table_name | 
|  | DATABASE COLUMNS | name | description | link | table_name | 
### Preferred Vocabularies

#### Column: analyte_reported Table: lk_analyte

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | immunology_symbol | immunology_symbol | immunology_symbol | 
|  | short_label | short_label | short_label | 
|  | analyte_reported | analyte_preferred | analyte_preferred | 

#### Column: concentration_unit_reported Table: lk_concentration_unit

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | concentration_unit_reported | concentration_unit_preferred | concentration_unit_preferred | 


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


