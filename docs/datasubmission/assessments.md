# Template: **assessments**

| Name | Value |
| --- | --- |
| Template Type | combined-result |
| Schema Version | 3.33 |
| Standard File Name | assessments.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Assessment Panel ID | assessment_panel_id | The assessment panel user defined ID is an identifier chosen by the data provider to refer to a set of assessments, often organized into a Case Report Form. This ID may be referenced by other data records (e.g. assessment). The user defined ID is not shared | Please enter either an assessment panel user defined ID or ImmPort accession. |
| Assessment Type | assessment_type | The assessment type is not a constrained list of terms and suggested values include Physical Exam, Questionnaire, Medical History, Family History. | Suggested values include Physical Exam, Questionnaire, Medical History, Family History. |
| CRF File Names | crf_filenames | Separate file names by a semi-colon (;). The file size name limit is 240 characters. | Please enter CRF file(s) to link to the assessment panel. Separate file names by a semi-colon (;). The file size name limit is 240 characters. |
| Name Reported | name_reported | The assessment panel name is a display name that is available when the data is shared, but it is not referenced by other data. | The assessment panel name is an alternate identifier that is visible when the assessment panel is shared. |
| Result Separator Column | result_separator_column | This pseudo column separates meta data from results. | This pseudo column separates the results (assessment components) from the assessment panel meta data. It must always appear and be the column that appears immediately after the last meta-data column and before any result columns. |
| Status | status | The assessment status is not a constrained list of terms and suggested values include Completed, Partial, and Not Completed. | The assessment status is not a constrained list of terms and suggested values include Completed, Partial, and Not Completed. |
| Study ID | study_id | An assessment panel may be linked to a single study. | Please enter either a study user defined ID or ImmPort accession. This column is only required when both the assessment panel is new. |
| Subject ID | subject_id | Please enter either a subject user defined ID or ImmPort accession for the subject for the subject from which the assessment was completed. A single subject record is permitted. | Please enter either a subject user defined ID or ImmPort accession for the subject from which the assessment was completed. |


### Combined Data

The ID Meta Data Columns include the ID columns that are referenced by more than one entity in the assessment panel template (for example, assessment panels). The subject ID is the primary ID and must be pre-defined and used only once within the template.  The assessment panel ID can be pre-defined or defined once and re-used within the template

| ID Columns | PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| subject_required | determine-combined-status | - | [subject_id, subject] | [subject_required, subject_user_defined_id, subject_accession] | - | - | - | 
| assessment_panel_required | determine-combined-status | - | [assessment_panel_id, assessment_panel] | [assessment_panel_required, assessment_panel_user_defined_id, assessment_panel_accession] | - | - | - | 

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| subject_user_defined_id | USER_DEFINED_ID | subject_accession | SUB | subject_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| assessment_panel_user_defined_id | ANCILLARY | assessment_panel | getAvailableUserDefinedIdsMap | assessment_panel_accession | AP | assessment_panel_seq | 
| subject_user_defined_id | PRIMARY | subject | getAvailableUserDefinedIdsMap | subject_accession | SUB | subject_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| assessment_panel_id | yes | - | - | - | - | - | - | - | - | - | 
| assessment_type | - | - | - | - | - | - | - | - | - | - | 
| crf_filenames | - | - | - | - | - | - | yes | - | - | - | 
| file_info_ids | - | - | - | - | - | - | yes | - | - | - | 
| name_reported | - | yes | - | - | - | - | - | - | - | - | 
| result_schema | - | - | - | - | - | - | - | yes | - | OTHER | 
| result_schemas | - | - | - | - | - | - | yes | - | - | - | 
| status | - | - | - | - | - | - | - | - | - | - | 
| study_id | - | yes | - | - | - | - | - | - | - | - | 
| subject_id | yes | - | - | - | - | - | - | - | - | - | 
| subject_required_value | - | - | - | - | - | - | - | yes | - | no | 

