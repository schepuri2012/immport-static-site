# Template: **biosamples**

| Name | Value |
| --- | --- |
| Template Type | single |
| Schema Version | 3.33 |
| Standard File Name | bioSamples.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Description | description | The biological sample description is used to describe details of the sample not captured in other columns. | The biological sample description is used to describe details of the sample not captured in other columns. |
| Name | name | The biological sample name is not referenced by other data records. | The biological sample name is an alternate identifier that is visible when the sample is shared. |
| Planned Visit ID | planned_visit_id | The link to a study's planned visit provides temporal context for a sample's derivation from a subject. | Please enter either a study's planned visit user defined ID or ImmPort accession. |
| Study ID | study_id | A biological sample may be linked to a single study. | Please enter either a study user defined ID or ImmPort accession. |
| Study Time Collected | study_time_collected | Study time collected describes the time value for when a sample was derived from a subject. | Please enter a number. |
| Study Time Collected Unit | study_time_collected_unit | The time units are standard terms recommended by the HIPC Standards group. | Please choose from the drop down list. |
| Study Time T0 Event | study_time_t0_event | The time zero event refers to the study milestone upon which time is based. | Please choose from the drop down list. |
| Study Time T0 Event Specify | study_time_t0_event_specify | Enter a time zero event if 'Other' is selected in column 'Study Time T0 Event'. | Enter a time zero event if 'Other' is selected in column 'Study Time T0 Event'. |
| Subject ID | subject_id | Please enter either a subject user defined ID or ImmPort accession for the subject from which the sample was derived. A single subject record is permitted. | Please enter either a subject user defined ID or ImmPort accession for the subject from which the sample was derived. |
| Subtype | subtype | Enter a sample type that is of finer resolution than the standard sample types provided. If the 'Biological Sample Type' is 'Other', then the sample subtype must be entered. | Enter a sample type that is of finer resolution than the standard sample types provided. If the 'Biological Sample Type' is 'Other', then the sample subtype must be entered. |
| Treatment ID(s) | treatment_ids | Please enter either a treatment user defined ID or ImmPort accession if the sample was manipulated in a manner significant to the assay prior to the assay being conducted. One or more identifiers can be entered per sample. Separate identifiers by semicolon (;). | Please enter either a treatment user defined ID or ImmPort accession. |
| Type | type | The sample types are adopted from Uberon, Cell and CHEBI ontologies. | Please choose from the drop down list. |
| User Defined ID | user_defined_id | The biological sample user defined ID is an identifier chosen by the data provider to refer to a sample. This ID may be referenced by other data records (e.g. experiment sample). The user defined ID is not shared. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| user_defined_id | USER_DEFINED_ID | biosample_accession | BS | biosample_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| user_defined_id | PRIMARY | biosample | getAvailableUserDefinedIdsMap | biosample_accession | BS | biosample_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| description | - | - | - | - | - | - | - | - | - | - | 
| name | - | - | - | - | - | - | - | - | - | - | 
| planned_visit_id | yes | - | - | - | - | - | - | - | - | - | 
| study_id | yes | - | - | - | - | - | - | - | - | - | 
| study_time_collected | yes | - | - | - | - | - | - | - | float | - | 
| study_time_collected_unit | yes | - | lk_time_unit | - | - | - | - | - | - | - | 
| study_time_t0_event | yes | - | lk_t0_event | - | - | - | - | - | - | - | 
| study_time_t0_event_specify | - | yes | - | - | - | - | - | - | - | - | 
| subject_id | yes | - | - | - | - | - | - | - | - | - | 
| subtype | - | yes | - | - | - | - | - | - | - | - | 
| treatment_accessions | - | - | - | - | - | - | yes | - | - | - | 
| treatment_ids | - | - | - | - | - | - | yes | - | - | - | 
| type | yes | - | lk_sample_type | - | - | - | - | - | - | - | 
| user_defined_id | yes | - | - | - | - | - | - | - | - | - | 

### Conditional Required Columns
| Column Name | CONDITION NAME | DATA ROW COLUMN | VALUE | 
|  --- | --- | --- | --- |
| study_time_t0_event_specify | case-insensitive-equals | study_time_t0_event | 'other' | 
| subtype | case-insensitive-equals | type | 'other' | 

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
| user_defined_id | varchar | 100 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: biosample_2_treatment    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| biosample_accession | varchar | 15 | - | - | - | - | - | 
| treatment_accession | varchar | 15 | - | - | - | treatment_accessions | yes | 

Table: workspace_2_biosample    Type: workspace

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| biosample_accession | varchar | 15 | - | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PostRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | LIST INPUT COLUMNS | LIST TABLE NAME | LIST VALIDATION QUERY NAME | 
|  --- | --- | --- | --- | --- | --- | --- |
| list type | check-value-in-entity | - | ['study_accession', 'subject_accession', 'biosample'] | [subject_accession] | arm_or_cohort | getStudiesForSubjectAccNum | 


| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | values-equal | - | ['The study_accession for the biological sample is not same as for the planned visit', 'study_accession', 'planned_visit_study_accession'] | 


### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-child-to-parent-accession | - | [biosample, accession-to-accession, getAvailableAccsToParentMap, biosample_accession, study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| get-taxonomy-id | - | [subject, subject_accession] | [taxonomy_id] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-entity-to-taxonomy-id | - | [biosample, user_defined_id, biosample_accession, taxonomy_id] | [] | - | - | - | 


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

