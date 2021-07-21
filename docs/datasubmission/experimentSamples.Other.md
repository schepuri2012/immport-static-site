# Template: **other**

| Name | Value |
| --- | --- |
| Template Type | combined-multiple |
| Schema Version | 3.33 |
| Standard File Name | experimentSamples.Other.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Additional Result File Names | additional_result_file_names | Separate file names by a semi-colon (;). The file size name limit is 240 characters. | Please enter additional result file(s) to link to the experiment sample. The file size name limit is 240 characters. |
| Biosample Description | biosample_description | The biological sample description is used to describe details of the sample not captured in other columns. | The biological sample description is used to describe details of the sample not captured in other columns. |
| Biosample ID | biosample_id | The biological sample user defined ID is an identifier chosen by the data provider to refer to a sample. This ID may be referenced by other data records (e.g. experiment sample). The user defined ID is not shared. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. Please enter either a biological sample user defined ID or ImmPort accession. A single biological sample may be linked to an experiment sample. |
| Biosample Name | biosample_name | The biological sample name is a display name that is available when the data is shared, but it is not referenced by other data. | The biological sample name is an alternate identifier that is visible when the sample is shared. |
| Experiment Description | experiment_description | The experiment description is used to describe details of the experiment not captured in other columns. | The experiment description is used to describe details of the experiment not captured in other columns. |
| Experiment ID | experiment_id | The experiment identifier must be stored in ImmPort or in the experiments.txt template. The experiment serves as the parent entity to bind assay results of a similar type together. | Please enter either a experiment user defined ID or ImmPort accession. |
| Experiment Name | experiment_name | The experiment name is a display name that is available when the data is shared, but it is not referenced by other data. | The experiment name is an alternate identifier that is visible when the sample is shared. |
| Expsample Description | expsample_description | Describe important characteristics of the sample being assayed. | Describe important characteristics of the sample being assayed. |
| Expsample ID | expsample_id | The experiment sample user defined ID is an identifier chosen by the data provider to refer to this sample. This ID may be referenced by other data records (e.g. assay results). The user defined ID is not shared. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |
| Expsample Name | expsample_name | The experiment sample name is a display name that is available when the data is shared, but it is not referenced by other data records. | The experiment sample name is an alternate identifier that is visible when the experiment sample is shared. |
| Result File Name | global.result_file_name | Enter the file name for this assay result. The file size name limit is 240 characters. | Enter the file name for this assay result. The file size name limit is 240 characters. |
| Measurement Technique | measurement_technique | The measurement technique describes the assay method. | Choose from a drop down list. |
| Planned Visit ID | planned_visit_id | The link to a study's planned visit provides temporal context for a sample's derivation from a subject. | Please enter either a study's planned visit user defined ID or ImmPort accession. |
| Protocol ID(s) | protocol_ids | Please enter either a protocol user defined ID or ImmPort accession for a protocol that describes how the sample was derived and prepared. One or more identifiers can be entered per sample. Separate identifiers by semicolon (;). | Please enter either a protocol user defined ID or ImmPort accession. This column is required when either the experiment or biological sample are new. |
| Reagent ID(s) | reagent_ids | One or more identifiers can be entered. Separate identifiers by semicolon (;). The reagent identifier(s) must be stored in ImmPort or in the reagents.txt template. | Please enter either an assay reagent user defined ID or ImmPort accession. |
| Study ID | study_id | An experiment and biological sample may be linked to a single study. | Please enter either a study user defined ID or ImmPort accession. This column is only required when both the experiment and biological sample are new. |
| Study Time Collected | study_time_collected | Study time collected describes the time value for when a sample was derived from a subject. | Please enter a number. |
| Study Time Collected Unit | study_time_collected_unit | The time units are standard terms recommended by the HIPC Standards group. | Please choose from the drop down list. |
| Study Time T0 Event | study_time_t0_event | The time zero event refers to the study milestone upon which time is based. | Please choose from the drop down list. |
| Study Time T0 Event Specify | study_time_t0_event_specify | Enter a time zero event if 'Other' is selected in column 'Study Time T0 Event'. | Enter a time zero event if 'Other' is selected in column 'Study Time T0 Event'. |
| Subject ID | subject_id | Please enter either a subject user defined ID or ImmPort accession for the subject from which the sample was derived. A single subject record is permitted. | Please enter either a subject user defined ID or ImmPort accession for the subject from which the sample was derived. |
| Subtype | subtype | Enter a sample type that is of finer resolution than the standard sample types provided. If the 'Biological Sample Type' is 'Other', then the sample subtype must be entered. | Enter a sample type that is of finer resolution than the standard sample types provided. If the 'Biological Sample Type' is 'Other', then the sample subtype must be entered. |
| Treatment ID(s) | treatment_ids | One or more identifiers can be entered. Separate identifiers by semicolon (;). The treatment identifier(s) must be stored in ImmPort or in the treatments.txt template. | Please enter either a treatment user defined ID or ImmPort accession. |
| Type | type | The sample types are adopted from Uberon, Cell and CHEBI ontologies. | Please choose from the drop down list. |