### Conditional Required Columns
| Column Name | CONDITION NAME | DATA ROW COLUMN | VALUE | 
|  --- | --- | --- | --- |
| study_id | case-insensitive-equals | assessment_panel_required | 'Yes' | 
| name_reported | case-insensitive-equals | assessment_panel_required | 'Yes' | 

### Foreign Key Information
FOREIGN KEY TYPE:	user-defined-id	Input column is a User Defined ID and the Output column is the Accession associated with User Defined ID in the given table if the input is a user defined ID

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | study_id | study_accession | study | getAvailableUserDefinedIdsMap | 

FOREIGN KEY TYPE:	accession	Input column is an Accession and the Output column is the Accession in the given table if the input is defined and an accession

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | study_id | study_accession | study | getAvailableAccsToParentMap | 

### File Info Information

| FILE NAME COLUMN | FILE TYPE | STUDY ACCESSION COLUMN | 
|  --- | --- | --- |
| crf_filenames | additional | study_accession | 

### Upload Table Information

Table: assessment_panel    Type: ancillary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| assessment_panel_accession | varchar | 15 | - | - | - | - | - | 
| assessment_type | varchar | 125 | yes | - | - | - | - | 
| name_reported | varchar | 125 | yes | - | - | - | - | 
| result_schema | varchar | 50 | - | - | - | - | - | 
| status | varchar | 40 | yes | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | assessment_panel_user_defined_id | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: subject    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| description | varchar | 4000 | - | - | - | - | - | 
| ethnicity | varchar | 50 | - | - | - | - | - | 
| gender | varchar | 20 | - | - | - | - | - | 
| race | varchar | 50 | - | - | - | - | - | 
| race_specify | varchar | 1000 | - | - | - | - | - | 
| species | varchar | 50 | - | - | - | - | - | 
| strain | varchar | 50 | - | - | - | - | - | 
| strain_characteristics | varchar | 500 | - | - | - | - | - | 
| subject_accession | varchar | 15 | - | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | subject_user_defined_id   | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: assessment_2_file_info    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| assessment_panel_accession | varchar | 15 | - | - | - | - | - | 
| file_info_id | integer | - | - | - | - | file_info_ids | yes | 
| result_schema | varchar | 50 | - | - | - | result_schemas | yes | 

Table: workspace_2_assessment_panel    Type: workspace

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| assessment_panel_accession | varchar | 15 | - | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: workspace_2_subject    Type: workspace

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| subject_accession | varchar | 15 | - | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PostRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | values-equal | - | ['The subject ID must always be for a predefined subject', 'subject_required_value', 'subject_required'] | 


| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | LIST INPUT COLUMNS | LIST TABLE NAME | LIST VALIDATION QUERY NAME | 
|  --- | --- | --- | --- | --- | --- | --- |
| list type | check-value-in-entity | - | ['study_accession', 'subject_accession', 'assessment_component'] | [subject_accession] | arm_or_cohort | getStudiesForSubjectAccNum | 


### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| initialize-columns | Provided Below | [] | [name_reported, assessment_type, crf_filenames, status, study_id] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	assessment_panel_required	'No'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-parent-accession | Provided Below | [assessment_panel_accession, assessment_panel, accession-to-accession] | [study_accession] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	assessment_panel_required	'No'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-case-insensitive-list | Provided Below | [crf_filenames] | [crf_filenames] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	assessment_panel_required	'Yes'

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-child-to-parent-accession | Provided Below | [assessment_panel, accession-to-accession, getAvailableAccsToParentMap, assessment_panel_accession, study_accession] | [] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	assessment_panel_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-file-info-ids | Provided Below | [crf_filenames] | [file_info_ids] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	assessment_panel_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-file-info | Provided Below | [crf_filenames, additional] | [result_schemas] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	assessment_panel_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-accession-to-file-info | Provided Below | [assessment_panel_accession, file_info_ids] | [] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	assessment_panel_required	'Yes'

