# Template: **labtests**

| Name | Value |
| --- | --- |
| Template Type | combined-result |
| Schema Version | 3.33 |
| Standard File Name | labTests.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Biosample ID | biosample_id | The biological sample user defined ID is an identifier chosen by the data provider to refer to a sample. This ID may be referenced by other data records (e.g. experiment sample). The user defined ID is not shared. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. Please enter either a biological sample user defined ID or ImmPort accession. A single biological sample may be linked to a lab test. |
| Description | description | The biological sample description is used to describe details of the sample not captured in other columns. | The biological sample description is used to describe details of the sample not captured in other columns. |
| Lab Test Panel ID | lab_test_panel_id | The lab test panel user defined ID is an identifier chosen by the data provider to refer to lab panel. This ID may be referenced by other data records (e.g. lab test). The user defined ID is not shared. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |
| Name | name | The biological sample name is not referenced by other data records. | The biological sample name is an alternate identifier that is visible when the sample is shared. |
| Name Reported | name_reported | The lab panel name describe lab test panel. Please select a lab panel name from the list provided if the name matches your name or enter a name if there is not an appropriate one provided. This name is visible when the panel is shared. | The lab panel name describes the lab test panel. Please select a lab panel name from the list provided if the name matches your name or enter a name if there is not an appropriate one provided. This name is visible when the panel is shared. |
| Planned Visit ID | planned_visit_id | The link to a study's planned visit provides temporal context for a sample's derivation from a subject. | Please enter either a study's planned visit user defined ID or ImmPort accession. |
| Protocol ID(s) | protocol_ids | Please enter either a protocol user defined ID or ImmPort accession. One or more identifiers can be entered per subject. Separate identifiers by semicolon (;). | Please enter either a protocol user defined ID or ImmPort accession. The Protocol ID(s) is required when either the lab test panel or the biological sample are new. |
| Result Separator Column | result_separator_column | This pseudo column separates meta data from results. | This pseudo column separates the results (lab tests) from the lab test panel meta data. It must always appear and be the column that appears immediately after the last meta-data column and before any result columns. |
| Study ID | study_id | A lab test panel may be linked to a single study. | Please enter a study user defined ID or ImmPort accession for the study in which the lab test panel occurs. The Study ID is only required when both the lab test panel and biological sample are new. |
| Study Time Collected | study_time_collected | Study time collected describes the time value for when a sample was derived from a subject. | Please enter a number. |
| Study Time Collected Unit | study_time_collected_unit | The time units are standard terms recommended by the HIPC Standards group. | Please choose from the drop down list. |
| Study Time T0 Event | study_time_t0_event | The time zero event refers to the study milestone upon which time is based. | Please choose from the drop down list. |
| Study Time T0 Event Specify | study_time_t0_event_specify | Enter a time zero event if 'Other' is selected in column 'Study Time T0 Event'. | Enter a time zero event if 'Other' is selected in column 'Study Time T0 Event'. |
| Subject ID | subject_id | Please enter either a subject user defined ID or ImmPort accession for the subject from which the sample was derived. A single subject record is permitted. | Please enter either a subject user defined ID or ImmPort accession for the subject from which the sample was derived. |
| Subtype | subtype | Enter a sample type that is of finer resolution than the standard sample types provided. If the 'Biological Sample Type' is 'Other', then the sample subtype must be entered. | Enter a sample type that is of finer resolution than the standard sample types provided. If the 'Biological Sample Type' is 'Other', then the sample subtype must be entered. |
| Type | type | The sample types are adopted from Uberon, Cell and CHEBI ontologies. | Please choose a biological sample type from the drop down list. |


### Combined Data

The ID Meta Data Columns include the ID columns that are referenced by more than one entity in the lab test template (for example, biological samples and lab test panels reference study IDs).  The biosample ID is the primary ID and can be pre-defined or defined once and not re-used. The lab test panel ID can be pre-defined or defined once and re-used within the template