### Combined Data

The ID Meta Data Columns include the ID columns that are referenced by more than one entity in the experiment sample template (for example, experiments and biological samples reference study IDs). The value entered the study ID is linked to experiment and biological sample.  The experiment sample ID is the primary ID and can be defined only once and not re-used.  The biological sample ID and experiment ID can be pre-defined or defined once and re-used within the template.

| ID Columns | PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| expsample_required | determine-combined-status | - | [expsample_id, expsample] | [expsample_required, expsample_user_defined_id, expsample_accession] | - | - | - | 
| biosample_required | determine-combined-status | - | [biosample_id, biosample] | [biosample_required, biosample_user_defined_id, biosample_accession] | - | - | - | 
| experiment_required | determine-combined-status | - | [experiment_id, experiment] | [experiment_required, experiment_user_defined_id, experiment_accession] | - | - | - | 

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| expsample_user_defined_id | USER_DEFINED_ID | expsample_accession | ES | expsample_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| biosample_user_defined_id | ANCILLARY | biosample | getAvailableUserDefinedIdsMap | biosample_accession | BS | biosample_seq | 
| experiment_user_defined_id | ANCILLARY | experiment | getAvailableUserDefinedIdsMap | experiment_accession | EXP | experiment_seq | 
| expsample_user_defined_id | PRIMARY | expsample | getAvailableUserDefinedIdsMap | expsample_accession | ES | expsample_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| additional_result_file_info_ids | - | - | - | - | - | - | yes | - | - | - | 
| additional_result_file_names | - | - | - | - | - | - | yes | - | - | - | 
| biosample_description | - | - | - | - | - | - | - | - | - | - | 
| biosample_id | yes | - | - | - | - | - | - | - | - | - | 
| biosample_name | - | - | - | - | - | - | - | - | - | - | 
| experiment_description | - | - | - | - | - | - | - | - | - | - | 
| experiment_id | yes | - | - | - | - | - | - | - | - | - | 
| experiment_name | - | yes | - | - | - | - | - | - | - | - | 
| expsample_description | - | - | - | - | - | - | - | - | - | - | 
| expsample_id | yes | - | - | - | - | - | - | - | - | - | 
| expsample_name | - | - | - | - | - | - | - | - | - | - | 
| expsample_result_schema | - | - | lk_expsample_result_schema | - | - | - | - | - | - | - | 
| file_info_ids | - | - | - | - | - | - | yes | - | - | - | 
| global.determine_file_preferred_info | - | - | - | - | - | yes | - | - | - | - | 
| global.immport_template | - | - | lk_yes_no | - | - | yes | - | - | - | - | 
| global.result_file_name | - | yes | - | - | - | yes | - | - | - | - | 
| global.resultfile_name | - | - | - | - | - | yes | - | - | - | - | 
| global.save_result_file_name | - | - | - | - | - | yes | - | yes | - | Yes | 
| global.use_immport_template | - | - | - | - | - | yes | - | yes | - | No | 
| measurement_technique | - | yes | lk_exp_measurement_tech | - | - | - | - | - | - | - | 
| planned_visit_id | - | yes | - | - | - | - | - | - | - | - | 
| protocol_accessions | - | - | - | - | - | - | yes | - | - | - | 
| protocol_ids | - | yes | - | - | - | - | yes | - | - | - | 
| reagent_accessions | - | - | - | - | - | - | yes | - | - | - | 
| reagent_ids | - | yes | - | - | - | - | yes | - | - | - | 
| result_schemas | - | - | - | - | - | - | yes | - | - | - | 
| study_id | - | yes | - | - | - | - | - | - | - | - | 
| study_time_collected | - | yes | - | - | - | - | - | - | float | - | 
| study_time_collected_unit | - | yes | lk_time_unit | - | - | - | - | - | - | - | 
| study_time_t0_event | - | yes | lk_t0_event | - | - | - | - | - | - | - | 
| study_time_t0_event_specify | - | yes | - | - | - | - | - | - | - | - | 
| subject_id | - | yes | - | - | - | - | - | - | - | - | 
| subtype | - | yes | - | - | - | - | - | - | - | - | 
| treatment_accessions | - | - | - | - | - | - | yes | - | - | - | 
| treatment_ids | - | yes | - | - | - | - | yes | - | - | - | 
| type | - | yes | lk_sample_type | - | - | - | - | - | - | - | 
| upload_result_status | - | - | - | - | - | - | - | yes | - | Not_Parsed | 