***
## Combined Result Template: **assessments**

| Name | Value |
| --- | --- |
| Template Type | combined-result |
| Schema Version | 3.33 |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Age At Onset Reported | age_at_onset_reported | Please indicate the age at which a condition reported in the assessment occurred.  This column is optional unless units (Age At Onset Unit Reported) is provided. | Please enter a number. |
| Age At Onset Unit Reported | age_at_onset_unit_reported | The time unit for the age of onset value.  This column is optional unless value (Age At Onset Reported) is provided. | Suggested values include Days, Months, Years. |
| Is Clinically Significant | is_clinically_significant | Is the condition reported in the assessment significant for the study analysis? | Please enter a 'Y' or 'N.' |
| Location Of Finding Reported | location_of_finding_reported | Please use SnoMED CT terms if possible. | Where on the subject's body does the condition reported in the assessment occur? |
| Name Reported | name_reported | The assessment component name is a display name that is available when the data is shared, but it is not referenced by other data. | The assessment component name is an alternate identifier that is visible when the sample is shared. |
| Organ Or Body System Reported | organ_or_body_system_reported | Please use SnoMED CT terms if possible. | What is the organ or body system affected by the condition reported in the assessment? |
| Planned Visit ID | planned_visit_id | The link to a study's planned visit provides temporal context for a subjects assessment during the course of a study. | Please enter either a study's planned visit user defined ID or ImmPort accession. |
| Result Unit Reported | result_unit_reported | The unit for the assessment value. | The unit for the assessment value. |
| Result Value Category | result_value_category | Suggested terms include Mild, Moderate, and Severe. | A categorical representation of the assessment value. |
| Result Value Reported | result_value_reported | The assessment component value is often the response to a question in a CRF. | The assessment component value is often the response to a question in a CRF. |
| Study Day | study_day | Study time collected describes the time value for when the assessment was completed. | Please enter a number. |
| Subject Position Reported | subject_position_reported | Suggested terms include prone, supine, seated, and standing. | The position the subject was in when the assessment was completed. |
| Time Of Day | time_of_day | There are no preferrred response values. | When during the day was the assessment completed. |
| User Defined ID | user_defined_id | The assessment component user defined ID is an identifier chosen by the data provider to refer to this assessment result. An assessment component is a portion of an assessment panel. The user defined ID is not shared. | The assessment component identifier should be unique to the ImmPort workspace to which the data will be uploaded. |
| Verbatim Question | verbatim_question | What is the wording of the question to elicit the assessment result? | What is the actual question in the CRF? |
| Who Is Assessed | who_is_assessed | Assessments can include study subject medical history and/or family history. | Is the study subject assessed or a member of the study subject's family? |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| user_defined_id | USER_DEFINED_ID | assessment_component_accession | AC | assessment_component_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| user_defined_id | PRIMARY | assessment_component | getAvailableUserDefinedIdsMap | assessment_component_accession | AC | assessment_component_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| age_at_onset_preferred | - | - | - | - | - | - | - | - | float | - | 
| age_at_onset_reported | - | yes | - | - | - | - | - | - | - | - | 
| age_at_onset_unit_reported | - | yes | - | lk_preferred_time_unit | age_at_onset_unit_preferred | - | - | - | - | - | 
| is_clinically_significant | - | - | - | - | - | - | - | - | - | - | 
| location_of_finding_reported | - | - | - | - | - | - | - | - | - | - | 
| name_reported | yes | - | - | - | - | - | - | - | - | - | 
| organ_or_body_system_reported | - | - | - | - | - | - | - | - | - | - | 
| planned_visit_id | yes | - | - | - | - | - | - | - | - | - | 
| result_unit_reported | - | - | - | lk_unit_of_measure | result_unit_preferred | - | - | - | - | - | 
| result_value_category | - | - | - | - | - | - | - | - | - | - | 
| result_value_preferred | - | - | - | - | - | - | - | - | float | - | 
| result_value_reported | - | - | - | - | - | - | - | - | - | - | 
| study_day | yes | - | - | - | - | - | - | - | float | - | 
| subject_position_reported | - | - | - | - | - | - | - | - | - | - | 
| time_of_day | - | - | - | - | - | - | - | - | - | - | 
| user_defined_id | yes | - | - | - | - | - | - | - | - | - | 
| verbatim_question | - | - | - | - | - | - | - | - | - | - | 
| who_is_assessed | - | - | - | - | - | - | - | - | - | - | 

