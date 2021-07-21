# Template: **interventions**

| Name | Value |
| --- | --- |
| Template Type | single |
| Schema Version | 3.33 |
| Standard File Name | interventions.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Compound Name Reported | compound_name_reported | The compound name describes what substance entered the subject. | The compound name describes what substance entered the subject. |
| Compound Role | compound_role | Compound role indicates the purpose or category of the substance. | Compound role indicates the purpose or category of the substance. |
| Dose | dose | The dose value. | The dose value. |
| Dose Freq Per Interval | dose_freq_per_interval | How often the substance was encountered. | How often the substance was encountered. |
| Dose Reported | dose_reported | The amount of a substance. | The amount of a substance. |
| Dose Units | dose_units | The dose unit. | The dose unit. |
| Duration | duration | Length of time for the encounter. | Length of time for the encounter. |
| Duration Unit | duration_unit | Time unit for the duration. | Time unit for the duration. |
| End Day | end_day | The study day in which the substance was encounter ended. | The study day in which the substance was encounter ended. |
| End Time | end_time | Time within a study day the substance encounter ended. | Time within a study day the substance encounter ended. |
| Formulation | formulation | The packaging or delivery of the substance. | The packaging or delivery of the substance. |
| Is Ongoing | is_ongoing | Is the substance encounter continuing. | Is the substance encounter continuing. |
| Name Reported | name_reported | The intervention name is not referenced by other data records. | The intervention name is an alternate identifier that is visible when the sample is shared. |
| Reported Indication | reported_indication | The purpose the substance was encountered. | The purpose the substance was encountered. |
| Route Of Admin Reported | route_of_admin_reported | How the substance was administered. | How the substance was administered. |
| Start Day | start_day | The study day in which the substance was initially encountered. | The study day in which the substance was initially encountered. |
| Start Time | start_time | Time within a study day the substance is initially encountered. | Time within a study day the substance is initially encountered. |
| Status | status | Did the substance encounter complete or was ended. | Did the substance encounter complete or was ended. |
| Study ID | study_id | A biological sample may be linked to a single study. | Please enter either a study user defined ID or ImmPort accession. |
| Subject ID | subject_id | Please enter either a subject user defined ID or ImmPort accession for the subject from which the sample was derived. A single subject record is permitted. | Please enter either a subject user defined ID or ImmPort accession for the subject from which the sample was derived. |
| User Defined ID | user_defined_id | The intervention user defined ID is an identifier chosen by the data provider to refer to a adverse event. The user defined ID is not shared. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| user_defined_id | USER_DEFINED_ID | intervention_accession | SM | intervention_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| user_defined_id | PRIMARY | intervention | getAvailableUserDefinedIdsMap | intervention_accession | SM | intervention_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| compound_name_reported | yes | - | - | - | - | - | - | - | - | - | 
| compound_role | yes | - | lk_compound_role | - | - | - | - | - | - | - | 
| dose | - | - | - | - | - | - | - | - | float | - | 
| dose_freq_per_interval | - | - | - | - | - | - | - | - | - | - | 
| dose_reported | yes | - | - | - | - | - | - | - | - | - | 
| dose_units | - | - | - | - | - | - | - | - | - | - | 
| duration | - | - | - | - | - | - | - | - | - | - | 
| duration_unit | - | - | lk_time_unit | - | - | - | - | - | - | - | 
| end_day | - | - | - | - | - | - | - | - | - | - | 
| end_time | - | - | - | - | - | - | - | - | - | - | 
| formulation | - | - | - | - | - | - | - | - | - | - | 
| is_ongoing | - | - | - | - | - | - | - | - | - | - | 
| name_reported | yes | - | - | - | - | - | - | - | - | - | 
| reported_indication | - | - | - | - | - | - | - | - | - | - | 
| route_of_admin_reported | - | - | - | - | - | - | - | - | - | - | 
| start_day | - | - | - | - | - | - | - | - | - | - | 
| start_time | - | - | - | - | - | - | - | - | - | - | 
| status | - | - | - | - | - | - | - | - | - | - | 
| study_id | yes | - | - | - | - | - | - | - | - | - | 
| subject_id | yes | - | - | - | - | - | - | - | - | - | 
| user_defined_id | yes | - | - | - | - | - | - | - | - | - | 

### Foreign Key Information
FOREIGN KEY TYPE:	user-defined-id	Input column is a User Defined ID and the Output column is the Accession associated with User Defined ID in the given table if the input is a user defined ID

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | study_id | study_accession | study | getAvailableUserDefinedIdsMap | 

FOREIGN KEY TYPE:	accession	Input column is an Accession and the Output column is the Accession in the given table if the input is defined and an accession

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | study_id | study_accession | study | getAvailableAccsToParentMap | 

### Upload Table Information

Table: intervention    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| compound_name_reported | varchar | 250 | yes | - | - | - | - | 
| compound_role | varchar | 40 | - | - | - | - | - | 
| dose | float | - | - | - | - | - | - | 
| dose_freq_per_interval | varchar | 40 | yes | - | - | - | - | 
| dose_reported | varchar | 150 | yes | - | - | - | - | 
| dose_units | varchar | 40 | yes | - | - | - | - | 
| duration | varchar | 40 | yes | - | - | - | - | 
| duration_unit | varchar | 10 | - | - | - | - | - | 
| end_day | varchar | 40 | yes | - | - | - | - | 
| end_time | varchar | 40 | yes | - | - | - | - | 
| formulation | varchar | 125 | yes | - | - | - | - | 
| intervention_accession | varchar | 15 | - | - | - | - | - | 
| is_ongoing | varchar | 40 | yes | - | - | - | - | 
| name_reported | varchar | 125 | yes | - | - | - | - | 
| reported_indication | varchar | 255 | yes | - | - | - | - | 
| route_of_admin_reported | varchar | 40 | yes | - | - | - | - | 
| start_day | varchar | 40 | yes | - | - | - | - | 
| start_time | varchar | 40 | yes | - | - | - | - | 
| status | varchar | 40 | yes | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | - | - | 
| subject_accession | varchar | 15 | - | - | - | - | - | 
| user_defined_id | varchar | 200 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PostRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | LIST INPUT COLUMNS | LIST TABLE NAME | LIST VALIDATION QUERY NAME | 
|  --- | --- | --- | --- | --- | --- | --- |
| list type | check-value-in-entity | - | ['study_accession', 'subject_accession', 'intervention'] | [subject_accession] | arm_or_cohort | getStudiesForSubjectAccNum | 


### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


### Controlled Vocabularies
| lk_compound_role | lk_compound_role | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 
| lk_time_unit | lk_time_unit | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 

