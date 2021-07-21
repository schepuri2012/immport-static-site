# Template: **study_design_edit**

| Name | Value |
| --- | --- |
| Template Type | compound |
| Schema Version | 3.33 |
| Standard File Name | study_design_edit.txt |

***
## Compound Template: **study_categorization**

| Name | Value |
| --- | --- |
| Format | vertical |
| Required | no |
| Multiple | no |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Research Focus | research_focus | A research focus for the study from the drop down list | Please use the drop down list |
| Study ID | study_id | The study ID can be either the study user defined ID or a study accession. | The study ID can be either the study user defined ID or a study accession. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| [research_focus, study_accession] | USER_DEFINED_ID | study_categorization_id | - | study_categorization_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| [research_focus, study_accession] | PRIMARY | study_categorization | getAvailableUserDefinedIdsByParentTable | study_categorization_id | - | study_categorization_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| research_focus | yes | - | lk_research_focus | - | - | - | - | - | - | - | 
| study_id | yes | - | - | - | - | - | - | - | - | - | 

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

Table: study_categorization    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| research_focus | varchar | 50 | - | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | - | - | 
| study_categorization_id | integer | - | - | - | - | - | - | 

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-user-defined-id-to-parent | - | [study_categorization, getAvailableUserDefinedIdsByParentTable, study_accession, study_accession] | [] | - | - | - | 


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
| Required | no |
| Multiple | yes |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Condition Reported | condition_reported | The condition(s)/disease(s) that is (are) being researched or evaluated in the study.  Please select condition or disease from the list provided if the condition or disease matches yours or enter a condition or disease if there is not an appropriate one provided.  Values provided by the user are further checked against the pref mapping table lk_study_condition_pref_mappng. | The condition(s)/disease(s) that is (are) being researched or evaluated in the study.  Please select condition or disease from the list provided if the condition or disease matches yours or enter a condition or disease if there is not an appropriate one provided.  Values provided by the user are further checked against the pref mapping table lk_study_condition_pref_mappng. |
| Study ID | study_id | The study ID can be either the study user defined ID or a study accession. | The study ID can be either the study user defined ID or a study accession. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| [condition_reported, study_accession] | USER_DEFINED_ID | - | - | - | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| [condition_reported, study_accession] | PRIMARY | study_2_condition_or_disease | getAvailableUserDefinedIdsByParentTable | - | - | - | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| condition_reported | yes | - | - | lk_disease_condition | condition_preferred | - | - | - | - | - | 
| study_id | yes | - | - | - | - | - | - | - | - | - | 

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

Table: study_2_condition_or_disease    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| condition_preferred | varchar | 250 | - | - | - | - | - | 
| condition_reported | varchar | 550 | yes | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | - | - | 

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-preferred-value | - | [lk_study_condition_pref_mappng, condition_reported, condition_preferred] | [condition_reported, condition_preferred] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-user-defined-id-to-parent | - | [study_2_condition_or_disease, getAvailableUserDefinedIdsByParentTable, study_accession, study_accession] | [] | - | - | - | 


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
## Compound Template: **study_data_release**

| Name | Value |
| --- | --- |
| Format | horizontal |
| Required | no |
| Multiple | yes |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Data Release Date | data_release_date | The date format is either dd-MMM-yy or dd-MMM-yyyy where day (dd) is one or two digits 1..31 appropriate to the month, month (MMM) is case-insensitive value (Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec), and year is either (yy) two digits, for example 05 means 2005, and 96 means 1996, or (yyyy) is four digit year, for example 2005. | The release date for the given version (Data Release Version) study. The date format is either dd-MMM-yy or dd-MMM-yyyy. |
| Data Release Version | data_release_version | The version of the study data release.  It is a positive integer. | The version of the study data release. It is a positive integer. |
| Data Release Status | status | The status of the data release for the study.  Either it is the 'Initial' release or an 'Updated' release. | The status of the data release for the study.  Either it is the 'Initial' release or an 'Updated' release. |
| Study ID | study_id | The study ID can be either the study user defined ID or a study accession. | The study ID can be either the study user defined ID or a study accession. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| [study_accession, data_release_version, data_release_date] | USER_DEFINED_ID | - | - | - | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| [study_accession, data_release_version, data_release_date] | PRIMARY | study_data_release | getAvailableUserDefinedIdsByParentTable | - | - | - | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| data_release_date | yes | - | - | - | - | - | - | - | - | - | 
| data_release_version | yes | - | - | - | - | - | - | - | positive | - | 
| status | yes | - | lk_release_status | - | - | - | - | - | - | - | 
| study_id | yes | - | - | - | - | - | - | - | - | - | 

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