### Conditional Required Columns
| Column Name | CONDITION NAME | DATA ROW COLUMN | VALUE | 
|  --- | --- | --- | --- |
| age_at_onset_reported | not-empty-value | age_at_onset_unit_reported | - | 
| age_at_onset_unit_reported | not-empty-value | age_at_onset_reported | - | 

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
|  | assessment_panel_accession | study_accession | assessment_panel | getAvailableAccsToParentMap | 

### Upload Table Information

Table: assessment_component    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| age_at_onset_preferred | float | - | - | - | - | - | - | 
| age_at_onset_reported | varchar | 100 | yes | - | - | - | - | 
| age_at_onset_unit_preferred | varchar | 40 | - | - | - | - | - | 
| age_at_onset_unit_reported | varchar | 25 | yes | - | - | - | - | 
| assessment_component_accession | varchar | 15 | - | - | - | - | - | 
| assessment_panel_accession | varchar | 15 | - | - | - | - | - | 
| is_clinically_significant | varchar | 1 | yes | - | - | - | - | 
| location_of_finding_reported | varchar | 256 | yes | - | - | - | - | 
| name_reported | varchar | 150 | yes | - | - | - | - | 
| organ_or_body_system_reported | varchar | 100 | yes | - | - | - | - | 
| planned_visit_accession | varchar | 15 | - | - | - | - | - | 
| result_unit_preferred | varchar | 40 | - | - | - | - | - | 
| result_unit_reported | varchar | 40 | yes | - | - | - | - | 
| result_value_category | varchar | 40 | yes | - | - | - | - | 
| result_value_preferred | float | - | - | - | - | - | - | 
| result_value_reported | varchar | 250 | yes | - | - | - | - | 
| study_day | float | - | - | - | - | - | - | 
| subject_accession | varchar | 15 | - | - | - | - | - | 
| subject_position_reported | varchar | 40 | yes | - | - | - | - | 
| time_of_day | varchar | 40 | yes | - | - | - | - | 
| user_defined_id | varchar | 200 | yes | - | - | - | - | 
| verbatim_question | varchar | 250 | yes | - | - | - | - | 
| who_is_assessed | varchar | 40 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PostRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | values-equal | - | ['The study_accession for the assessment component is not same as for the planned visit', 'study_accession', 'planned_visit_study_accession'] | 


### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| convert-to-float | - | [age_at_onset_reported] | [age_at_onset_preferred] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| convert-to-float | - | [result_value_reported] | [result_value_preferred] | - | - | - | 


### Preferred Vocabularies

#### Column: age_at_onset_unit_reported Table: lk_preferred_time_unit

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | age_at_onset_unit_reported | age_at_onset_unit_preferred | time_unit_preferred | 

#### Column: result_unit_reported Table: lk_unit_of_measure

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | result_unit_reported | result_unit_preferred | unit_of_measure_preferred | 


### Preferred Vocabulary Tables

#### lk_preferred_time_unit

| lk_preferred_time_unit | lk_time_unit | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | time_unit_preferred | description | link | 
|  | DATABASE COLUMNS | name | description | link | 

#### lk_unit_of_measure

| lk_unit_of_measure | lk_unit_of_measure | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | unit_of_measure_preferred | description | link | 
|  | DATABASE COLUMNS | name | description | link | 