| ID Columns | PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| biosample_required | determine-combined-status | - | [biosample_id, biosample] | [biosample_required, biosample_user_defined_id, biosample_accession] | - | - | - | 
| lab_test_panel_required | determine-combined-status | - | [lab_test_panel_id, lab_test_panel] | [lab_test_panel_required, lab_test_panel_user_defined_id, lab_test_panel_accession] | - | - | - | 

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| biosample_user_defined_id | USER_DEFINED_ID | biosample_accession | BS | biosample_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| lab_test_panel_user_defined_id | ANCILLARY | lab_test_panel | getAvailableUserDefinedIdsMap | lab_test_panel_accession | LP | lab_test_panel_seq | 
| biosample_user_defined_id | PRIMARY | biosample | getAvailableUserDefinedIdsMap | biosample_accession | BS | biosample_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| biosample_id | yes | - | - | - | - | - | - | - | - | - | 
| description | - | - | - | - | - | - | - | - | - | - | 
| lab_test_panel_id | yes | - | - | - | - | - | - | - | - | - | 
| lab_test_panel_protocol_accessions | - | - | - | - | - | - | yes | - | - | - | 
| name | - | - | - | - | - | - | - | - | - | - | 
| name_reported | - | yes | - | lk_lab_test_panel_name | name_preferred | - | - | - | - | - | 
| planned_visit_id | - | yes | - | - | - | - | - | - | - | - | 
| protocol_accessions | - | - | - | - | - | - | yes | - | - | - | 
| protocol_ids | - | yes | - | - | - | - | yes | - | - | - | 
| study_id | - | yes | - | - | - | - | - | - | - | - | 
| study_time_collected | - | yes | - | - | - | - | - | - | float | - | 
| study_time_collected_unit | - | yes | lk_time_unit | - | - | - | - | - | - | - | 
| study_time_t0_event | - | yes | lk_t0_event | - | - | - | - | - | - | - | 
| study_time_t0_event_specify | - | yes | - | - | - | - | - | - | - | - | 
| subject_id | - | yes | - | - | - | - | - | - | - | - | 
| subtype | - | yes | - | - | - | - | - | - | - | - | 
| type | - | yes | lk_sample_type | - | - | - | - | - | - | - | 

### Conditional Required Columns
| Column Name | CONDITION NAME | DATA ROW COLUMN | VALUE | 
|  --- | --- | --- | --- |
| study_id | case-insensitive-equals | biosample_required | 'Yes' | 
| study_id | case-insensitive-equals | lab_test_panel_required | 'Yes' | 
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
| name_reported | case-insensitive-equals | lab_test_panel_required | 'Yes' | 
| protocol_ids | case-insensitive-equals | lab_test_panel_required | 'Yes' | 

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

### Upload Table Information

Table: lab_test_panel    Type: ancillary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| lab_test_panel_accession | varchar | 15 | - | - | - | - | - | 
| name_preferred | varchar | 125 | - | - | - | - | - | 
| name_reported | varchar | 125 | yes | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | lab_test_panel_user_defined_id | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: biosample    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| biosample_accession | varchar | 15 | - | - | - | - | - | 
| description | varchar | 4000 | yes | - | - | - | - | 
| name | varchar | 200 | yes | - | - | - | - | 
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

Table: lab_test_panel_2_protocol    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| lab_test_panel_accession | varchar | 15 | - | - | - | - | - | 
| protocol_accession | varchar | 15 | - | - | - | lab_test_panel_protocol_accessions | yes | 

