# Template: **standardcurves**

| Name | Value |
| --- | --- |
| Template Type | combined |
| Schema Version | 3.33 |
| Standard File Name | standardCurves.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Additional Result File Names | additional_result_file_names | See the ImmPort Data Upload Guide for details on where MBAA bead level files are stored depending on the assay platform used. Separate file names by a semi-colon (;). The file size name limit is 240 characters. | HIPC recommends including bead level result files if they are available. The file size name limit is 240 characters. |
| Analyte Reported | analyte_reported | The molecule or entity being measured. Please select a name from the list provided if the name matches your name or enter a name if there is not an appropriate one provided. This name is visible when the result is shared. | The molecule or entity being measured. Please select a name from the list provided if the name matches your name or enter a name if there is not an appropriate one provided. This name is visible when the result is shared. |
| Assay Group ID | assay_group_id | The assay group ID represents a collection of plates or arrays. This ID may be used to link collections of standard curves, control samples, and experiment samples results. | The assay group ID represents a collection of plates or arrays. This ID may be used to link collections of standard curves, control samples, and experiment samples results. |
| Assay ID | assay_id | The assay ID represents the plate or array ID where standard curves, control samples, and experiment samples were collected and assayed. This ID will be used to link standard curves, control samples, and experiment samples results. | The assay ID represents the plate or array ID where standard curves, control samples, and experiment samples were collected and assayed. This ID will be used to link standard curves, control samples, and experiment samples results. |
| Description | description | The experiment description is used to describe details of the experiment not captured in other columns. | The experiment description is used to describe details of the experiment not captured in other columns. |
| Experiment ID | experiment_id | The experiment identifier must be stored in ImmPort or in the experiments.txt template. | Please enter either a experiment user defined ID or ImmPort accession. |
| Formula | formula | The formula used to calculate the standard curve from the input data. | The formula used to calculate the standard curve from the input data. |
| ImmPort Template? | immport_template | The format of the result file depends on the assay type. ImmPort supports results templates (MBAA_Results.txt) for some of the commonly used immunological assay methods. These template facilitate the sharing and re-use of results data in a standard format. If the result file is the ImmPort results template (strongly recommended by NIAID DAIT), choose 'Yes' from the drop down list and do not include a file name in the "Result File Name" column. If the result file is not an ImmPort results template, choose 'No' from the drop down list and include a file name in the "Result File Name" column. | The format of the result file depends on the assay type. ImmPort supports results templates (MBAA_Results.txt) for some of the commonly used immunological assay methods. These template facilitate the sharing and re-use of results data in a standard format. If the result file is the ImmPort results template (strongly recommended by NIAID DAIT), choose 'Yes' from the drop down list and do not include a file name in the "Result File Name" column. If the result file is not an ImmPort results template, choose 'No' from the drop down list and include a file name in the "Result File Name" column. |
| Lower Limit | lower_limit | A number is expected. | Lower limit value established by the standard curve. |
| Lower Limit Unit | lower_limit_unit | Lower limit unit established by the standard curve. | Lower limit unit established by the standard curve. |
| Measurement Technique | measurement_technique | The measurement technique describes the assay method. | Choose from a drop down list. |
| Name | name | The experiment name is not referenced by other data records. | The experiment name is an alternate identifier that is visible when the sample is shared. |
| Protocol ID(s) | protocol_ids | Please enter either a protocol user defined ID or ImmPort accession for a protocol that describes how the sample was derived and prepared. One or more identifiers can be entered per sample. Separate identifiers by semicolon (;). | Please enter either a protocol user defined ID or ImmPort accession. |
| Result File Name | result_file_name | Enter the full result file name including file extension. The file size name limit is 240 characters. | Enter the full result file name including file extension. The file size name limit is 240 characters. |
| Standard Curve ID | standard_curve_id | The Standard Curve user defined ID is an identifier chosen by the data provider to refer to a Standard Curve. This ID may be referenced by other data records (e.g. MBAA results). The user defined ID is not shared. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |
| Study ID | study_id | An experiment may be linked to a single study. | Please enter either a study user defined ID or ImmPort accession. |
| Upper Limit | upper_limit | A number is expected. | Upper limit value established by the standard curve. |
| Upper Limit Unit | upper_limit_unit | Upper limit value established by the standard curve. | Upper limit value established by the standard curve. |


### Combined Data

The ID Meta Data Columns include the ID columns that are referenced by more than one entity in the standard curve template (for example, experiments).  The standard curve ID is primary ID and can be defined only once and not re-used. The experiment ID can be pre-defined or defined once and re-used within the template.