Table: study_data_release    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| data_release_date | date | - | - | - | - | - | - | 
| data_release_version | integer | - | - | - | - | - | - | 
| status | varchar | 50 | - | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PreRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | check-date-format | - | ['data_release_date'] | 


### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| to-date-comparison-format | - | [data_release_date] | [data_release_date] | - | - | - | 


### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


### Controlled Vocabularies
| lk_release_status | lk_release_status | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | 
|  | DATABASE COLUMNS | name | description | 


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
| File Name | file_name | If there are additional files (e.g. as data dictionaries, CRFs, custom formatted lab tests or assements) that should be linked to the study please indicate them in this block. Insert rows in the template to link additional files to the study. The file size name limit is 250 characters. For a given study, all file names for study_file must be unique. | The name of the file, including file extension, that is to be linked to the study. The file size name limit is 250 characters. For a given study, all file names for study_file must be unique. |
| Study File Type | study_file_type | Additional study data or study description are current preferred terms. | Please choose from the drop down list. |
| Study ID | study_id | The study ID can be either the study user defined ID or a study accession. | The study ID can be either the study user defined ID or a study accession. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| [study_accession, file_name] | USER_DEFINED_ID | study_file_accession | SFL | study_file_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| [study_accession, file_name] | PRIMARY | study_file | getAvailableUserDefinedIdsByParentTable | study_file_accession | SFL | study_file_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| description | yes | - | - | - | - | - | - | - | - | - | 
| file_name | yes | - | - | - | - | - | - | - | - | - | 
| study_file_type | yes | - | lk_study_file_type | - | - | - | - | - | - | - | 
| study_id | yes | - | - | - | - | - | - | - | - | - | 

### Foreign Key Information
FOREIGN KEY TYPE:	user-defined-id	Input column is a User Defined ID and the Output column is the Accession associated with User Defined ID in the given table if the input is a user defined ID

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | study_id | study_accession | study | getAvailableUserDefinedIdsMap | 

FOREIGN KEY TYPE:	accession	Input column is an Accession and the Output column is the Accession in the given table if the input is defined and an accession

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | study_id | study_accession | study | getAvailableAccsToParentMap | 

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
| study_accession | varchar | 15 | - | - | - | - | - | 
| study_file_accession | varchar | 15 | - | - | - | - | - | 
| study_file_type | varchar | 50 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| create-study-file-path-expression | - | [file_name, study_accession] | [path] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-user-defined-id-to-parent | - | [study_file, getAvailableUserDefinedIdsByParentTable, study_accession, study_accession] | [] | - | - | - | 


### Controlled Vocabularies
| lk_study_file_type | lk_study_file_type | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 


***
## Compound Template: **study_image**

| Name | Value |
| --- | --- |
| Format | horizontal |
| Required | no |
| Multiple | yes |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Description | description | A brief description of the study image file. | A brief description of the study image file. |
| Image Filename | image_filename | The name of the file containing the study image for the study. The file size name limit is 250 characters. For a given study, all file names for study_file must be unique. | The name of the file containing the study image for the study. |
| Name | name | The name or title for the study schematic. | The name or title for the study schematic. |
| Study ID | study_id | The study ID can be either the study user defined ID or a study accession. | The study ID can be either the study user defined ID or a study accession. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| [study_accession, image_filename] | USER_DEFINED_ID | schematic_accession | SCH | study_image_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| [study_accession, image_filename] | PRIMARY | study_image | getAvailableUserDefinedIdsByParentTable | schematic_accession | SCH | study_image_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| description | - | - | - | - | - | - | - | - | - | - | 
| image_filename | yes | - | - | - | - | - | - | - | - | - | 
| image_type | - | - | - | - | - | - | - | yes | - | STUDY_SCHEMATIC_PRIMARY | 
| name | yes | - | - | - | - | - | - | - | - | - | 
| study_id | yes | - | - | - | - | - | - | - | - | - | 