Table: workspace_2_biosample    Type: workspace

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| biosample_accession | varchar | 15 | - | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: workspace_2_lab_test_panel    Type: workspace

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| lab_test_panel_accession | varchar | 15 | - | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PostRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | values-equal | Provided Below | ['The study_accession for the biological sample is not same as for the lab test panel', 'lab_test_panel_study_accession', 'biosample_study_accession'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		case-insensitive-equals	biosample_required	'No'
		case-insensitive-equals	lab_test_panel_required	'No'

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | LIST INPUT COLUMNS | LIST TABLE NAME | LIST VALIDATION QUERY NAME | 
|  --- | --- | --- | --- | --- | --- | --- |
| list type | check-value-in-entity | Provided Below | ['study_accession', 'subject_accession', 'biosample'] | [subject_accession] | arm_or_cohort | getStudiesForSubjectAccNum | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		case-insensitive-equals	biosample_required	'Yes'

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | values-equal | Provided Below | ['The study_accession for the biological sample is not same as for the planned visit', 'study_accession', 'planned_visit_study_accession'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		case-insensitive-equals	biosample_required	'Yes'

### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| initialize-columns | Provided Below | [] | [name_reported, protocol_ids, study_id] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	lab_test_panel_required	'No'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| initialize-columns | Provided Below | [] | [study_id, type, subtype, name, description, subject_id, planned_visit_id, study_time_collected, study_time_collected_unit, study_time_t0_event, study_time_t0_event_specify] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	biosample_required	'No'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-parent-accession | Provided Below | [biosample_accession, biosample, accession-to-accession] | [biosample_study_accession] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	biosample_required	'No'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-parent-accession | Provided Below | [lab_test_panel_accession, lab_test_panel, accession-to-accession] | [lab_test_panel_study_accession] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	lab_test_panel_required	'No'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [lab_test_panel_study_accession] | [study_accession] | - | - | Yes | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	biosample_required	'Yes'
	case-insensitive-equals	lab_test_panel_required	'No'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [biosample_study_accession] | [study_accession] | - | - | Yes | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	biosample_required	'No'
	case-insensitive-equals	lab_test_panel_required	'Yes'

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-child-to-parent-accession | Provided Below | [lab_test_panel, accession-to-accession, getAvailableAccsToParentMap, lab_test_panel_accession, study_accession] | [] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	lab_test_panel_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-child-to-parent-accession | Provided Below | [biosample, accession-to-accession, getAvailableAccsToParentMap, biosample_accession, study_accession] | [] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	biosample_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| copy-lists | Provided Below | [protocol_accessions] | [lab_test_panel_protocol_accessions] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	lab_test_panel_required	'Yes'

### Controlled Vocabularies
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
### Preferred Vocabularies

#### Column: name_reported Table: lk_lab_test_panel_name

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | name_reported | name_preferred | name_preferred | 


### Preferred Vocabulary Tables

#### lk_lab_test_panel_name

| lk_lab_test_panel_name | lk_lab_test_panel_name | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name_preferred | description | link | 
|  | DATABASE COLUMNS | name | description | link | 


***
## Combined Result Template: **labtests**

| Name | Value |
| --- | --- |
| Template Type | combined-result |
| Schema Version | 3.33 |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Name Reported | name_reported | The lab test name describes lab test. Please select a lab test name from the list provided if the name matches your name or enter a name if there is not an appropriate one provided. This name is visible when the panel is shared. | Please select a lab test name from the list provided if the name matches your name or enter a name if there is not an appropriate one provided. |
| Result Unit Reported | result_unit_reported | The lab test result unit describes the unit for the lab test value. | The lab test result unit describes the unit for the lab test value. |
| Result Value Reported | result_value_reported | The lab test result captures the assayed value for a sample and can include letters, numbers and greater than or less than symbols. | The lab test result captures the assayed value. |
| User Defined ID | user_defined_id | The lab test user defined ID is an identifier chosen by the data provider to refer the lab test. The user defined ID is not shared. | The lab test identifier should be unique to the ImmPort workspace to which the data will be uploaded. This COLUMN must appear as the FIRST COLUMN for a repeating result column group. |

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
| name_reported | yes | - | - | lk_lab_test_name | name_preferred | - | - | - | - | - | 
| result_unit_reported | yes | - | - | lk_unit_of_measure | result_unit_preferred | - | - | - | - | - | 
| result_value_preferred | - | - | - | - | - | - | - | - | float | - | 
| result_value_reported | yes | - | - | - | - | - | - | - | - | - | 
| user_defined_id | yes | - | - | - | - | - | - | - | - | - | 

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

### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| convert-to-float | - | [result_value_reported] | [result_value_preferred] | - | - | - | 


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


