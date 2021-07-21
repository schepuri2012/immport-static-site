# Template: **subjectanimals**

| Name | Value |
| --- | --- |
| Template Type | combined-result |
| Schema Version | 3.33 |
| Standard File Name | subjectAnimals.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Age Event | age_event | A list of preferred terms is available. | Please choose from the drop down list. |
| Age Event Specify | age_event_specify | This column supports providing study milestones for subject's age determination that ImmPort does not support. | If "Age Event" = Other, this field specifies the age event (free text). Otherwise, leave this column blank. |
| Age Unit | age_unit | A list of preferred terms is available.  The age unit must conform to the age unit assigned to the study. | Please choose from the drop down list.  The age unit must conform to the age unit assigned to the study. |
| Arm Or Cohort ID | arm_or_cohort_id | A subject may be assigned to a single arm within a study. When subjects are initially uploaded to ImmPort, they may be assigned to a single study's arm. | Please enter either a study arm or cohort user defined ID or ImmPort accession. When subjects are initially uploaded to ImmPort, they may be assigned to a single study's arm. |
| Gender | gender | A list of preferred terms is available. | Please choose from the drop down list. |
| Max Subject Age | max_subject_age | The subject age at the end of the study may be determined form one of several study milestones. | Please enter a number. |
| Min Subject Age | min_subject_age | The subject age at the outset of the study may be determined form one of several study milestones as indicated in the Age Event column. | Please enter a number. |
| Result Separator Column | result_separator_column | This pseudo column separates meta data from results. | This pseudo column separates the results (lab tests) from the lab test panel meta data. It must always appear and be the column that appears immediately after the last meta-data column and before any result columns. |
| Species | species | A list of preferred terms is available. Macaca fascicularis is also commonly called cynomologus monkey, crab eating macaque, long-tailed macaque. Macaca mulatta is also commonly called rhesus macaque | Please choose from the drop down list. |
| Strain | strain | Please provide strain and breed information as available. | Please provide strain and breed information as available. |
| Strain Characteristics | strain_characteristics | Strain or breed characteristics that are relevant for the study (e.g. susceptibility). | Strain or breed characteristics that are relevant for the study (e.g. susceptibility). |
| Subject ID | subject_id | The subject defined ID is an identifier chosen by the data provider to refer to a subject. This ID may be referenced by other data records (e.g. biological sample). The user defined ID is not shared. For human subjects, the ID should not be identifying. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |
| Subject Location | subject_location | A list of subject locations is available. | Please choose from the drop down list. |
| Subject Phenotype | subject_phenotype | The subject phenotype captures key aspects of the subject's disposition for the study. | Enter a description of the subject. |


### Combined Data

The ID Meta Data Columns include the ID columns that are referenced by more than one entity in the subject template (for example, arm_or_cohorts).  The subject ID is the primary ID and is pre-defined and can be used only once within the template. The arm_or_cohort ID must be pre-defined and can be re-used within the template.

| ID Columns | PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| subject_required | determine-combined-status | - | [subject_id, subject] | [subject_required, subject_user_defined_id, subject_accession] | - | - | - | 
| arm_or_cohort_required | determine-combined-status | - | [arm_or_cohort_id, arm_or_cohort] | [arm_or_cohort_required, arm_or_cohort_user_defined_id, arm_accession] | - | - | - | 

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| subject_user_defined_id | USER_DEFINED_ID | subject_accession | SUB | subject_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| arm_or_cohort_user_defined_id | ANCILLARY | arm_or_cohort | getAvailableUserDefinedIdsMap | arm_accession | ARM | arm_or_cohort_seq | 
| subject_user_defined_id | PRIMARY | subject | getAvailableUserDefinedIdsMap | subject_accession | SUB | subject_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| age_event | - | yes | lk_age_event | - | - | - | - | - | - | - | 
| age_event_specify | - | yes | - | - | - | - | - | - | - | - | 
| age_unit | - | yes | lk_time_unit | - | - | - | - | - | - | - | 
| arm_or_cohort_id | yes | - | - | - | - | - | - | - | - | - | 
| arm_or_cohort_required_value | - | - | - | - | - | - | - | yes | - | no | 
| gender | - | yes | lk_gender | - | - | - | - | - | - | - | 
| max_subject_age | - | - | - | - | - | - | - | - | float | - | 
| min_subject_age | - | yes | - | - | - | - | - | - | float | - | 
| species | - | yes | lk_species | - | - | - | - | - | - | - | 
| strain | - | yes | - | - | - | - | - | - | - | - | 
| strain_characteristics | - | - | - | - | - | - | - | - | - | - | 
| subject_id | yes | - | - | - | - | - | - | - | - | - | 
| subject_location | - | yes | lk_subject_location | - | - | - | - | - | - | - | 
| subject_phenotype | - | - | - | - | - | - | - | - | - | - | 
| subject_required_value | - | - | - | - | - | - | - | yes | - | yes | 

