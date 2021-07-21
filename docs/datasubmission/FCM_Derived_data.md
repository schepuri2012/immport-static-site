# Template: **fcm_derived_data**

| Name | Value |
| --- | --- |
| Template Type | multiple |
| Schema Version | 3.33 |
| Standard File Name | FCM_Derived_data.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Comments | comments | Comments captures additional descriptive information. | Comments captures additional descriptive information. |
| Expsample ID | expsample_id | The experiment sample identifier must be stored in ImmPort or in the experimentsamples.txt template. | Please enter either an experiment sample user defined ID or ImmPort accession. |
| Parent Population Reported | parent_population_reported | The drop down provides the base parent population. Please select a name if it matches your base parent population name or enter a name if there is not an appropriate one provided.  This column can also have the format: "lineage_prefix ; population name", "population_name&modifiers", or "lineage_prefix ; population_name&modifiers". Also, if the Parent Population Reported does not occur in the drop down, it will be tested against the lk_cell_population_pref_map to determine a preferred name. | The base parent population name. Please select a population name from the drop down list if it matches your base parent population name or enter a name if there is not an appropriate one provided.  This column can also have the format: "lineage_prefix ; population name", "population_name&modifiers", or "lineage_prefix ; population_name&modifiers" . Also, if the Parent Population eported does not occur in the drop down, it will be tested against the lk_cell_population_pref_map to determine a preferred name. |
| Gating Definition Reported | population_defnition_reported | he gating definition is the set of markers and their expression profile that describes a cell population name. Please select a gating definition from the drop down list if it matches your gating definition or enter a gating definition if there is not an appropriate one provided. The marker names should conform to standard names as described in the LK_ANALYTE table. Note that a comma, forward slash or pipe may be used as marker delimiter. The expression values are '-', '+', '+-', '+~', '++', or ''. The gating definition has a limit of 150 characters. | The gating definition is the set of markers and their expression profile. Please select a gating definition from the drop down list or enter a gating definition. Please see the ImmPort Upload Templates for details on representing marker names, delimiters and expression values. |
| Population Name Reported | population_name_reported | The drop down list provides a list of cell population names. Please select a name if it matches your cell population name or enter a population name if there is not an appropriate one provided. The population name has a limit of 150 characters.  This column can also have the format: "lineage_prefix ; population name", "population_name&modifiers", or "lineage_prefix ; population_name&modifiers". Also, if the Population Name Reported does not occur in the drop down, it will be tested against the lk_cell_population_pref_map to determine a preferred name. | The population name is the type of cells whose count is reported. Please select a population name from the drop down list if it matches your cell population name or enter a name if there is not an appropriate one provided.  This column can also have the format: "lineage_prefix ; population name", "population_name&modifiers", or "lineage_prefix ; population_name&modifiers". Also, if the Population Name Reported does not occur in the drop down, it will be tested against the lk_cell_population_pref_map to determine a preferred name. |
| Population Stat Unit Reported | population_stat_unit_reported | The unit used to describe the cell count. Please select a unit from the drop down list if the definition matches your unit name or enter a unit if there is not an appropriate one provided. | The unit used to describe the cell count. Please select a unit from the list provided if the definition matches your unit name or enter a unit if there is not an appropriate one provided. |
| Population Statistic (count, percentile, etc) | population_statistic_reported | The count of the cell type defined by the marker gating definition. | A number is expected. |
| Workspace File | workspace_file | An XML formatted export of the analysis program is expected (e.g. an xml format of a FlowJo .jo or .wsp file). The file size name limit is 240 characters. | The name of the file that stores the interpreted flow cytometry results from the analysis program. The file size name limit is 240 characters. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| result_id | KEY | result_id | - | fcs_analyzed_result_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| comments | - | - | - | - | - | - | - | - | - | - | 
| expsample_id | yes | - | - | - | - | - | - | - | - | - | 
| fcs_analyzed_result_marker_ids | - | - | - | - | - | - | yes | - | - | - | 
| file_info_ids | - | - | - | - | - | - | yes | - | - | - | 
| global.fcs_analyzed_result_marker_id | - | - | - | - | - | yes | - | - | - | fcs_analyzed_result_marker_seq | 
| max_components | - | - | - | - | - | - | - | yes | - | 2 | 
| parent_population_prefix | - | - | - | lk_cell_population | parent_population_prefix_preferred | - | - | - | - | - | 
| parent_population_reported | - | - | - | lk_cell_population | parent_population_preferred | - | - | - | - | - | 
| population_defnition_reported | yes | - | - | lk_cell_population_definition | population_definition_preferred | - | - | - | - | - | 
| population_marker_accessions | - | - | lk_analyte_population_marker | - | - | - | yes | - | - | - | 
| population_marker_preferreds | - | - | - | - | - | - | yes | - | - | - | 
| population_marker_reporteds | - | - | - | - | - | - | yes | - | - | - | 
| population_marker_types | - | - | - | - | - | - | yes | - | - | - | 
| population_name_prefix | - | - | - | lk_cell_population | population_prefix_preferred | - | - | - | - | - | 
| population_name_reported | yes | - | - | lk_cell_population | population_name_preferred | - | - | - | - | - | 
| population_stat_unit_reported | yes | - | - | lk_cell_pop_statistic_unit | population_stat_unit_preferred | - | - | - | - | - | 
| population_statistic_preferred | - | - | - | - | - | - | - | - | float | - | 
| population_statistic_reported | yes | - | - | - | - | - | - | - | - | - | 
| result_schemas | - | - | - | - | - | - | yes | - | - | - | 
| workspace_file | yes | - | - | - | - | - | - | - | - | - | 

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

