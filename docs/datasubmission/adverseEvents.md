# Template: **adverseevents**

| Name | Value |
| --- | --- |
| Template Type | single |
| Schema Version | 3.33 |
| Standard File Name | adverseEvents.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Causality | causality | Was the adverse event believed to be casued by a study intervention. | Was the adverse event believed to be caused by a study intervention. |
| Description | description | A lengthier description of the adverse event. | A lengthier description of the adverse event. |
| End Study Day | end_study_day | The study day in which the adverse event ceased. | The study day in which the adverse event ceased. |
| End Time | end_time | Allows for describing the time during a study day in which an adverse event was reported. | Allows for describing the time during a study day in which an adverse event was reported. |
| Location Of Reaction Reported | location_of_reaction_reported | Where on/in the subject was the adverse event reported. | Where on/in the subject was the adverse event reported. |
| Name Preferred | name_preferred | The preferred adverse event name is a term from the MedDRA (www.meddra.org) adverse event classification dictionary. This is an optional term and often updated by ImmPort staff by mapping AE reported names to MedDRA terms. | The preferred adverse event name is a term from the MedDRA (www.meddra.org) adverse event classification dictionary. |
| Name Reported | name_reported | The adverse event name is a display name that is available when the data is shared, but it is not referenced by other data.. | The adverse event name is an alternate identifier that is visible when the adverse event is shared. |
| Organ Or Body System Reported | organ_or_body_system_reported | Which portion(s) of the subject was affected by the adverse event. | Which portion(s) of the subject was affected by the adverse event. |
| Outcome Reported | outcome_reported | Describe the outcome of the adverse event. | The outcome of the adverse event. |
| Relation To Nonstudy Treatment | relation_to_nonstudy_treatment | Was the adverse event related to some non-study intervention. | Was the adverse event related to some non-study intervention. |
| Relation To Study Treatment | relation_to_study_treatment | Was the adverse event believed to be related to a study intervention. | Was the adverse event believed to be related to a study intervention. |
| Severity Reported | severity_reported | The severity value is chosen from a list of preferred terms. | The severity value is chosen from a list of preferred terms. |
| Start Study Day | start_study_day | The study day in which the adverse event was initially reported. | The study day in which the adverse event was initially reported. |
| Start Time | start_time | Allows for describing the time during a study day in which an adverse event was reported. | Allows for describing the time during a study day in which an adverse event was reported. |
| Study ID | study_id | An adverse event may be linked to a single study. | Please enter either a study user defined ID or ImmPort accession for the study in which the reported adverse event occurred. |
| Study Treatment Action Taken | study_treatment_action_taken | What was done to address the adverse event. | What was done to address the adverse event. |
| Subject ID | subject_id | Please enter either a subject user defined ID or ImmPort accession for the subject for the reported adverse event. | Please enter either a subject user defined ID or ImmPort accession for the subject for the reported adverse event. |
| User Defined ID | user_defined_id | The adverse event user defined ID is an identifier chosen by the data provider to refer to a adverse event. The user defined ID is not shared. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| user_defined_id | USER_DEFINED_ID | adverse_event_accession | AE | adverse_event_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| user_defined_id | PRIMARY | adverse_event | getAvailableUserDefinedIdsMap | adverse_event_accession | AE | adverse_event_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| causality | - | - | - | - | - | - | - | - | - | - | 
| description | - | - | - | - | - | - | - | - | - | - | 
| end_study_day | - | - | - | - | - | - | - | - | float | - | 
| end_time | - | - | - | - | - | - | - | - | - | - | 
| location_of_reaction_reported | - | - | - | - | - | - | - | - | - | - | 
| name_preferred | - | - | - | - | - | - | - | - | - | - | 
| name_reported | yes | - | - | - | - | - | - | - | - | - | 
| organ_or_body_system_reported | - | - | - | - | - | - | - | - | - | - | 
| outcome_reported | yes | - | - | - | - | - | - | - | - | - | 
| relation_to_nonstudy_treatment | - | - | - | - | - | - | - | - | - | - | 
| relation_to_study_treatment | yes | - | - | - | - | - | - | - | - | - | 
| severity_reported | yes | - | - | lk_adverse_event_severity | severity_preferred | - | - | - | - | - | 
| start_study_day | - | - | - | - | - | - | - | - | float | - | 
| start_time | - | - | - | - | - | - | - | - | - | - | 
| study_id | yes | - | - | - | - | - | - | - | - | - | 
| study_treatment_action_taken | - | - | - | - | - | - | - | - | - | - | 
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

Table: adverse_event    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| adverse_event_accession | varchar | 15 | - | - | - | - | - | 
| causality | varchar | 250 | yes | - | - | - | - | 
| description | varchar | 4000 | yes | - | - | - | - | 
| end_study_day | float | - | - | - | - | - | - | 
| end_time | varchar | 40 | yes | - | - | - | - | 
| location_of_reaction_reported | varchar | 126 | yes | - | - | - | - | 
| name_preferred | varchar | 126 | yes | - | - | - | - | 
| name_reported | varchar | 126 | yes | - | - | - | - | 
| organ_or_body_system_reported | varchar | 126 | yes | - | - | - | - | 
| outcome_reported | varchar | 40 | yes | - | - | - | - | 
| relation_to_nonstudy_treatment | varchar | 250 | yes | - | - | - | - | 
| relation_to_study_treatment | varchar | 250 | yes | - | - | - | - | 
| severity_preferred | varchar | 60 | - | - | - | - | - | 
| severity_reported | varchar | 60 | yes | - | - | - | - | 
| start_study_day | float | - | - | - | - | - | - | 
| start_time | varchar | 40 | yes | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | - | - | 
| study_treatment_action_taken | varchar | 250 | yes | - | - | - | - | 
| subject_accession | varchar | 15 | - | - | - | - | - | 
| user_defined_id | varchar | 150 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PostRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | LIST INPUT COLUMNS | LIST TABLE NAME | LIST VALIDATION QUERY NAME | 
|  --- | --- | --- | --- | --- | --- | --- |
| list type | check-value-in-entity | - | ['study_accession', 'subject_accession', 'adverse_event'] | [subject_accession] | arm_or_cohort | getStudiesForSubjectAccNum | 


### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


### Preferred Vocabularies

#### Column: severity_reported Table: lk_adverse_event_severity

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | severity_reported | severity_preferred | severity_preferred | 


### Preferred Vocabulary Tables

#### lk_adverse_event_severity

| lk_adverse_event_severity | lk_adverse_event_severity | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | severity_preferred | description | link | 
|  | DATABASE COLUMNS | name | description | link | 


