# Template: **immuneexposure**

| Name | Value |
| --- | --- |
| Template Type | single |
| Schema Version | 3.33 |
| Standard File Name | immuneExposure.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Arm Or Cohort ID | arm_or_cohort_id | A subject may be assigned to a single arm within a study. When subjects are initially uploaded to ImmPort, they may be assigned to a single study's arm. | Please enter either a study arm or cohort user defined ID or ImmPort accession. When subjects are initially uploaded to ImmPort, they may be assigned to a single study's arm. |
| Disease Ontology ID | disease_ontology_id | The NCBI Disease Ontology ID associated with the disease. If the Disease Reported is not a preferred value, then the Disease Ontology ID must be provided. If the disease is a preferred value, then the Disease Ontology ID will be the DOID associated with the preferred value. | The NCBI Disease Ontology ID associated with the disease. If the Disease Reported is not a preferred value, then the Disease Ontology ID must be provided. If the disease is a preferred value, then the Disease Ontology ID will be the DOID associated with the preferred value. |
| Disease Reported | disease_reported | This indicates the specific disease of the host associated with the exposure. Please select a disease from the list provided if the disease matches yours or enter a disease if there is not an appropriate one provided. This disease is visible when the result is shared.  The value provided by the user is further checked against the pref mapping table lk_exposure_material_pref_map. | This indicates the specific disease of the host associated with the exposure. Please select a disease from the list provided if the disease matches yours or enter a disease if there is not an appropriate one provided. This disease is visible when the result is shared.  The Value provide by the user is further checked against the pref mapping table lk_study_condition_pref_mappng. |
| Disease Stage Reported | disease_stage_reported | This provides a broad classification of how the disease has progressed. Please select a disease stage from the list provided if the disease stage matches yours or enter a disease stage if there is not an appropriate one provided. This disease stage is visible when the result is shared. | This provides a broad classification of how the disease has progressed. Please select a disease stage from the list provided if the disease stage matches yours or enter a disease stage if there is not an appropriate one provided. This disease stage is visible when the result is shared. |
| Exposure Material ID | exposure_material_id | The NCBI or Vaccine Ontology ID associated with the exposure material. If the Exposure Material Reported is not a preferred value, then the Exposure Material ID must be provided. If the Exposure Material Reported is a preferred value, then the Exposure Material ID will be automatically be the ID associated with the preferred value and user will NOT need to supply this ID. | The NCBI or Vaccine Ontology ID associated with the exposure material. If the Exposure Material Reported is not a preferred value, then the Exposure Material ID must be provided. If the Exposure Material Reported is a preferred value, then the Exposure Material ID will be automatically be the ID associated with the preferred value and user will NOT need to supply this ID. |
| Exposure Material Reported | exposure_material_reported | This describes what substance(s) the host is exposed to and/or develops immune reactions to as part of the exposure process. Please select an exposure material from the list provided if the exposure material matches yours or enter a exposure material if there is not an appropriate one provided. This exposure material is visible when the result is shared.  The value provided by the user is further checked against the pref mapping table lk_exposure_material_pref_map. | This describes what substance(s) the host is exposed to and/or develops immune reactions to as part of the exposure process. Please select an exposure material from the list provided if the exposure material matches yours or enter a exposure material if there is not an appropriate one provided. This exposure material is visible when the result is shared.  The value provided by the user is further checked against the pref mapping table lk_exposure_material_pref_map. |
| Exposure Process Reported | exposure_process_reported | This identifies the type of process through which a host is exposed and the type of evidence for that exposure to have happened, which are tightly intertwined. This is the only element of the four that is always mandatory. Please select an exposure process from the list provided if the process matches yours or enter a exposure process if there is not an appropriate one provided. This exposure process is visible when the result is shared.  The value provided by the user is further checked against the pref mapping table lk_exposure_process_pref_map. | This identifies the type of process through which a host is exposed and the type of evidence for that exposure to have happened, which are tightly intertwined. This is the only element of the four that is always mandatory. Please select an exposure process from the list provided if the process matches yours or enter a exposure process if there is not an appropriate one provided. This exposure process is visible when the result is shared.  The value provided by the user is further checked against the pref mapping table lk_exposure_process_pref_map. |
| Subject ID | subject_id | Please enter either a subject user defined ID or ImmPort accession for the subject for the reported immune exposure. | Please enter either a subject user defined ID or ImmPort accession for the subject for the reported immune exposure. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| [subject_accession, arm_accession, exposure_process_reported, exposure_material_reported, exposure_material_id, disease_reported, disease_ontology_id, disease_stage_reported] | USER_DEFINED_ID | exposure_accession | IM | immune_exposure_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| [subject_accession, arm_accession, exposure_process_reported, exposure_material_reported, exposure_material_id, disease_reported, disease_ontology_id, disease_stage_reported] | PRIMARY | immune_exposure | getAvailableUserDefinedIdsByParentTable | exposure_accession | IM | immune_exposure_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| arm_or_cohort_id | yes | - | - | - | - | - | - | - | - | - | 
| disease_ontology_id | - | yes | - | - | - | - | - | - | - | - | 
| disease_reported | - | yes | - | lk_disease | disease_preferred | - | - | - | - | - | 
| disease_stage_reported | - | yes | - | lk_disease_stage | disease_stage_preferred | - | - | - | - | - | 
| emr_disease_ontology_id | - | - | - | lk_disease | emr_disease_ontology_id | - | - | - | - | - | 
| emr_exposure_material_id | - | - | - | lk_exposure_material | emr_exposure_material_id | - | - | - | - | - | 
| exposure_material_id | - | yes | - | - | - | - | - | - | - | - | 
| exposure_material_reported | - | yes | - | lk_exposure_material | exposure_material_preferred | - | - | - | - | - | 
| exposure_process_reported | yes | - | - | lk_exposure_process | exposure_process_preferred | - | - | - | - | - | 
| max_components | - | - | - | - | - | - | - | yes | - | 2 | 
| subject_id | yes | - | - | - | - | - | - | - | - | - | 

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

### Foreign Key Information
FOREIGN KEY TYPE:	user-defined-id	Input column is a User Defined ID and the Output column is the Accession associated with User Defined ID in the given table if the input is a user defined ID

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | arm_or_cohort_id | arm_accession | arm_or_cohort | getAvailableUserDefinedIdsMap | 

FOREIGN KEY TYPE:	accession	Input column is an Accession and the Output column is the Accession in the given table if the input is defined and an accession

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | arm_or_cohort_id | arm_accession | arm_or_cohort | getAvailableAccsToParentMap | 

FOREIGN KEY TYPE:	accession-to-accession	Input column is an Accession and Output column is the parent Accession associated with the Accession in given table if the input column is defined and an accession

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | arm_accession | study_accession | arm_or_cohort | getAvailableAccsToParentMap | 

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

### PostRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | LIST INPUT COLUMNS | LIST TABLE NAME | LIST VALIDATION QUERY NAME | 
|  --- | --- | --- | --- | --- | --- | --- |
| list type | check-value-in-entity | - | ['arm_accession', 'subject_accession', 'immune_exposure'] | [subject_accession] | arm_2_subject | getArmsForSubjectAccNum | 


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
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


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