| ID Columns | PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| standard_curve_required | determine-combined-status | - | [standard_curve_id, standard_curve] | [standard_curve_required, standard_curve_user_defined_id, standard_curve_accession] | - | - | - | 
| experiment_required | determine-combined-status | - | [experiment_id, experiment] | [experiment_required, experiment_user_defined_id, experiment_accession] | - | - | - | 

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| standard_curve_user_defined_id | USER_DEFINED_ID | standard_curve_accession | SC | standard_curve_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| experiment_user_defined_id | ANCILLARY | experiment | getAvailableUserDefinedIdsMap | experiment_accession | EXP | experiment_seq | 
| standard_curve_user_defined_id | PRIMARY | standard_curve | getAvailableUserDefinedIdsMap | standard_curve_accession | SC | standard_curve_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| additional_result_file_info_ids | - | - | - | - | - | - | yes | - | - | - | 
| additional_result_file_names | - | - | - | - | - | - | yes | - | - | - | 
| analyte_reported | - | yes | - | lk_analyte | analyte_preferred | - | - | - | - | - | 
| assay_group_id | - | - | - | - | - | - | - | - | - | - | 
| assay_id | - | yes | - | - | - | - | - | - | - | - | 
| description | - | - | - | - | - | - | - | - | - | - | 
| experiment_id | yes | - | - | - | - | - | - | - | - | - | 
| file_info_ids | - | - | - | - | - | - | yes | - | - | - | 
| formula | - | yes | - | - | - | - | - | - | - | - | 
| immport_template | - | yes | lk_yes_no | - | - | - | - | - | - | - | 
| immunology_symbol | - | - | - | lk_analyte | immunology_symbol | - | - | - | - | - | 
| lower_limit | - | yes | - | - | - | - | - | - | - | - | 
| lower_limit_unit | - | yes | - | - | - | - | - | - | - | - | 
| max_components | - | - | - | - | - | - | - | yes | - | 3 | 
| measurement_technique | - | yes | lk_exp_measurement_tech | - | - | - | - | - | - | - | 
| name | - | yes | - | - | - | - | - | - | - | - | 
| protocol_accessions | - | - | - | - | - | - | yes | - | - | - | 
| protocol_ids | - | yes | - | - | - | - | yes | - | - | - | 
| result_file_name | - | - | - | - | - | - | - | - | - | - | 
| result_schemas | - | - | - | - | - | - | yes | - | - | - | 
| sc_result_schema | - | - | lk_expsample_result_schema | - | - | - | - | - | - | - | 
| short_label | - | - | - | lk_analyte | short_label | - | - | - | - | - | 
| source_type | - | - | - | - | - | - | - | yes | - | standard curve | 
| standard_curve_id | yes | - | - | - | - | - | - | - | - | - | 
| study_id | - | yes | - | - | - | - | - | - | - | - | 
| upload_result_status | - | - | - | - | - | - | - | yes | - | Not_Parsed | 
| upper_limit | - | yes | - | - | - | - | - | - | - | - | 
| upper_limit_unit | - | yes | - | - | - | - | - | - | - | - | 

### Conditional Required Columns
| Column Name | CONDITION NAME | DATA ROW COLUMN | VALUE | 
|  --- | --- | --- | --- |
| study_id | case-insensitive-equals | experiment_required | 'Yes' | 
| protocol_ids | case-insensitive-equals | experiment_required | 'Yes' | 
| measurement_technique | case-insensitive-equals | experiment_required | 'Yes' | 
| name | case-insensitive-equals | experiment_required | 'Yes' | 
| analyte_reported | case-insensitive-equals | standard_curve_required | 'Yes' | 
| assay_id | case-insensitive-equals | standard_curve_required | 'Yes' | 
| immport_template | case-insensitive-equals | standard_curve_required | 'Yes' | 
| formula | case-insensitive-equals | standard_curve_required | 'Yes' | 
| lower_limit | case-insensitive-equals | standard_curve_required | 'Yes' | 
| lower_limit_unit | case-insensitive-equals | standard_curve_required | 'Yes' | 
| upper_limit | case-insensitive-equals | standard_curve_required | 'Yes' | 
| upper_limit_unit | case-insensitive-equals | standard_curve_required | 'Yes' | 

### Foreign Key Information
FOREIGN KEY TYPE:	user-defined-id	Input column is a User Defined ID and the Output column is the Accession associated with User Defined ID in the given table if the input is a user defined ID

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | protocol_ids | protocol_accessions | protocol | getAvailableUserDefinedIdsMap | 

FOREIGN KEY TYPE:	accession	Input column is an Accession and the Output column is the Accession in the given table if the input is defined and an accession

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | protocol_ids | protocol_accessions | protocol | getAvailableAccsToParentMap | 

### File Info Information

| FILE NAME COLUMN | FILE TYPE | STUDY ACCESSION COLUMN | 
|  --- | --- | --- |
| additional_result_file_names | additional | study_accession | 
| result_file_name | result | study_accession | 

### Upload Table Information