### Conditional Required Columns
| Column Name | CONDITION NAME | DATA ROW COLUMN | VALUE | 
|  --- | --- | --- | --- |
| study_id | case-insensitive-equals | biosample_required | 'Yes' | 
| study_id | case-insensitive-equals | experiment_required | 'Yes' | 
| study_time_t0_event_specify | case-insensitive-equals | biosample_required | 'Yes' | 
| study_time_t0_event_specify | case-insensitive-equals | study_time_t0_event | 'other' | 
| planned_visit_id | case-insensitive-equals | biosample_required | 'Yes' | 
| type | case-insensitive-equals | biosample_required | 'Yes' | 
| subtype | case-insensitive-equals | biosample_required | 'Yes' | 
| subtype | case-insensitive-equals | type | 'other' | 
| study_time_collected | case-insensitive-equals | biosample_required | 'Yes' | 
| study_time_collected_unit | case-insensitive-equals | biosample_required | 'Yes' | 
| subject_id | case-insensitive-equals | biosample_required | 'Yes' | 
| study_time_t0_event | case-insensitive-equals | biosample_required | 'Yes' | 
| protocol_ids | case-insensitive-equals | experiment_required | 'Yes' | 
| measurement_technique | case-insensitive-equals | experiment_required | 'Yes' | 
| experiment_name | case-insensitive-equals | experiment_required | 'Yes' | 
| reagent_ids | case-insensitive-equals | expsample_required | 'Yes' | 
| treatment_ids | case-insensitive-equals | expsample_required | 'Yes' | 
| global.result_file_name | case-insensitive-equals | expsample_required | 'Yes' | 

### Foreign Key Information
FOREIGN KEY TYPE:	user-defined-id	Input column is a User Defined ID and the Output column is the Accession associated with User Defined ID in the given table if the input is a user defined ID

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | planned_visit_id | planned_visit_accession | planned_visit | getAvailableUserDefinedIdsMap | 

FOREIGN KEY TYPE:	accession	Input column is an Accession and the Output column is the Accession in the given table if the input is defined and an accession

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | planned_visit_id | planned_visit_accession | planned_visit | getAvailableAccsToParentMap | 

FOREIGN KEY TYPE:	accession-to-accession	Input column is an Accession and Output column is the parent Accession associated with the Accession in given table if the input column is defined and an accession

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | planned_visit_accession | planned_visit_study_accession | planned_visit | getAvailableAccsToParentMap | 

### File Info Information

| FILE NAME COLUMN | FILE TYPE | STUDY ACCESSION COLUMN | 
|  --- | --- | --- |
| additional_result_file_names | additional | study_accession | 
| final.resultfile_name | result | study_accession | 

### Upload Table Information

Table: biosample    Type: ancillary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| biosample_accession | varchar | 15 | - | - | - | - | - | 
| description | varchar | 4000 | yes | - | - | biosample_description | - | 
| name | varchar | 200 | yes | - | - | biosample_name | - | 
| planned_visit_accession | varchar | 15 | - | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | - | - | 
| study_time_collected | float | - | - | - | - | - | - | 
| study_time_collected_unit | varchar | 25 | - | - | - | - | - | 
| study_time_t0_event | varchar | 50 | - | - | - | - | - | 
| study_time_t0_event_specify | varchar | 50 | yes | - | - | - | - | 
| subject_accession | varchar | 15 | - | - | - | - | - | 
| subtype | varchar | 50 | yes | - | - | - | - | 
| type | varchar | 50 | - | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | biosample_user_defined_id | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: experiment    Type: ancillary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| description | varchar | 4000 | yes | - | - | experiment_description | - | 
| experiment_accession | varchar | 15 | - | - | - | - | - | 
| measurement_technique | varchar | 50 | - | - | - | - | - | 
| name | varchar | 500 | yes | - | - | experiment_name | - | 
| study_accession | varchar | 15 | - | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | experiment_user_defined_id | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: expsample    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| description | varchar | 4000 | yes | - | - | expsample_description | - | 
| experiment_accession | varchar | 15 | - | - | - | - | - | 
| expsample_accession | varchar | 15 | - | - | - | - | - | 
| name | varchar | 200 | yes | - | - | expsample_name | - | 
| result_schema | varchar | 50 | - | - | - | expsample_result_schema | - | 
| upload_result_status | varchar | 20 | - | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | expsample_user_defined_id | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: experiment_2_protocol    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| experiment_accession | varchar | 15 | - | - | - | - | - | 
| protocol_accession | varchar | 15 | - | - | - | protocol_accessions | yes | 

