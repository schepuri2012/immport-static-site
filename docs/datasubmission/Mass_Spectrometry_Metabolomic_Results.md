# Template: **mass_spec_metabolomic_results**

| Name | Value |
| --- | --- |
| Template Type | multiple |
| Schema Version | 3.33 |
| Standard File Name | Mass_Spectrometry_Metabolomic_Results.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Comments | comments | Comments captures additional descriptive information that is added to the result. | Comments captures additional descriptive information that is added to the result. |
| Database ID Reported | database_id_reported | The Optional HMDB, PubChem, or RefMet ID associated with the result. Pick a value from the list if it fits the result. | The Optional Database ID (Human Metabalone Database (HMDB), PubChem, or RefMet ID) associated with the result. Pick a value from the list if it fits the result. |
| Expsample ID | expsample_id | The experiment sample identifier must be stored in ImmPort or in the experimentsamples.txt template. | Please enter either an experiment sample user defined ID or ImmPort accession. |
| Intensity | intensity | The intensity of the mass spectrometry result. | The intensity of the mass spectrometry result. |
| M/Z Ratio | m_z_ratio | The ratio of mass to Z charge. | The ratio of mass to Z charge. |
| Metabolite Name | metabolite_name_reported | The Optional name of the reported metabolite used in the mass spectrometry. | The Optional name of the reported metabolite used in the mass spectrometry. |
| Retention Time | retention_time | The retention time of the mass spectrometry result. | The retention time of the mass spectrometry result. |
| Retention Time Unit | retention_time_unit | The unit of time for the the retention time of the mass spectrometry result.  Please select a time unit name from the list provided. | The unit of time for the the retention time of the mass spectrometry result.  Please select a time unit name from the list provided. |
| Z (Charge) | z_charge | The Z charge of the mass spectrometry result. | The Z charge of the mass spectrometry result. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| result_id | KEY | result_id | - | mass_spectrometry_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| comments | - | - | - | - | - | - | - | - | - | - | 
| database_id_reported | - | - | - | lk_hmdb | database_id_preferred | - | - | - | - | - | 
| expsample_id | yes | - | - | - | - | - | - | - | - | - | 
| file_info_ids | - | - | - | - | - | - | yes | - | - | - | 
| intensity | yes | - | - | - | - | - | - | - | float | - | 
| m_z_ratio | yes | - | - | - | - | - | - | - | float | - | 
| mass_spectrometry_type | - | - | lk_mass_spectrometry_type | - | - | - | - | yes | - | metabolomics | 
| max_components | - | - | - | - | - | - | - | yes | - | 2 | 
| metabolite_name_reported | - | - | - | lk_hmdb | metabolite_name | - | - | - | - | - | 
| result_schemas | - | - | - | - | - | - | yes | - | - | - | 
| retention_time | yes | - | - | - | - | - | - | - | float | - | 
| retention_time_unit | yes | - | lk_time_unit | - | - | - | - | - | - | - | 
| z_charge | yes | - | - | - | - | - | - | - | - | - | 

### Foreign Key Information
FOREIGN KEY TYPE:	user-defined-id	Input column is a User Defined ID and the Output column is the Accession associated with User Defined ID in the given table if the input is a user defined ID

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | expsample_id | expsample_accession | expsample | getAvailableUserDefinedIdsMap | 

FOREIGN KEY TYPE:	accession	Input column is an Accession and the Output column is the Accession in the given table if the input is defined and an accession

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | expsample_id | expsample_accession | expsample | getAvailableAccsToParentMap | 

FOREIGN KEY TYPE:	accession-to-accession	Input column is an Accession and Output column is the parent Accession associated with the Accession in given table if the input column is defined and an accession

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | experiment_accession | study_accession | experiment | getAvailableAccsToParentMap | 

### Upload Table Information

Table: mass_spectrometry_result    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| comments | varchar | 500 | yes | - | - | - | - | 
| database_id_preferred | varchar | 25 | - | - | - | - | - | 
| database_id_reported | varchar | 50 | yes | - | - | - | - | 
| experiment_accession | varchar | 15 | - | - | - | - | - | 
| expsample_accession | varchar | 15 | - | - | - | - | - | 
| file_info_id | integer | - | - | - | - | result_file_info_id | - | 
| intensity | float | - | - | - | - | - | - | 
| m_z_ratio | float | - | - | - | - | - | - | 
| mass_spectrometry_type | varchar | 50 | - | - | - | - | - | 
| metabolite_name_preferred | varchar | 255 | - | - | - | - | - | 
| metabolite_name_reported | varchar | 255 | yes | - | - | - | - | 
| protein_name_preferred | varchar | 255 | - | - | - | - | - | 
| protein_name_reported | varchar | 255 | - | - | - | - | - | 
| result_id | integer | - | - | - | - | - | - | 
| retention_time | float | - | - | - | - | - | - | 
| retention_time_unit | varchar | 25 | - | - | - | - | - | 
| z_charge | varchar | 50 | yes | - | - | - | - | 

Table: expsample_2_file_info    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| expsample_accession | varchar | 15 | - | - | - | - | - | 
| file_info_id | integer | - | - | - | - | file_info_ids | yes | 
| result_schema | varchar | 50 | - | - | - | result_schemas | yes | 

### PostRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | check-result-schema-for-accession | - | ['expsample', 'expsample_accession', 'rs_result_schema', 'getEntityToResultSchemaMap'] | 


### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-semi-colon-if-needed | - | [database_id_reported, max_components, left] | [database_id_reported] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| break-into-components | - | [database_id_reported] | [metabolite_name, database_id_reported] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-template-file-name | - | [] | [result_file_name] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-file-info-ids | - | [result_file_name] | [result_file_info_id] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-file-info | - | [result_file_name, result] | [result_schema] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| get-result-schema-result | - | [] | [rs_result_schema] | - | - | - | 


### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-accession-to-file-info-for-result | Provided Below | [expsample_accession, result_file_info_id] | [file_info_id] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	not-empty-value	expsample_accession	-

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-data-to-lists | Provided Below | [file_info_id, result_schema] | [file_info_ids, result_schemas] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	not-empty-value	file_info_id	-

### Controlled Vocabularies
| lk_mass_spectrometry_type | lk_mass_spectrometry_type | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 
| lk_time_unit | lk_time_unit | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 
### Preferred Vocabularies

#### Column: database_id_reported Table: lk_hmdb

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | metabolite_name_reported | metabolite_name | metabolite_name | 
|  | database_id_reported | database_id_preferred | hmdb_id | 
|  |  | ANCILLARY DATA | 
|  |  | DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  |  | metabolite_name_preferred | metabolite_name | 


### Preferred Vocabulary Tables

#### lk_hmdb

| lk_hmdb | lk_hmdb | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | hmdb_id | metabolite_name | description | link | 
|  | DATABASE COLUMNS | hmdb_id | name | description | link | 