### Foreign Key Information
FOREIGN KEY TYPE:	user-defined-id	Input column is a User Defined ID and the Output column is the Accession associated with User Defined ID in the given table if the input is a user defined ID

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | study_id | study_accession | study | getAvailableUserDefinedIdsMap | 

FOREIGN KEY TYPE:	accession	Input column is an Accession and the Output column is the Accession in the given table if the input is defined and an accession

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | study_id | study_accession | study | getAvailableAccsToParentMap | 

### Save File Information

| TABLE NAME | FILE NAME COLUMN | PATH COLUMN | 
|  --- | --- | --- |
| study_image | image_filename | image_path | 

### Upload Table Information

Table: study_image    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| description | varchar | 4000 | yes | - | - | - | - | 
| image_filename | varchar | 250 | yes | - | - | - | - | 
| image_path | varchar | 4000 | - | - | - | - | - | 
| image_type | varchar | 40 | yes | - | - | - | - | 
| name | varchar | 40 | yes | - | - | - | - | 
| schematic_accession | varchar | 15 | - | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| create-study-image-path-expression | - | [image_filename, study_accession] | [image_path] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-user-defined-id-to-parent | - | [study_image, getAvailableUserDefinedIdsByParentTable, study_accession, study_accession] | [] | - | - | - | 



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
| Name | name | The name of the website to which the link refers. | The name of the website to which the link refers. |
| Study ID | study_id | The study ID can be either the study user defined ID or a study accession. | The study ID can be either the study user defined ID or a study accession. |
| Value | value | If this is a clinical trial, please include the clinicalTrial.gov URL. | Define websites that are linked to the study. Insert rows in the template to define additional websites linked to the study. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| [study_accession, name, value] | USER_DEFINED_ID | study_link_id | - | study_link_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| [study_accession, name, value] | PRIMARY | study_link | getAvailableUserDefinedIdsByParentTable | study_link_id | - | study_link_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| name | yes | - | - | - | - | - | - | - | - | - | 
| study_id | yes | - | - | - | - | - | - | - | - | - | 
| value | yes | - | - | - | - | - | - | - | - | - | 

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