Table: expsample_2_biosample    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| biosample_accession | varchar | 15 | - | - | - | - | - | 
| expsample_accession | varchar | 15 | - | - | - | new_expsample_accession | yes | 

Table: expsample_2_file_info    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| expsample_accession | varchar | 15 | - | - | - | - | - | 
| file_info_id | integer | - | - | - | - | file_info_ids | yes | 
| result_schema | varchar | 50 | - | - | - | result_schemas | yes | 

Table: expsample_2_reagent    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| expsample_accession | varchar | 15 | - | - | - | - | - | 
| reagent_accession | varchar | 15 | - | - | - | reagent_accessions | yes | 

Table: expsample_2_treatment    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| expsample_accession | varchar | 15 | - | - | - | - | - | 
| treatment_accession | varchar | 15 | - | - | - | treatment_accessions | yes | 

Table: workspace_2_biosample    Type: workspace

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| biosample_accession | varchar | 15 | - | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: workspace_2_experiment    Type: workspace

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| experiment_accession | varchar | 15 | - | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: workspace_2_expsample    Type: workspace

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| expsample_accession | varchar | 15 | - | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PreRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | check-immport-template | Provided Below | ['global.immport_template', 'global.result_file_name'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		case-insensitive-equals	expsample_required	'Yes'
		case-insensitive-equals	global.use_immport_template	'Yes'

### PostRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | check-not-contains-case-insensitive | Provided Below | ['final.resultfile_name', 'additional_result_file_names'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		case-insensitive-equals	expsample_required	'Yes'
		case-insensitive-equals	global.save_result_file_name	'Yes'

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | values-not-equal | Provided Below | ['For an existing biological sample and experiment, the experiment sample must be new.', 'biosample_required', 'expsample_required'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		case-insensitive-equals	biosample_required	'No'
		case-insensitive-equals	experiment_required	'No'

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | values-equal | Provided Below | ['A new biological sample is inconsistent with an existing experiment sample.', 'biosample_required', 'expsample_required'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		case-insensitive-equals	biosample_required	'Yes'

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | values-equal | Provided Below | ['A new experiment is inconsistent with an existing experiment sample.', 'experiment_required', 'expsample_required'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		case-insensitive-equals	experiment_required	'Yes'

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | values-equal | Provided Below | ['The study_accession for the biological sample is not the same as for the experiment', 'experiment_study_accession', 'biosample_study_accession'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		case-insensitive-equals	biosample_required	'No'
		case-insensitive-equals	experiment_required	'No'

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | LIST INPUT COLUMNS | LIST TABLE NAME | LIST VALIDATION QUERY NAME | 
|  --- | --- | --- | --- | --- | --- | --- |
| list type | check-value-in-entity | Provided Below | ['study_accession', 'subject_accession', 'biosample'] | [subject_accession] | arm_or_cohort | getStudiesForSubjectAccNum | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		case-insensitive-equals	biosample_required	'Yes'

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | values-equal | Provided Below | ['The study_accession for the biological sample is not the same as for the planned visit', 'study_accession', 'planned_visit_study_accession'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		case-insensitive-equals	biosample_required	'Yes'

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | check-result-schema-for-result-file | Provided Below | ['final.resultfile_name', 'expsample_result_schema'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		case-insensitive-equals	expsample_required	'Yes'
		case-insensitive-equals	global.save_result_file_name	'Yes'

### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-resultfile-name | Provided Below | [global.immport_template, global.result_file_name] | [global.resultfile_name] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	expsample_required	'Yes'
	case-insensitive-equals	global.use_immport_template	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [global.result_file_name] | [global.resultfile_name] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	expsample_required	'Yes'
	case-insensitive-equals	global.use_immport_template	'No'
	case-insensitive-equals	global.save_result_file_name	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [global.resultfile_name] | [final.resultfile_name] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	expsample_required	'Yes'
	case-insensitive-equals	global.save_result_file_name	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-case-insensitive-list | Provided Below | [additional_result_file_names] | [additional_result_file_names] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	expsample_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| initialize-columns | Provided Below | [] | [biosample_description, biosample_name, planned_visit_id, study_id, study_time_collected, study_time_collected_unit, study_time_t0_event, study_time_t0_event_specify, subject_id, subtype, type] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	biosample_required	'No'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| initialize-columns | Provided Below | [] | [experiment_description, experiment_name, measurement_technique, protocol_ids, study_id] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	experiment_required	'No'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| initialize-columns | Provided Below | [] | [additional_result_file_names, expsample_description, expsample_name, reagent_ids, treatment_ids] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	expsample_required	'No'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-parent-accession | Provided Below | [biosample_accession, biosample, accession-to-accession] | [biosample_study_accession] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	biosample_required	'No'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [biosample_study_accession] | [study_accession] | - | - | Yes | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	biosample_required	'No'
	case-insensitive-equals	experiment_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-parent-accession | Provided Below | [experiment_accession, experiment, accession-to-accession] | [experiment_study_accession] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	experiment_required	'No'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [experiment_study_accession] | [study_accession] | - | - | Yes | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	biosample_required	'Yes'
	case-insensitive-equals	experiment_required	'No'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [experiment_study_accession] | [study_accession] | - | - | Yes | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	biosample_required	'No'
	case-insensitive-equals	experiment_required	'No'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| get-result-schema | - | [global.immport_template] | [expsample_result_schema] | - | - | - | 


### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-result-schema | Provided Below | [expsample, expsample_accession, expsample_result_schema] | [] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	expsample_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [expsample_accession] | [new_expsample_accession] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	expsample_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-child-to-parent-accession | Provided Below | [biosample, accession-to-accession, getAvailableAccsToParentMap, biosample_accession, study_accession] | [] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	biosample_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-child-to-parent-accession | Provided Below | [experiment, accession-to-accession, getAvailableAccsToParentMap, experiment_accession, study_accession] | [] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	experiment_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-child-to-parent-accession | Provided Below | [expsample, accession-to-accession, getAvailableAccsToParentMap, expsample_accession, experiment_accession] | [] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	expsample_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-child-to-parent-accession | Provided Below | [expsample_2_biosample, accession-to-accession, getAvailableAccsToParentMap, expsample_accession, biosample_accession] | [] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	expsample_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-file-info-ids | Provided Below | [global.resultfile_name] | [resultfile_name_file_info_id] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	expsample_required	'Yes'
	case-insensitive-equals	global.save_result_file_name	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-file-info-ids | Provided Below | [additional_result_file_names] | [additional_result_file_info_ids] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	expsample_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-all-accessions-from-set | Provided Below | [reagent_accessions, getAccNumsForReagentSet, reagent_set_2_reagent] | [reagent_accessions] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	expsample_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-file-info | Provided Below | [final.resultfile_name, result] | [result_schema] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	expsample_required	'Yes'
	case-insensitive-equals	global.save_result_file_name	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-file-info | Provided Below | [additional_result_file_names, additional] | [result_schemas] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	expsample_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-accession-to-file-info | Provided Below | [expsample_accession, resultfile_name_file_info_id] | [] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	expsample_required	'Yes'
	case-insensitive-equals	global.save_result_file_name	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-accession-to-file-info | Provided Below | [expsample_accession, additional_result_file_info_ids] | [] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	expsample_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-data-to-lists | Provided Below | [additional_result_file_info_ids] | [file_info_ids] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	expsample_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-data-to-lists | Provided Below | [resultfile_name_file_info_id, result_schema] | [file_info_ids, result_schemas] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	expsample_required	'Yes'
	case-insensitive-equals	global.save_result_file_name	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| get-taxonomy-id | Provided Below | [subject, subject_accession] | [taxonomy_id] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	biosample_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-entity-to-taxonomy-id | Provided Below | [biosample, biosample_user_defined_id, biosample_accession, taxonomy_id] | [] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	biosample_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| get-taxonomy-id | Provided Below | [biosample, biosample_accession] | [taxonomy_id] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	expsample_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-entity-to-taxonomy-id | Provided Below | [expsample, expsample_user_defined_id, expsample_accession, taxonomy_id] | [] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	expsample_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-fcs-file-preferred-info | Provided Below | [expsample_accession, pnn_reported_list, pns_reported_list] | [panel_preferred, pnn_preferred_list, pns_preferred_list] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	not-empty-value	global.determine_file_preferred_info	-
	file-exists	global.result_file_name	-

### Controlled Vocabularies
| lk_exp_measurement_tech | lk_exp_measurement_tech | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 
| lk_expsample_result_schema | lk_expsample_result_schema | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | 
|  | DATABASE COLUMNS | name | description | 
| lk_sample_type | lk_sample_type | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 
| lk_t0_event | lk_t0_event | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 
| lk_time_unit | lk_time_unit | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 
| lk_yes_no | - | static | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | 
|  | DATABASE COLUMNS | name | description | 
	DATA VALUES	No	No
		Yes	Yes