### File Info Information

| FILE NAME COLUMN | FILE TYPE | STUDY ACCESSION COLUMN | 
|  --- | --- | --- |
| workspace_file | result | study_accession | 

### Upload Table Information

Table: fcs_analyzed_result    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| comments | varchar | 500 | yes | - | - | - | - | 
| experiment_accession | varchar | 15 | - | - | - | - | - | 
| expsample_accession | varchar | 15 | - | - | - | - | - | 
| file_info_id | integer | - | - | - | - | result_file_info_id | - | 
| parent_population_modifier | varchar | 150 | - | - | - | - | - | 
| parent_population_preferred | varchar | 150 | - | - | - | - | - | 
| parent_population_reported | varchar | 150 | yes | - | - | - | - | 
| population_defnition_preferred | varchar | 150 | yes | - | - | - | - | 
| population_defnition_reported | varchar | 150 | yes | - | - | - | - | 
| population_name_modifier | varchar | 150 | - | - | - | - | - | 
| population_name_preferred | varchar | 150 | - | - | - | - | - | 
| population_name_reported | varchar | 150 | yes | - | - | - | - | 
| population_stat_unit_preferred | varchar | 50 | - | - | - | - | - | 
| population_stat_unit_reported | varchar | 100 | yes | - | - | - | - | 
| population_statistic_preferred | float | - | - | - | - | - | - | 
| population_statistic_reported | varchar | 50 | yes | - | - | - | - | 
| result_id | integer | - | - | - | - | - | - | 
| workspace_file_info_id | integer | - | - | - | - | - | - | 

Table: expsample_2_file_info    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| expsample_accession | varchar | 15 | - | - | - | - | - | 
| file_info_id | integer | - | - | - | - | file_info_ids | yes | 
| result_schema | varchar | 50 | - | - | - | result_schemas | yes | 

Table: fcs_analyzed_result_marker    Type: linkage

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| fcs_analyzed_result_marker_id | integer | - | - | - | - | fcs_analyzed_result_marker_ids | yes | 
| population_marker_preferred | varchar | 500 | yes | - | - | population_marker_preferreds | yes | 
| population_marker_reported | varchar | 500 | yes | - | - | population_marker_reporteds | yes | 
| preferred_analyte_accession | varchar | 15 | - | - | - | population_marker_accessions | yes | 
| result_id | integer | - | - | - | - | - | - | 

### PostRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | check-population-markers | Provided Below | ['population_marker_reporteds', 'population_marker_preferreds', 'population_marker_accessions', 'population_marker_types', 'population_defnition_reported'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		case-insensitive-equals	validation_level	'HIPC'

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | check-result-schema-for-accession | - | ['expsample', 'expsample_accession', 'rs_result_schema', 'getEntityToResultSchemaMap'] | 


### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| generate-fcs-analyzed-result-markers | - | [expsample_id, population_defnition_reported] | [population_marker_reporteds, population_marker_preferreds, population_marker_accessions, population_marker_types] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| assign-result-id | - | [population_marker_reporteds, global.fcs_analyzed_result_marker_id] | [fcs_analyzed_result_marker_ids] | - | - | - | 


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


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| convert-to-float | - | [population_statistic_reported] | [population_statistic_preferred] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-semi-colon-if-needed | - | [population_name_reported, max_components, left] | [population_name_reported] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| break-into-components | - | [population_name_reported] | [population_name_prefix, population_name_reported] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-semi-colon-if-needed | - | [parent_population_reported, max_components, left] | [parent_population_reported] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| break-into-components | - | [parent_population_reported] | [parent_population_prefix, parent_population_reported] | - | - | - | 


### PostProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-and-check-study-accession | - | [study_accession] | [] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| determine-file-info-ids | - | [workspace_file] | [workspace_file_info_id] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-accession-to-file-info-for-result | - | [expsample_accession, workspace_file_info_id] | [final.workspace_file_info_id] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-file-info | - | [workspace_file, result] | [workspace_result_schema] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-data-to-lists | Provided Below | [final.workspace_file_info_id, workspace_result_schema] | [file_info_ids, result_schemas] | - | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	not-empty-value	final.workspace_file_info_id	-

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

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| update-population-defnition-preferred | - | [population_marker_reporteds, population_marker_preferreds, population_defnition_reported] | [population_defnition_preferred] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| process-population-name | - | [population_name_reported, population_name_preferred, lk_cell_population, lk_cell_population_pref_map, population_name_preferred] | [population_name_reported, population_name_preferred, population_name_modifier] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| process-population-name | - | [parent_population_reported, parent_population_preferred, lk_cell_population, lk_cell_population_pref_map, population_name_preferred] | [parent_population_reported, parent_population_preferred, parent_population_modifier] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-preferred-value | - | [lk_cell_population_pref_map, population_name_reported, population_name_preferred] | [population_name_reported, population_name_preferred] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-preferred-value | - | [lk_cell_population_pref_map, parent_population_reported, parent_population_preferred] | [parent_population_reported, parent_population_preferred] | - | - | - | 


### Controlled Vocabularies
| lk_analyte_population_marker | lk_analyte | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | analyte_accession | protein_ontology_name | link | 
### Preferred Vocabularies

#### Column: population_name_reported Table: lk_cell_population

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | population_name_prefix | population_prefix_preferred | population_prefix_preferred | 
|  | population_name_reported | population_name_preferred | population_name_preferred | 

#### Column: parent_population_reported Table: lk_cell_population

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | parent_population_prefix | parent_population_prefix_preferred | population_prefix_preferred | 
|  | parent_population_reported | parent_population_preferred | population_name_preferred | 

#### Column: population_defnition_reported Table: lk_cell_population_definition

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | population_defnition_reported | population_definition_preferred | population_defnition_preferred | 

#### Column: population_stat_unit_reported Table: lk_cell_pop_statistic_unit

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | population_stat_unit_reported | population_stat_unit_preferred | statistic_unit_preferred | 


### Preferred Vocabulary Tables

#### lk_cell_pop_statistic_unit

| lk_cell_pop_statistic_unit | lk_unit_of_measure | database | type in ('derived_flow','Not_Specified') | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | statistic_unit_preferred | description | link | 
|  | DATABASE COLUMNS | name | description | link | 

#### lk_cell_population

| lk_cell_population | lk_cell_population | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | population_name_preferred | population_prefix_preferred | description | link | 
|  | DATABASE COLUMNS | name | lineage_prefix | description | link | 

#### lk_cell_population_definition

| lk_cell_population_definition | lk_cell_population | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | population_defnition_preferred | description | link | 
|  | DATABASE COLUMNS | definition | description | link | 


