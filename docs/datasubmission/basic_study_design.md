# Template: **basic_study_design**

| Name | Value |
| --- | --- |
| Template Type | compound |
| Schema Version | 3.33 |
| Standard File Name | basic_study_design.txt |

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| global.panel_name | - | - | lk_study_panel | - | - | yes | yes | - | - | [arm or cohorts, demographics, documentation, mechassays, subject, summary, inclusionExclusion] | 
| global.study_accession | - | - | - | - | - | yes | - | - | - | - | 

### Upload Table Information

Table: study_2_panel    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| panel_name | varchar | 100 | - | - | - | global.panel_name | yes | 
| study_accession | varchar | 15 | - | - | - | global.study_accession | - | 

### Controlled Vocabularies
| lk_study_panel | lk_study_panel | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | 
|  | DATABASE COLUMNS | name | description | 

***
## Compound Template: **study**

| Name | Value |
| --- | --- |
| Format | vertical |
| Required | yes |
| Multiple | no |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Actual Start Date | actual_start_date | The date format is either dd-MMM-yy or dd-MMM-yyyy where day (dd) is one or two digits 1..31 appropriate to the month, month (MMM) is case-insensitive value (Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec), and year is either (yy) two digits, for example 05 means 2005, and 96 means 1996, or (yyyy) is four digit year, for example 2005. | The commencement time point of the study. The date format is either dd-MMM-yy or dd-MMM-yyyy. |
| Age Unit | age_unit | The unit of time used to describe the subject's age in the study.  The unit of time for a subject must conform to this unit. | The unit of time used to describe the subject's age in the study.  The unit of time for a subject must conform to this unit. |
| Brief Description | brief_description | A brief study description highlights the essential features of a study. | Summarize the goals, methods and results of the study. |
| Brief Title | brief_title | The brief title will be displayed on ImmPort wherever the study is described. | The brief title serves as a working title for a study. |
| Description | description | The detailed description can be formatted with html tags to improve legibility. Embedded new line characters should be removed. | The detailed description supports a lengthy description of the goals and methods of the study. |
| Endpoints | endpoints | The endpoints can be formatted with html tags to improve legibility. Embedded new line characters should be removed. | Endpoints include assessments, lab tests and assays that are part of a study design. |
| Hypothesis | hypothesis | The hypothesis can be formatted with html tags to improve legibility. Embedded new line characters should be removed. | The explanatory proposition(s) being tested by the research study. |
| Intervention Agent | intervention_agent | If a study is interventional or has an interventional component, a short descriptive name of the intervention agent is requested. | IA brief description of the study's interventional component (e.g. influenza vaccine). |
| Maximum Age | maximum_age | The maximum age of subjects enrolled in the study. | The maximum age of subjects enrolled in the study. |
| Minimum Age | minimum_age | The minimum age of subjects enrolled in the study. | The minimum age of subjects enrolled in the study. |
| Objectives | objectives | The objectives can be formatted with html tags to improve legibility. Embedded new line characters should be removed. | The goals of the research study. |
| Official Title | official_title | The official study title is displayed on the ImmPort study detail page. | The official study title may be the same as the brief title, but is often more descriptive. |
| Sponsoring Organization | sponsoring_organization | The organization that provides funding and support for the study. | The organization that provides funding and support for the study. |
| Target Enrollment | target_enrollment | The number of subjects proposed to be enrolled in the study. | The number of subjects proposed to be enrolled in the study. |
| User Defined ID | user_defined_id | The study user defined ID is an identifier chosen by the data provider to refer to a study design. This ID may be referenced by other data records (e.g. arm). The user defined ID is not shared. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| user_defined_id | USER_DEFINED_ID | global.study_accession | SDY | study_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| user_defined_id | PRIMARY | study | getAvailableUserDefinedIdsMap | global.study_accession | SDY | study_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| actual_start_date | - | - | - | - | - | - | - | - | - | - | 
| age_unit | yes | - | lk_time_unit | - | - | - | - | - | - | - | 
| brief_description | yes | - | - | - | - | - | - | - | - | - | 
| brief_title | yes | - | - | - | - | - | - | - | - | - | 
| description | yes | - | - | - | - | - | - | - | - | - | 
| endpoints | yes | - | - | - | - | - | - | - | - | - | 
| hypothesis | - | - | - | - | - | - | - | - | - | - | 
| intervention_agent | yes | - | - | - | - | - | - | - | - | - | 
| maximum_age | - | - | - | - | - | - | - | - | - | - | 
| minimum_age | - | - | - | - | - | - | - | - | - | - | 
| objectives | - | - | - | - | - | - | - | - | - | - | 
| official_title | yes | - | - | - | - | - | - | - | - | - | 
| sponsoring_organization | yes | - | - | - | - | - | - | - | - | - | 
| target_enrollment | - | - | - | - | - | - | - | - | positive | - | 
| user_defined_id | yes | - | - | - | - | - | - | - | - | - | 