### Conditional Required Columns
| Column Name | CONDITION NAME | DATA ROW COLUMN | VALUE | 
|  --- | --- | --- | --- |
| age_event | case-insensitive-equals | subject_required | 'Yes' | 
| age_unit | case-insensitive-equals | subject_required | 'Yes' | 
| gender | case-insensitive-equals | subject_required | 'Yes' | 
| min_subject_age | case-insensitive-equals | subject_required | 'Yes' | 
| species | case-insensitive-equals | subject_required | 'Yes' | 
| strain | case-insensitive-equals | subject_required | 'Yes' | 
| age_event_specify | case-insensitive-equals | subject_required | 'Yes' | 
| age_event_specify | case-insensitive-equals | age_event | 'other' | 
| subject_location | case-insensitive-equals | subject_required | 'Yes' | 

### Foreign Key Information
FOREIGN KEY TYPE:	accession-to-accession	Input column is an Accession and Output column is the parent Accession associated with the Accession in given table if the input column is defined and an accession

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | arm_accession | study_accession | arm_or_cohort | getAvailableAccsToParentMap | 

### Upload Table Information

Table: arm_or_cohort    Type: ancillary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| arm_accession | varchar | 15 | - | - | - | - | - | 
| description | varchar | 4000 | - | - | - | - | - | 
| name | varchar | 126 | - | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | - | - | 
| type | varchar | 20 | - | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | arm_or_cohort_user_defined_id | - | 
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
| strain | varchar | 50 | yes | - | - | - | - | 
| strain_characteristics | varchar | 500 | yes | - | - | - | - | 
| subject_accession | varchar | 15 | - | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | subject_user_defined_id   | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: arm_2_subject    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| age_event | varchar | 50 | - | - | - | - | - | 
| age_event_specify | varchar | 50 | yes | - | - | - | - | 
| age_unit | varchar | 50 | - | - | - | - | - | 
| arm_accession | varchar | 15 | - | - | - | - | - | 
| max_subject_age | float | - | - | - | - | - | - | 
| min_subject_age | float | - | - | - | - | - | - | 
| subject_accession | varchar | 15 | - | - | - | - | - | 
| subject_location | varchar | 50 | - | - | - | - | - | 
| subject_phenotype | varchar | 200 | yes | - | - | - | - | 

Table: workspace_2_study    Type: workspace

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| study_accession | varchar | 15 | - | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: workspace_2_subject    Type: workspace

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| subject_accession | varchar | 15 | - | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PostRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | values-equal | - | ['The subject ID must always be for a new subject', 'subject_required_value', 'subject_required'] | 


| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | values-equal | - | ['The Arm Or Cohort ID must always be predefined', 'arm_or_cohort_required_value', 'arm_or_cohort_required'] | 


| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | LIST INPUT COLUMNS | LIST TABLE NAME | LIST VALIDATION QUERY NAME | 
|  --- | --- | --- | --- | --- | --- | --- |
| list type | check-value-in-entity | - | ['age_unit', 'study_accession', 'subject'] | [study_accession] | study | getAgeUnitForStudy | 


### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| initialize-columns | Provided Below | [] | [gender, min_subject_age, max_subject_age, age_unit, age_event, age_event_specify, subject_phenotype, species, strain, strain_characteristics] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	subject_required	'No'

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-values-to-entity | - | [study_accession, subject_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-values-to-entity | - | [arm_accession, subject_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [min_subject_age] | [max_subject_age] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	empty-value	max_subject_age	-

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| get-taxonomy-id | Provided Below | [lk_species, species] | [taxonomy_id] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	subject_required	'Yes'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-entity-to-taxonomy-id | Provided Below | [subject, subject_user_defined_id, subject_accession, taxonomy_id] | [] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	subject_required	'Yes'

### Controlled Vocabularies
| lk_age_event | lk_age_event | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 
| lk_gender | lk_gender | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 
| lk_species | lk_species | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | id | subset_id | 
|  | DATABASE COLUMNS | name | common_name | link | taxonomy_id | taxonomy_id_subset | 
| lk_subject_location | lk_subject_location | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 
| lk_time_unit | lk_time_unit | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 

***
## Combined Result Template: **subjectanimals**

| Name | Value |
| --- | --- |
| Template Type | combined-result |
| Schema Version | 3.33 |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Disease Ontology ID | disease_ontology_id | The NCBI Disease Ontology ID associated with the disease. If the Disease Reported is not a preferred value, then the Disease Ontology ID must be provided. If the disease is a preferred value, then the Disease Ontology ID will be the DOID associated with the preferred value. | The NCBI Disease Ontology ID associated with the disease. If the Disease Reported is not a preferred value, then the Disease Ontology ID must be provided. If the disease is a preferred value, then the Disease Ontology ID will be the DOID associated with the preferred value. |
| Disease Reported | disease_reported | This indicates the specific disease of the host associated with the exposure. Please select a disease from the list provided if the disease matches yours or enter a disease if there is not an appropriate one provided. This disease is visible when the result is shared.  The Value provide by the user is further checked against the pref mapping table lk_study_condition_pref_mappng. | This indicates the specific disease of the host associated with the exposure. Please select a disease from the list provided if the disease matches yours or enter a disease if there is not an appropriate one provided. This disease is visible when the result is shared.  The Value provide by the user is further checked against the pref mapping table lk_study_condition_pref_mappng. |
| Disease Stage Reported | disease_stage_reported | This provides a broad classification of how the disease has progressed. Please select a disease stage from the list provided if the disease stage matches yours or enter a disease stage if there is not an appropriate one provided. This disease stage is visible when the result is shared. | This provides a broad classification of how the disease has progressed. Please select a disease stage from the list provided if the disease stage matches yours or enter a disease stage if there is not an appropriate one provided. This disease stage is visible when the result is shared. |
| Exposure Material ID | exposure_material_id | The NCBI or Vaccine Ontology ID associated with the exposure material. If the Exposure Material Reported is not a preferred value, then the Exposure Material ID must be provided. If the Exposure Material Reported is a preferred value, then the Exposure Material ID will be automatically be the ID associated with the preferred value and user will NOT need to supply this ID. | The NCBI or Vaccine Ontology ID associated with the exposure material. If the Exposure Material Reported is not a preferred value, then the Exposure Material ID must be provided. If the Exposure Material Reported is a preferred value, then the Exposure Material ID will be automatically be the ID associated with the preferred value and user will NOT need to supply this ID. |
| Exposure Material Reported | exposure_material_reported | This describes what substance(s) the host is exposed to and/or develops immune reactions to as part of the exposure process. Please select an exposure material from the list provided if the exposure material matches yours or enter a exposure material if there is not an appropriate one provided. This exposure material is visible when the result is shared.  The value provided by the user is further checked against the pref mapping table lk_exposure_material_pref_map. | This describes what substance(s) the host is exposed to and/or develops immune reactions to as part of the exposure process. Please select an exposure material from the list provided if the exposure material matches yours or enter a exposure material if there is not an appropriate one provided. This exposure material is visible when the result is shared.  The value provided by the user is further checked against the pref mapping table lk_exposure_material_pref_map. |
| Exposure Process Reported | exposure_process_reported | This identifies the type of process through which a host is exposed and the type of evidence for that exposure to have happened, which are tightly intertwined. This is the only element of the four that is always mandatory. Please select an exposure process from the list provided if the process matches yours or enter a exposure process if there is not an appropriate one provided. This exposure process is visible when the result is shared.  The value provided by the user is further checked against the pref mapping table lk_exposure_process_pref_map. | This identifies the type of process through which a host is exposed and the type of evidence for that exposure to have happened, which are tightly intertwined. This is the only element of the four that is always mandatory. Please select an exposure process from the list provided if the process matches yours or enter a exposure process if there is not an appropriate one provided. This exposure process is visible when the result is shared.  The value provided by the user is further checked against the pref mapping table lk_exposure_process_pref_map. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| [subject_accession, arm_accession, exposure_process_reported, exposure_material_reported, exposure_material_id, disease_reported, disease_ontology_id, disease_stage_reported] | KEY | exposure_accession | IM | immune_exposure_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| disease_ontology_id | - | yes | - | - | - | - | - | - | - | - | 
| disease_reported | - | yes | - | lk_disease | disease_preferred | - | - | - | - | - | 
| disease_stage_reported | - | yes | - | lk_disease_stage | disease_stage_preferred | - | - | - | - | - | 
| emr_disease_ontology_id | - | - | - | lk_disease | emr_disease_ontology_id | - | - | - | - | - | 
| emr_exposure_material_id | - | - | - | lk_exposure_material | emr_exposure_material_id | - | - | - | - | - | 
| exposure_material_id | - | yes | - | - | - | - | - | - | - | - | 
| exposure_material_reported | - | yes | - | lk_exposure_material | exposure_material_preferred | - | - | - | - | - | 
| exposure_process_reported | yes | - | - | lk_exposure_process | exposure_process_preferred | - | - | - | - | - | 
| max_components | - | - | - | - | - | - | - | yes | - | 2 | 

### Conditional Required Columns
| Column Name | CONDITION NAME | DATA ROW COLUMN | VALUE | 
|  --- | --- | --- | --- |
| exposure_material_reported | case-insensitive-equals | exposure_process_reported | 'administering substance in vivo ; occurrence of asymptomatic infection ; environmental exposure to endemic/ubiquitous agent without evidence for disease ; documented exposure without evidence for disease ; exposure with existing immune reactivity without evidence for disease ; exposure to substance without evidence for disease ; infectious challenge ; transplantation or transfusion ; vaccination ; occurrence of infectious disease ; occurrence of allergy' | 
| exposure_material_id | case-insensitive-equals | exposure_process_reported | 'administering substance in vivo ; occurrence of asymptomatic infection ; environmental exposure to endemic/ubiquitous agent without evidence for disease ; documented exposure without evidence for disease ; exposure with existing immune reactivity without evidence for disease ; exposure to substance without evidence for disease ; infectious challenge ; transplantation or transfusion ; vaccination ; occurrence of infectious disease ; occurrence of allergy' | 
| exposure_material_id | not-preferred-value | exposure_material_reported | 'lk_exposure_material' | 
| disease_ontology_id | case-insensitive-equals | exposure_process_reported | 'infectious challenge' | 
| disease_ontology_id | not-empty-value | disease_reported | - | 
| disease_ontology_id | not-preferred-value | disease_reported | 'lk_disease' | 
| disease_reported | case-insensitive-equals | exposure_process_reported | 'occurrence of autoimmune disease ; occurrence of cancer ; occurrence of disease ; occurrence of infectious disease ; occurrence of allergy' | 
| disease_ontology_id | case-insensitive-equals | exposure_process_reported | 'occurrence of autoimmune disease ; occurrence of cancer ; occurrence of disease ; occurrence of infectious disease ; occurrence of allergy' | 
| disease_ontology_id | not-preferred-value | disease_reported | 'lk_disease' | 
| disease_stage_reported | case-insensitive-equals | exposure_process_reported | 'occurrence of autoimmune disease ; occurrence of cancer ; occurrence of disease ; occurrence of infectious disease ; occurrence of allergy' | 

### Upload Table Information

Table: immune_exposure    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| arm_accession | varchar | 15 | - | - | - | - | - | 
| disease_ontology_id | varchar | 100 | yes | - | - | - | - | 
| disease_preferred | varchar | 250 | - | - | - | - | - | 
| disease_reported | varchar | 550 | yes | - | - | - | - | 
| disease_stage_preferred | varchar | 50 | - | - | - | - | - | 
| disease_stage_reported | varchar | 100 | yes | - | - | - | - | 
| exposure_accession | varchar | 15 | - | - | - | - | - | 
| exposure_material_id | varchar | 100 | yes | - | - | - | - | 
| exposure_material_preferred | varchar | 200 | - | - | - | - | - | 
| exposure_material_reported | varchar | 200 | yes | - | - | - | - | 
| exposure_process_preferred | varchar | 100 | - | - | - | - | - | 
| exposure_process_reported | varchar | 100 | yes | - | - | - | - | 
| subject_accession | varchar | 15 | - | - | - | - | - | 

### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-semi-colon-if-needed | - | [exposure_material_reported, max_components, right] | [exposure_material_reported] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| break-into-components | - | [exposure_material_reported] | [exposure_material_reported, emr_exposure_material_id] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-semi-colon-if-needed | - | [disease_reported, max_components, right] | [disease_reported] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| break-into-components | - | [disease_reported] | [disease_reported, emr_disease_ontology_id] | - | - | - | 


### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-preferred-value | - | [lk_exposure_material_pref_map, exposure_material_reported, exposure_material_preferred] | [exposure_material_reported, exposure_material_preferred] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-preferred-id | - | [lk_exposure_material_id_map, exposure_material_preferred] | [exposure_material_id] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-preferred-value | - | [lk_study_condition_pref_mappng, disease_reported, disease_preferred] | [disease_reported, disease_preferred] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-preferred-id | - | [lk_disease_ontology_id_map, disease_preferred] | [disease_ontology_id] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-preferred-value | - | [lk_exposure_process_pref_map, exposure_process_reported, exposure_process_preferred] | [exposure_process_reported, exposure_process_preferred] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-user-defined-id-to-parent | - | [immune_exposure, getAvailableUserDefinedIdsByParentTable, exposure_accession, exposure_accession] | [] | - | - | - | 


### Preferred Vocabularies

#### Column: disease_reported Table: lk_disease

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | disease_reported | disease_preferred | disease_preferred | 
|  |  | ANCILLARY DATA | 
|  |  | DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  |  | disease_ontology_id | disease_ontology_id | 
|  | emr_disease_ontology_id | emr_disease_ontology_id | disease_ontology_id | 

#### Column: disease_stage_reported Table: lk_disease_stage

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | disease_stage_reported | disease_stage_preferred | disease_stage_preferred | 

#### Column: exposure_process_reported Table: lk_exposure_process

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | exposure_process_reported | exposure_process_preferred | exposure_process_preferred | 

#### Column: exposure_material_reported Table: lk_exposure_material

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | exposure_material_reported | exposure_material_preferred | exposure_material_preferred | 
|  |  | ANCILLARY DATA | 
|  |  | DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  |  | exposure_material_id | exposure_material_id | 
|  | emr_exposure_material_id | emr_exposure_material_id | exposure_material_id | 


### Preferred Vocabulary Tables

#### lk_disease

| lk_disease | lk_disease | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | disease_preferred | description | link | disease_ontology_id | id | 
|  | DATABASE COLUMNS | name | description | link | disease_ontology_id | human_phenotype_id | 

#### lk_disease_stage

| lk_disease_stage | lk_disease_stage | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | disease_stage_preferred | description | link | 
|  | DATABASE COLUMNS | name | description | link | 

#### lk_exposure_material

| lk_exposure_material | lk_exposure_material | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | exposure_material_preferred | description | link | exposure_material_id | 
|  | DATABASE COLUMNS | name | description | link | exposure_material_id | 

#### lk_exposure_process

| lk_exposure_process | lk_exposure_process | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | exposure_process_preferred | description | link | 
|  | DATABASE COLUMNS | name | description | link | 