Table: experiment    Type: ancillary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| description | varchar | 4000 | yes | - | - | - | - | 
| experiment_accession | varchar | 15 | - | - | - | - | - | 
| measurement_technique | varchar | 50 | - | - | - | - | - | 
| name | varchar | 500 | yes | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | experiment_user_defined_id | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: standard_curve    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| analyte_preferred | varchar | 15 | - | - | - | - | - | 
| analyte_reported | varchar | 100 | yes | - | - | - | - | 
| assay_group_id | varchar | 100 | yes | - | - | - | - | 
| assay_id | varchar | 100 | yes | - | - | - | - | 
| experiment_accession | varchar | 15 | - | - | - | - | - | 
| formula | varchar | 500 | yes | - | - | - | - | 
| lower_limit | varchar | 100 | yes | - | - | - | - | 
| lower_limit_unit | varchar | 100 | yes | - | - | - | - | 
| result_schema | varchar | 50 | - | - | - | sc_result_schema | - | 
| standard_curve_accession | varchar | 15 | - | - | - | - | - | 
| upload_result_status | varchar | 20 | - | - | - | - | - | 
| upper_limit | varchar | 100 | yes | - | - | - | - | 
| upper_limit_unit | varchar | 100 | yes | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | standard_curve_user_defined_id | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: experiment_2_protocol    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| experiment_accession | varchar | 15 | - | - | - | - | - | 
| protocol_accession | varchar | 15 | - | - | - | protocol_accessions | yes | 

Table: standard_curve_2_file_info    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| file_info_id | integer | - | - | - | - | file_info_ids | yes | 
| result_schema | varchar | 50 | - | - | - | result_schemas | yes | 
| standard_curve_accession | varchar | 15 | - | - | - | - | - | 

Table: workspace_2_experiment    Type: workspace

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| experiment_accession | varchar | 15 | - | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: workspace_2_standard_curve    Type: workspace

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| standard_curve_accession | varchar | 15 | - | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PreRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | check-immport-template | - | ['immport_template', 'result_file_name'] | 


### PostRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | values-not-equal | Provided Below | ['For an existing experiment, the standard curve must be new.', 'experiment_required', 'standard_curve_required'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		case-insensitive-equals	experiment_required	'No'

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | values-equal | Provided Below | ['For an new experiment, the standard curve must be new.', 'experiment_required', 'standard_curve_required'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		case-insensitive-equals	experiment_required	'Yes'

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | check-not-contains-case-insensitive | - | ['result_file_name', 'additional_result_file_names'] | 


| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | check-result-schema-for-result-file | Provided Below | ['result_file_name', 'sc_result_schema'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		case-insensitive-equals	standard_curve_required	'Yes'

### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-parent-accession | Provided Below | [experiment_accession, experiment, accession-to-accession] | [study_accession] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	experiment_required	'No'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| initialize-columns | Provided Below | [] | [description, measurement_technique, protocol_ids, study_id, name] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	experiment_required	'No'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-resultfile-name | - | [immport_template, result_file_name] | [result_file_name] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-case-insensitive-list | - | [additional_result_file_names] | [additional_result_file_names] | - | - | - | 


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
| get-result-schema | - | [immport_template] | [sc_result_schema] | - | - | - | 


### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-result-schema | Provided Below | [standard_curve, standard_curve_accession, sc_result_schema] | [] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	standard_curve_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-child-to-parent-accession | Provided Below | [experiment, accession-to-accession, getAvailableAccsToParentMap, experiment_accession, study_accession] | [] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	experiment_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-file-info-ids | Provided Below | [result_file_name] | [result_filename_file_info_id] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	standard_curve_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-file-info-ids | Provided Below | [additional_result_file_names] | [additional_result_file_info_ids] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	standard_curve_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-assay-info | Provided Below | [source_type, standard_curve_user_defined_id, standard_curve_accession, experiment_accession, assay_group_id, assay_id] | [] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	standard_curve_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-accession-to-file-info | Provided Below | [standard_curve_accession, result_filename_file_info_id] | [] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	standard_curve_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-accession-to-file-info | Provided Below | [standard_curve_accession, additional_result_file_info_ids] | [] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	standard_curve_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-file-info | Provided Below | [additional_result_file_names, additional] | [result_schemas] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	standard_curve_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-data-to-lists | Provided Below | [additional_result_file_info_ids] | [file_info_ids] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	standard_curve_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-data-to-lists | Provided Below | [result_filename_file_info_id, result_schema] | [file_info_ids, result_schemas] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	standard_curve_required	'Yes'

### Controlled Vocabularies
| lk_exp_measurement_tech | lk_exp_measurement_tech | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 
| lk_expsample_result_schema | lk_expsample_result_schema | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | 
|  | DATABASE COLUMNS | name | description | 
| lk_yes_no | - | static | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | 
|  | DATABASE COLUMNS | name | description | 
	DATA VALUES	No	No
		Yes	Yes
### Preferred Vocabularies

#### Column: analyte_reported Table: lk_analyte

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | immunology_symbol | immunology_symbol | immunology_symbol | 
|  | short_label | short_label | short_label | 
|  | analyte_reported | analyte_preferred | analyte_preferred | 


### Preferred Vocabulary Tables

#### lk_analyte

| lk_analyte | lk_analyte | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | analyte_preferred | immunology_symbol | official_gene_name | id | gene_symbol | description | short_label | link | 
|  | DATABASE COLUMNS | analyte_accession | immunology_symbol | official_gene_name | gene_id | gene_symbol | protein_ontology_name | protein_ontology_short_label | link | 