Table: study_link    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| name | varchar | 500 | yes | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | - | - | 
| study_link_id | integer | - | - | - | - | - | - | 
| value | varchar | 2000 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-user-defined-id-to-parent | - | [study_link, getAvailableUserDefinedIdsByParentTable, study_accession, study_accession] | [] | - | - | - | 



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
| Authors | authors |  |  |
| DOI | doi | Digital Object Identifier is a persistent identifier or handle used to uniquely identify an object. ImmPort DOIs are generated by DataCite (https://www.datacite.org/) | Digital Object Identifier is a persistent identifier or handle used to uniquely identify an object. |
| Issue | issue |  |  |
| Journal | journal | The journal name that publishes an article that includes data from this study. | The journal name that publishes an article that includes data from this study. |
| Month | month |  |  |
| Pages | pages |  |  |
| Pubmed ID | pubmed_id | The Pubmed or PubMedCentral identifier of an article that includes data from this study. | The Pubmed or PubMedCentral identifier of an article that includes data from this study. |
| Study ID | study_id | The study ID can be either the study user defined ID or a study accession. | The study ID can be either the study user defined ID or a study accession. |
| Title | title | The title of an article that includes data from this study. | The title of an article that includes data from this study. |
| Year | year |  |  |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| [study_accession, pubmed_id] | USER_DEFINED_ID | - | - | - | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| [study_accession, pubmed_id] | PRIMARY | study_pubmed | getAvailableUserDefinedIdsByParentTable | - | - | - | 

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
| study_id | yes | - | - | - | - | - | - | - | - | - | 
| title | - | - | - | - | - | - | - | - | - | - | 
| year | - | - | - | - | - | - | - | - | - | - | 

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
| study_accession | varchar | 15 | - | - | - | - | - | 
| title | varchar | 4000 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 
| year | varchar | 4 | yes | - | - | - | - | 

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-user-defined-id-to-parent | - | [study_pubmed, getAvailableUserDefinedIdsByParentTable, study_accession, study_accession] | [] | - | - | - | 



***
## Compound Template: **arm_or_cohort**

| Name | Value |
| --- | --- |
| Format | horizontal |
| Required | no |
| Multiple | yes |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Description | description | The description should expand any abbreviations used in the arm or cohort name. For example for an observational study with a cohort whose name was "ADEH+", the description would be "Atopic dermatitis with eczema herpeticum". | The description should expand any abbreviations used in the arm or cohort name. |
| Name | name | The arm or cohort name is not referenced by other data records. | The arm or cohort name is an alternate identifier that is visible when the study is shared. |
| Study ID | study_id | The study ID can be either the study user defined ID or a study accession. | The study ID can be either the study user defined ID or a study accession. |
| Type | type | For an interventional study, the type defines the treatment/control attributes of the arms. The attributes are selected from the values listed below (a study may have more than one arm of a given value). Clinical studies often use the following terms. Experimental - Arm for procedure or drug being evaluated. Active Comparator - arm receiving "standard of care" treatment. Placebo Comparator - arm receiving placebo treatment. Sham Comparator - arm receiving a sham procedure such as a surgery or a sham device. No Intervention - arm receiving neither "standard of care" treatment a placebo, or sham procedure or device. For an observational study, the type should be Observational - All arms are observing differences in cohorts | Example clinical study values: Observational, Experimental, Active Comparator, Placebo Comparator, Sham Comparator |
| User Defined ID | user_defined_id | The study's arm(s) or cohort(s) group subjects by criteria relevant to the study (e.g. age, condition) and/or treatments or interventions. Insert rows in the template to define additional arms or cohorts linked to the study. | The arm or cohort user defined ID is an identifier chosen by the data provider to refer to a subject grouping in the study document. This ID may be referenced by other data records (e.g. subjects). The user defined ID is not shared. |

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
| study_id | yes | - | - | - | - | - | - | - | - | - | 
| type | - | - | - | - | - | - | - | - | - | - | 
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

Table: arm_or_cohort    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| arm_accession | varchar | 15 | - | - | - | - | - | 
| description | varchar | 4000 | yes | - | - | - | - | 
| name | varchar | 126 | yes | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | - | - | 
| type | varchar | 20 | yes | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-child-to-parent-accession | - | [arm_or_cohort, accession-to-accession, getAvailableAccsToParentMap, arm_accession, study_accession] | [] | - | - | - | 



***
## Compound Template: **arm_2_subject**

| Name | Value |
| --- | --- |
| Format | horizontal |
| Required | no |
| Multiple | yes |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Age Event | age_event | A list of preferred terms is available. | Please choose from the drop down list. |
| Age Event Specify | age_event_specify | This column supports providing study milestones for subject's age determination that ImmPort does not support. | If "Age Event" = Other, this field specifies the age event (free text). Otherwise, leave this column blank. |
| Age Unit | age_unit | A list of preferred terms is available..  The age unit must conform to the age unit assigned to the study. | Please choose from the drop down list.  The age unit must conform to the age unit assigned to the study. |
| Arm Or Cohort ID | arm_or_cohort_id | A subject may be assigned to a single arm within a study. To link a subject to more than one study's arm, create a new record for each subject to arm link. | The arm or cohort ID can be either arm or cohort user defined ID or an arm or cohort accession. |
| Max Subject Age | max_subject_age | The subject age at the end of the study may be determined form one of several study milestones. | Please enter a number. |
| Min Subject Age | min_subject_age | The subject age at the outset of the study may be determined form one of several study milestones as indicated in the Age Event column. | Please enter a number. |
| Subject ID | subject_id | The subject ID can be either subject user defined ID or a subject accession. | The subject ID can be either subject user defined ID or a subject accession. |
| Subject Location | subject_location | A list of subject locations is available. | Please choose from the drop down list. |
| Subject Phenotype | subject_phenotype | The subject phenotype captures key aspects of the subject's disposition for the study. | Enter a description of the subject. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| [arm_accession, subject_accession] | USER_DEFINED_ID | - | - | - | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| [arm_accession, subject_accession] | PRIMARY | arm_2_subject | getAvailableUserDefinedIdsByParentTable | - | - | - | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| age_event | yes | - | lk_age_event | - | - | - | - | - | - | - | 
| age_event_specify | - | yes | - | - | - | - | - | - | - | - | 
| age_unit | yes | - | lk_time_unit | - | - | - | - | - | - | - | 
| arm_or_cohort_id | yes | - | - | - | - | - | - | - | - | - | 
| max_subject_age | - | - | - | - | - | - | - | - | float | - | 
| min_subject_age | yes | - | - | - | - | - | - | - | float | - | 
| subject_id | yes | - | - | - | - | - | - | - | - | - | 
| subject_location | - | - | lk_subject_location | - | - | - | - | - | - | - | 
| subject_phenotype | - | - | - | - | - | - | - | - | - | - | 

### Conditional Required Columns
| Column Name | CONDITION NAME | DATA ROW COLUMN | VALUE | 
|  --- | --- | --- | --- |
| age_event_specify | case-insensitive-equals | age_event | 'other' | 

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

Table: arm_2_subject    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| age_event | varchar | 50 | - | - | - | - | - | 
| age_event_specify | varchar | 50 | - | - | - | - | - | 
| age_unit | varchar | 50 | - | - | - | - | - | 
| arm_accession | varchar | 15 | - | - | - | - | - | 
| max_subject_age | float | - | - | - | - | - | - | 
| min_subject_age | float | - | - | - | - | - | - | 
| subject_accession | varchar | 15 | - | - | - | - | - | 
| subject_location | varchar | 50 | - | - | - | - | - | 
| subject_phenotype | varchar | 200 | - | - | - | - | - | 

### PostRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | LIST INPUT COLUMNS | LIST TABLE NAME | LIST VALIDATION QUERY NAME | 
|  --- | --- | --- | --- | --- | --- | --- |
| list type | check-value-not-in-entity | - | ['study_accession', 'subject_accession', 'arm_or_cohort'] | [subject_accession] | arm_or_cohort | getStudiesForSubjectAccNum | 


| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | LIST INPUT COLUMNS | LIST TABLE NAME | LIST VALIDATION QUERY NAME | 
|  --- | --- | --- | --- | --- | --- | --- |
| list type | check-value-in-entity | - | ['age_unit', 'study_accession', 'arm_2_subject'] | [study_accession] | study | getAgeUnitForStudy | 


### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [] | [min_subject_age] | [Action = set, Value = 90] | [Outputs = [description], Append Str = ;age rounded down to 90 by ImmPort Upload tool[ | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	case-insensitive-equals	age_unit	'years'
	greater-than	min_subject_age	'89'

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [] | [max_subject_age] | [Action = set, Value = 90] | [Outputs = [description], Append Str = ;age rounded down to 90 by ImmPort Upload tool[ | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	not-empty-value	max_subject_age	-
	case-insensitive-equals	age_unit	'years'
	greater-than	max_subject_age	'89'

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

### Controlled Vocabularies
| lk_age_event | lk_age_event | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 
| lk_subject_location | lk_subject_location | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 
| lk_time_unit | lk_time_unit | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 


***
## Compound Template: **planned_visit**

| Name | Value |
| --- | --- |
| Format | horizontal |
| Required | no |
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
| Study ID | study_id | The study ID can be either the study user defined ID or a study accession. | The study ID can be either the study user defined ID or a study accession. |
| User Defined ID | user_defined_id | The planned visit user defined ID is an identifier chosen by the data provider to refer to a protocol document. This ID may be referenced by other data records (e.g. biological samples). The user defined ID is not shared. Insert rows in the template to define additional planned visits linked to the study. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
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
| study_id | - | - | - | - | - | - | - | - | - | - | 
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
| study_accession | varchar | 15 | - | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PostRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | LIST INPUT COLUMNS | LIST TABLE NAME | LIST VALIDATION QUERY NAME | 
|  --- | --- | --- | --- | --- | --- | --- |
| list type | check-value-not-in-entity | - | ['order_number', 'study_accession', 'planned_visit'] | [study_accession] | planned_visit | getOrderColumnForStudy | 


### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [min_start_day] | [max_start_day] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	empty-value	max_start_day	-

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-child-to-parent-accession | - | [planned_visit, accession-to-accession, getAvailableAccsToParentMap, planned_visit_accession, study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-values-to-entity | - | [order_number, study_accession] | [] | - | - | - | 



***
## Compound Template: **study_personnel**

| Name | Value |
| --- | --- |
| Format | horizontal |
| Required | no |
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
| Site Name | site_name | Enter the site name if there is a need to further differentiate the affiliation of the study personnel form the Organization. | Enter the site name if there is a need to further differentiate the affiliation of the study personnel form the Organization. |
| Study ID | study_id | The study ID can be either the study user defined ID or a study accession. | The study ID can be either the study user defined ID or a study accession. |
| Suffixes | suffixes | Suffixes that are part of the study personnel's name being described. | Suffixes that are part of the study personnel's name being described. |
| Title In Study | title_in_study | The role the personnel play in the study as defined by the research team. | The role the personnel play in the study as defined by the research team. |
| User Defined ID | user_defined_id | The personnel user defined ID is an identifier chosen by the data provider to refer to personnel who may be contacted for more details about the study document. If more than one study personnel record is to be defined, copy the block of rows from Study_Personnel_ID to Site_Name for each additional study personnel record. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |

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
| study_id | yes | - | - | - | - | - | - | - | - | - | 
| suffixes | - | - | - | - | - | - | - | - | - | - | 
| title_in_study | yes | - | - | - | - | - | - | - | - | - | 
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
| study_accession | varchar | 15 | - | - | - | - | - | 
| suffixes | varchar | 40 | yes | - | - | - | - | 
| title_in_study | varchar | 100 | yes | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


### Controlled Vocabularies
| lk_personnel_role | lk_personnel_role | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 


***
## Compound Template: **inclusion_exclusion**

| Name | Value |
| --- | --- |
| Format | horizontal |
| Required | no |
| Multiple | yes |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Criterion | criterion | One or more criterion must be described to decide whether a subject may be enrolled in a study. | The criterion describes the parameter used to decide if a subject may be enrolled in a study. |
| Criterion Category | criterion_category | The criterion category is selected from a preferred list of terms. | There are two values to choose from: inclusion or exclusion. |
| Study ID | study_id | The study ID can be either the study user defined ID or a study accession. | The study ID can be either the study user defined ID or a study accession. |
| User Defined ID | user_defined_id | The inclusion or exclusion user defined ID is an identifier chosen by the data provider to refer to a criterion used to determine whether a subject may be enrolled in a study. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |

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
| study_id | yes | - | - | - | - | - | - | - | - | - | 
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

Table: inclusion_exclusion    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| criterion | varchar | 750 | yes | - | - | - | - | 
| criterion_accession | varchar | 15 | - | - | - | - | - | 
| criterion_category | varchar | 40 | - | - | - | - | - | 
| study_accession | varchar | 15 | - | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


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
| Required | no |
| Multiple | yes |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Protocol ID | protocol_id | The protocol ID for the study. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. It can be either a protocol user defined ID or an Accession. |
| Study ID | study_id | The study ID can be either the study user defined ID or a study accession. | The study ID can be either the study user defined ID or a study accession. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| [protocol_accession, study_accession] | USER_DEFINED_ID | - | - | - | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| [protocol_accession, study_accession] | PRIMARY | study_2_protocol | getAvailableUserDefinedIdsByParentTable | - | - | - | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| protocol_id | yes | - | - | - | - | - | - | - | - | - | 
| study_id | yes | - | - | - | - | - | - | - | - | - | 

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
| study_accession | varchar | 15 | - | - | - | - | - | 

### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-user-defined-id-to-parent | - | [study_2_protocol, getAvailableUserDefinedIdsByParentTable, study_accession, study_accession] | [] | - | - | - | 