### Upload Table Information

Table: study    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| actual_start_date | date | - | - | - | - | - | - | 
| age_unit | varchar | 25 | - | - | - | - | - | 
| brief_description | varchar | 4000 | yes | - | - | - | - | 
| brief_title | varchar | 250 | yes | - | - | - | - | 
| description | clob | - | - | yes | - | - | - | 
| endpoints | clob | - | - | yes | - | - | - | 
| hypothesis | varchar | 4000 | yes | - | - | - | - | 
| intervention_agent | varchar | 1000 | yes | - | - | - | - | 
| maximum_age | varchar | 40 | yes | - | - | - | - | 
| minimum_age | varchar | 40 | yes | - | - | - | - | 
| objectives | clob | - | - | yes | - | - | - | 
| official_title | varchar | 500 | yes | - | - | - | - | 
| sponsoring_organization | varchar | 250 | yes | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | global.study_accession | - | 
| target_enrollment | integer | - | - | - | - | - | - | 
| user_defined_id | varchar | 150 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: workspace_2_study    Type: workspace

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| study_accession | varchar | 15 | - | - | - | global.study_accession | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PreRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | check-date-format | Provided Below | ['actual_start_date'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		not-empty-value	actual_start_date	-

### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | - | [] | [order_number] | [Action = set, Value = 1] | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | - | [user_defined_id] | [user_defined_id] | - | - | - | 


### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [global.study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| create-study-directories | - | [global.study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | - | [global.study_accession] | [study_accession] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-values-to-entity | - | [age_unit, study_accession] | [] | - | - | - | 


### Controlled Vocabularies
| lk_time_unit | lk_time_unit | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 


***
## Compound Template: **study_categorization**

| Name | Value |
| --- | --- |
| Format | vertical |
| Required | yes |
| Multiple | no |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Research Focus | research_focus | A research focus for the study from the drop down list | Please use the drop down list |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| research_focus | KEY | study_categorization_id | - | study_categorization_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| research_focus | yes | - | lk_research_focus | - | - | - | - | - | - | - | 

### Upload Table Information

Table: study_categorization    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| research_focus | varchar | 50 | - | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | global.study_accession | - | 
| study_categorization_id | integer | - | - | - | - | - | - | 

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-user-defined-id-to-parent | - | [study_categorization, getAvailableUserDefinedIdsByParentTable, global.study_accession, study_accession] | [] | - | - | - | 


### Controlled Vocabularies
| lk_research_focus | lk_research_focus | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 


***
## Compound Template: **study_2_condition_or_disease**

| Name | Value |
| --- | --- |
| Format | vertical |
| Required | yes |
| Multiple | yes |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Condition Reported | condition_reported | The condition(s)/disease(s) that is (are) being researched or evaluated in the study.  Please select condition or disease from the list provided if the condition or disease matches yours or enter a condition or disease if there is not an appropriate one provided.  Values provided by the user are further checked against the pref mapping table lk_study_condition_pref_mappng. | The condition(s)/disease(s) that is (are) being researched or evaluated in the study.  Please select condition or disease from the list provided if the condition or disease matches yours or enter a condition or disease if there is not an appropriate one provided.  Values provided by the user are further checked against the pref mapping table lk_study_condition_pref_mappng. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| condition_reported | KEY | - | - | - | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| condition_reported | yes | - | - | lk_disease_condition | condition_preferred | - | - | - | - | - | 

### Upload Table Information

Table: study_2_condition_or_disease    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| condition_preferred | varchar | 250 | - | - | - | - | - | 
| condition_reported | varchar | 550 | yes | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | global.study_accession | - | 

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-preferred-value | - | [lk_study_condition_pref_mappng, condition_reported, condition_preferred] | [condition_reported, condition_preferred] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-user-defined-id-to-parent | - | [study_2_condition_or_disease, getAvailableUserDefinedIdsByParentTable, global.study_accession, study_accession] | [] | - | - | - | 


### Preferred Vocabularies

#### Column: condition_reported Table: lk_disease_condition

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | condition_reported | condition_preferred | condition_preferred | 


### Preferred Vocabulary Tables

#### lk_disease_condition

| lk_disease_condition | lk_disease | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | condition_preferred | description | link | disease_ontology_id | id | 
|  | DATABASE COLUMNS | name | description | link | disease_ontology_id | human_phenotype_id | 



***
## Compound Template: **arm_or_cohort**

| Name | Value |
| --- | --- |
| Format | horizontal |
| Required | yes |
| Multiple | yes |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Description | description | The description should expand any abbreviations used in the arm or cohort name. For example for an observational study with a cohort whose name was "ADEH+", the description would be "Atopic dermatitis with eczema herpeticum". | The description should expand any abbreviations used in the arm or cohort name. |
| Name | name | The arm or cohort name is not referenced by other data records. | The arm or cohort name is an alternate identifier that is visible when the study is shared. |
| Type | type | For an interventional study, the type defines the treatment/control attributes of the arms. The attributes are selected from the values listed below (a study may have more than one arm of a given value). Clinical studies often use the following terms. Experimental - Arm for procedure or drug being evaluated. Active Comparator - arm receiving "standard of care" treatment. Placebo Comparator - arm receiving placebo treatment. Sham Comparator - arm receiving a sham procedure such as a surgery or a sham device. No Intervention - arm receiving neither "standard of care" treatment a placebo, or sham procedure or device. For an observational study, the type should be Observational - All arms are observing differences in cohorts | Example clinical study values: Observational, Experimental, Active Comparator, Placebo Comparator, Sham Comparator |
| User Defined ID | user_defined_id | The study's arm(s) or cohort(s) group subjects by criteria relevant to the study (e.g. age, condition) and/or treatments or interventions. Insert rows in the template to define additional arms or cohorts linked to the study. Use the study_design_edit template to add additional records after a study is defined in ImmPort. | The arm or cohort user defined ID is an identifier chosen by the data provider to refer to a subject grouping in the study document. This ID may be referenced by other data records (e.g. subjects). The user defined ID is not shared. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| user_defined_id | USER_DEFINED_ID | arm_accession | ARM | arm_or_cohort_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| user_defined_id | PRIMARY | arm_or_cohort | getAvailableUserDefinedIdsMap | arm_accession | ARM | arm_or_cohort_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| description | yes | - | - | - | - | - | - | - | - | - | 
| name | yes | - | - | - | - | - | - | - | - | - | 
| type | - | - | - | - | - | - | - | - | - | - | 
| user_defined_id | yes | - | - | - | - | - | - | - | - | - | 

### Upload Table Information

Table: arm_or_cohort    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| arm_accession | varchar | 15 | - | - | - | - | - | 
| description | varchar | 4000 | yes | - | - | - | - | 
| name | varchar | 126 | yes | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | global.study_accession | - | 
| type | varchar | 20 | yes | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-child-to-parent-accession | - | [arm_or_cohort, accession-to-accession, getAvailableAccsToParentMap, arm_accession, global.study_accession] | [] | - | - | - | 



***
## Compound Template: **study_personnel**

| Name | Value |
| --- | --- |
| Format | horizontal |
| Required | yes |
| Multiple | yes |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Email | email | Contact information of the study personnel being described. | Contact information of the study personnel being described. |
| First Name | first_name | The first name of the study personnel being described. | The first name of the study personnel being described. |
| Honorific | honorific | Usually, the education achievement level of the person. | Usually, the education achievement level of the person. |
| Last Name | last_name | The last name of the study personnel being described. | The last name of the study personnel being described. |
| ORCID ID | orcid | ORCID (Open Researcher and Contributor Identification), a non-profit organization that promotes the use of its unique digital identifier to connect researchers with their science contributions over time and across changes of name, location and institutional affiliation.  The NIH encourages use of this ID.  See the link https://nexus.od.nih.gov/all/2019/08/05/linking-orcid-identifiers-to-era-profiles-to-streamline-application-processes-and-to-enhance-tracking-of-career-outcomes/. | ORCID (Open Researcher and Contributor Identification), a non-profit organization that promotes the use of its unique digital identifier to connect researchers with their science contributions over time and across changes of name, location and institutional affiliation.  The NIH encourages use of this ID. |
| Organization | organization | The organization with whom the study personnel being described is affiliated. | The organization with whom the study personnel being described is affiliated. |
| Role In Study | role_in_study | The ImmPort display will show the personnel listed as 'PI' in the study. | Please use the drop down list. |
| Site Name | site_name | Enter the site name if there is a need to further differentiate the affiliation of the study personnel form the Organization. | Enter the site name if there is a need to further differentiate the affiliation of the study personnel from the Organization. |
| Suffixes | suffixes | Suffixes that are part of the study personnel's name being described. | Suffixes that are part of the study personnel's name being described. |
| Title In Study | title_in_study | The role the personnel play in the study as defined by the research team. | The role the personnel play in the study as defined by the research team. |
| User Defined ID | user_defined_id | The personnel user defined ID is an identifier chosen by the data provider to refer to personnel who may be contacted for more details about the study document. If more than one study personnel record is to be defined, copy the block of rows from Study_Personnel_ID to Site_Name for each additional study personnel record. Use the study_design_edit template to add additional records after a study is defined in ImmPort. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| user_defined_id | USER_DEFINED_ID | person_accession | PSN | study_personnel_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| user_defined_id | PRIMARY | study_personnel | getAvailableUserDefinedIdsMap | person_accession | PSN | study_personnel_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| email | yes | - | - | - | - | - | - | - | - | - | 
| first_name | yes | - | - | - | - | - | - | - | - | - | 
| honorific | - | - | - | - | - | - | - | - | - | - | 
| last_name | yes | - | - | - | - | - | - | - | - | - | 
| orcid | - | - | - | - | - | - | - | - | - | - | 
| organization | yes | - | - | - | - | - | - | - | - | - | 
| role_in_study | yes | - | lk_personnel_role | - | - | - | - | - | - | - | 
| site_name | yes | - | - | - | - | - | - | - | - | - | 
| suffixes | - | - | - | - | - | - | - | - | - | - | 
| title_in_study | yes | - | - | - | - | - | - | - | - | - | 
| user_defined_id | yes | - | - | - | - | - | - | - | - | - | 

### Upload Table Information

Table: study_personnel    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| email | varchar | 100 | yes | - | - | - | - | 
| first_name | varchar | 40 | yes | - | - | - | - | 
| honorific | varchar | 20 | yes | - | - | - | - | 
| last_name | varchar | 40 | yes | - | - | - | - | 
| orcid | varchar | 1000 | yes | - | - | - | - | 
| organization | varchar | 125 | yes | - | - | - | - | 
| person_accession | varchar | 15 | - | - | - | - | - | 
| role_in_study | varchar | 40 | - | - | - | - | - | 
| site_name | varchar | 100 | yes | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | global.study_accession | - | 
| suffixes | varchar | 40 | yes | - | - | - | - | 
| title_in_study | varchar | 100 | yes | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### Controlled Vocabularies
| lk_personnel_role | lk_personnel_role | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 


***
## Compound Template: **planned_visit**

| Name | Value |
| --- | --- |
| Format | horizontal |
| Required | yes |
| Multiple | yes |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| End Rule | end_rule | Enter an end rule only if it is more interesting than "subject has arrived for a scheduled visit". | Enter an end rule only if it is more interesting than "subject has arrived for a scheduled visit". |
| Max Start Day | max_start_day | This is a positive or negative numeric value. If no value is entered, the maximum start day will be set equal to the minimum start day. | The maximum start day for a visit as defined in the study schedule. |
| Min Start Day | min_start_day | This is a positive or negative numeric value. | The minimum start day for a visit as defined in the study schedule. |
| Name | name | the visit name should indicate the purpose of the visit (e.g. screening, assessment, inoculation, sample drawn). The visit name is not referenced by other data records. | The visit name is an alternate identifier that is visible when the protocol is shared. |
| Order Number | order_number | This is a positive whole number value. | The order of the visit within the study design schedule. |
| Start Rule | start_rule | Enter a start rule only if it is more interesting than "subject has arrived for a scheduled visit". | Enter a start rule only if it is more interesting than "subject has arrived for a scheduled visit". |
| User Defined ID | user_defined_id | The planned visit user defined ID is an identifier chosen by the data provider to refer to a planned visit. This ID may be referenced by other data records (e.g. biological samples). The user defined ID is not shared. Insert rows in the template to define additional planned visits linked to the study. Use the study_design_edit template to add additional records after a study is defined in ImmPort. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| order_number | UNIQUE | - | - | - | 
| user_defined_id | USER_DEFINED_ID | planned_visit_accession | PV | planned_visit_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| user_defined_id | PRIMARY | planned_visit | getAvailableUserDefinedIdsMap | planned_visit_accession | PV | planned_visit_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| end_rule | - | - | - | - | - | - | - | - | - | - | 
| max_start_day | - | - | - | - | - | - | - | - | float | - | 
| min_start_day | yes | - | - | - | - | - | - | - | float | - | 
| name | yes | - | - | - | - | - | - | - | - | - | 
| order_number | yes | - | - | - | - | - | - | - | positive | - | 
| start_rule | - | - | - | - | - | - | - | - | - | - | 
| user_defined_id | yes | - | - | - | - | - | - | - | - | - | 

### Upload Table Information

Table: planned_visit    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| end_rule | varchar | 256 | yes | - | - | - | - | 
| max_start_day | float | - | - | - | - | - | - | 
| min_start_day | float | - | - | - | - | - | - | 
| name | varchar | 125 | yes | - | - | - | - | 
| order_number | integer | - | - | - | - | - | - | 
| planned_visit_accession | varchar | 15 | - | - | - | - | - | 
| start_rule | varchar | 256 | yes | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | global.study_accession | - | 
| user_defined_id | varchar | 100 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [min_start_day] | [max_start_day] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	empty-value	max_start_day	-

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-child-to-parent-accession | - | [planned_visit, accession-to-accession, getAvailableAccsToParentMap, planned_visit_accession, global.study_accession] | [] | - | - | - | 



***
## Compound Template: **inclusion_exclusion**

| Name | Value |
| --- | --- |
| Format | horizontal |
| Required | yes |
| Multiple | yes |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Criterion | criterion | One or more criterion must be described to decide whether a subject may be enrolled in a study. | The criterion describes the parameter used to decide if a subject may be enrolled in a study. |
| Criterion Category | criterion_category | The criterion category is selected form a preferred list of terms. | There are two values to choose from: inclusion or exclusion. |
| User Defined ID | user_defined_id | The inclusion or exclusion user defined ID is an identifier chosen by the data provider to refer to a criterion used to determine whether a subject may be enrolled in a study. Use the study_design_edit template to add additional records after a study is defined in ImmPort. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| user_defined_id | USER_DEFINED_ID | criterion_accession | CRIT | inclusion_exclusion_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| user_defined_id | PRIMARY | inclusion_exclusion | getAvailableUserDefinedIdsMap | criterion_accession | CRIT | inclusion_exclusion_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| criterion | yes | - | - | - | - | - | - | - | - | - | 
| criterion_category | yes | - | lk_criterion_category | - | - | - | - | - | - | - | 
| user_defined_id | yes | - | - | - | - | - | - | - | - | - | 

### Upload Table Information

Table: inclusion_exclusion    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| criterion | varchar | 750 | yes | - | - | - | - | 
| criterion_accession | varchar | 15 | - | - | - | - | - | 
| criterion_category | varchar | 40 | - | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | global.study_accession | - | 
| user_defined_id | varchar | 100 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### Controlled Vocabularies
| lk_criterion_category | lk_criterion_category | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 


***
## Compound Template: **study_2_protocol**

| Name | Value |
| --- | --- |
| Format | vertical |
| Required | yes |
| Multiple | yes |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Protocol ID | protocol_id | The protocol ID for the study. Use the study_design_edit template to add additional records after a study is defined in ImmPort. | The protocol ID for the study. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| protocol_id | KEY | - | - | - | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| protocol_id | yes | - | - | - | - | - | - | - | - | - | 

### Foreign Key Information
FOREIGN KEY TYPE:	user-defined-id	Input column is a User Defined ID and the Output column is the Accession associated with User Defined ID in the given table if the input is a user defined ID

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | protocol_id | protocol_accession | protocol | getAvailableUserDefinedIdsMap | 

FOREIGN KEY TYPE:	accession	Input column is an Accession and the Output column is the Accession in the given table if the input is defined and an accession

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | protocol_id | protocol_accession | protocol | getAvailableAccsToParentMap | 

### Upload Table Information

Table: study_2_protocol    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| protocol_accession | varchar | 15 | - | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | global.study_accession | - | 

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-user-defined-id-to-parent | - | [study_2_protocol, getAvailableUserDefinedIdsByParentTable, global.study_accession, study_accession] | [] | - | - | - | 



***
## Compound Template: **study_file**

| Name | Value |
| --- | --- |
| Format | horizontal |
| Required | no |
| Multiple | yes |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Description | description | A brief description of the file. | A brief description of the file. |
| File Name | file_name | If there are additional files (e.g. as data dictionaries, CRFs, custom formatted lab tests or assessments) that should be linked to the study please indicate them in this block. Insert rows in the template to link additional files to the study. Use the study_design_edit template to add additional records after a study is defined in ImmPort. The file size name limit is 250 characters. For a given study, all file names for study_file must be unique. | The name of the file, including file extension, that is to be linked to the study. The file size name limit is 250 characters. For a given study, all file names for study_file must be unique. |
| Study File Type | study_file_type | Additional study data or study descriptions are current preferred terms. | Please choose from the drop down list. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| file_name | KEY | study_file_accession | SFL | study_file_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| description | yes | - | - | - | - | - | - | - | - | - | 
| file_name | yes | - | - | - | - | - | - | - | - | - | 
| study_file_type | yes | - | lk_study_file_type | - | - | - | - | - | - | - | 
| study_files | - | - | - | - | - | - | - | yes | - | study files | 

### Save File Information

| TABLE NAME | FILE NAME COLUMN | PATH COLUMN | 
|  --- | --- | --- |
| study_file | file_name | path | 

### Upload Table Information

Table: study_file    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| description | varchar | 4000 | yes | - | - | - | - | 
| file_name | varchar | 250 | yes | - | - | - | - | 
| path | varchar | 4000 | - | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | global.study_accession | - | 
| study_file_accession | varchar | 15 | - | - | - | - | - | 
| study_file_type | varchar | 50 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-name-uniquely-to-list | - | [study_files] | [global.panel_name] | - | - | - | 


### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| create-study-file-path-expression | - | [file_name, global.study_accession] | [path] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-user-defined-id-to-parent | - | [study_file, getAvailableUserDefinedIdsByParentTable, global.study_accession, study_accession] | [] | - | - | - | 


### Controlled Vocabularies
| lk_study_file_type | lk_study_file_type | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 


***
## Compound Template: **study_link**

| Name | Value |
| --- | --- |
| Format | horizontal |
| Required | no |
| Multiple | yes |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Name | name | The name of the website to which the link refers. Use the study_design_edit template to add additional records after a study is defined in ImmPort. | The name of the website to which the link refers. |
| Value | value | If this is a clinical trial, please include the clinicalTrial.gov URL. | Define websites that are linked to the study. Insert rows in the template to define additional websites linked to the study. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| [name, value] | KEY | study_link_id | - | study_link_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| name | yes | - | - | - | - | - | - | - | - | - | 
| value | yes | - | - | - | - | - | - | - | - | - | 

### Upload Table Information

Table: study_link    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| name | varchar | 500 | yes | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | global.study_accession | - | 
| study_link_id | integer | - | - | - | - | - | - | 
| value | varchar | 2000 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-user-defined-id-to-parent | - | [study_link, getAvailableUserDefinedIdsByParentTable, global.study_accession, study_accession] | [] | - | - | - | 



***
## Compound Template: **study_pubmed**

| Name | Value |
| --- | --- |
| Format | horizontal |
| Required | no |
| Multiple | yes |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Authors | authors | The article's authors. | The article's authors. |
| DOI | doi | Digital Object Identifier is a persistent identifier or handle used to uniquely identify an object. ImmPort DOIs are generated by DataCite (https://www.datacite.org/) | Digital Object Identifier is a persistent identifier or handle used to uniquely identify an object. |
| Issue | issue | The journal's issue number. | The journal's issue number. |
| Journal | journal | The journal name that publishes an article that includes data from this study. | The journal name that publishes an article that includes data from this study. |
| Month | month | The article publication month. | The article publication month. |
| Pages | pages | The journal's page number. | The journal's page number. |
| Pubmed ID | pubmed_id | The Pubmed or PubMedCentral identifier of an article that includes data from this study. Use the study_design_edit template to add additional records after a study is defined in ImmPort. | The Pubmed or PubMedCentral identifier of an article that includes data from this study. |
| Title | title | The title of an article that includes data from this study. | The title of an article that includes data from this study. |
| Year | year | The article publication year. | The article publication year. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| pubmed_id | KEY | - | - | - | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| authors | - | - | - | - | - | - | - | - | - | - | 
| doi | - | - | - | - | - | - | - | - | - | - | 
| issue | - | - | - | - | - | - | - | - | - | - | 
| journal | - | - | - | - | - | - | - | - | - | - | 
| month | - | - | - | - | - | - | - | - | - | - | 
| pages | - | - | - | - | - | - | - | - | - | - | 
| pubmed_id | yes | - | - | - | - | - | - | - | - | - | 
| title | - | - | - | - | - | - | - | - | - | - | 
| year | - | - | - | - | - | - | - | - | - | - | 

### Upload Table Information

Table: study_pubmed    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| authors | varchar | 4000 | yes | - | - | - | - | 
| doi | varchar | 100 | - | - | - | - | - | 
| issue | varchar | 20 | yes | - | - | - | - | 
| journal | varchar | 250 | yes | - | - | - | - | 
| month | varchar | 12 | yes | - | - | - | - | 
| pages | varchar | 20 | yes | - | - | - | - | 
| pubmed_id | varchar | 16 | yes | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | global.study_accession | - | 
| title | varchar | 4000 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 
| year | varchar | 4 | yes | - | - | - | - | 

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-user-defined-id-to-parent | - | [study_pubmed, getAvailableUserDefinedIdsByParentTable, global.study_accession, study_accession] | [] | - | - | - | 


