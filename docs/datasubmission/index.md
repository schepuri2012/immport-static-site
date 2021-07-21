# Overview

## Standard Template Processing

Standard template file processing applies to template files of type single, multiple, compound, or result segment a combined templates. The processing for compound template files applies to each segment of the file assigned to a particular compound-template. For each data row, the following processing steps are applied.

```
A. Initial Processing Steps
        1. (Internal) Template used for processing data rows must be the one that created the data rows.
        2. Determine the validation_level. If the value is not defined in the template, then the value is set to Standard. The validation_level can be used in Conditions for differing levels of validation. Currently, the only other validation_level defined is Standard and HIPC.
        3. Add the Data Row to data rows to be processed and inserted into the database table(s)
        4. Set the line number of the data row for reporting purposes
B. Processing Steps
        1. Pre-Rules executed
        2. Pre-Processing executed
        3. Foreign Keys executed (user_defined_id and accession data are checked and pre-existing accessions are assigned)
        4. Files processing executed (only for templates that load files as part of table loads)
        5. For each Data Row, set the user_defined_id, accession, and ancillary accession(s) as necessary
                a. Do user_defined_id and accession testing
                b. Set the user_defined_id and accession
                c. Set the ancillary accession and ancillary user_defined_id, as necessary
                d. Add Workspace Tables, as necessary
        6. The key for the data row is the user_defined_id column, if specified, or a key column, if a Key is specified. The uniqueness of the user_defined_id or key is tested for duplicates.
        7. File Info Maps processing is executed
        8. Vocabulary Checks
                a. Controlled Vocabulary checks
                b. Preferred Vocabulary checks
        9. Post-Rules executed
        10. Post-Processing executed
        11. Miscellaneous Validation Checks
                a. Unique Column data column check besides the primary key for a data row
                b. Required data column(s) check
                c. Conditional Required data column(s)
                d. Numeric data column(s) check
C. Data Row Processing into table rows for insertion.
        Process each table as specified in the following order: ancillary tables, primary table, workspace tables, and linkage tables.
        A data row is transformed into one or more table rows as specified by the above XML structures and infra-structure data Upload Tables. The following checks are made to skip certain inserts:
                1. For a workspace table a key is defined, and a user_defined_id is repeated. Do not add table and workspace table rows for repeats
                2. If a set of Data Row Column names in the Data Row have empty values, then skip inserting the row into the table
                3. In the case that the table is a linkage table, it is part of a result template, and it does not have multiple columns, do not add duplicate row
        Finally, the database columns specified in Column Lengths are checked for column length against the database column lengths.
D. Process Save Files
        Process the save file.
```

## Template Loading Order

- protocols.txt
- reagents.array.txt
- reagents.elisa.txt
- reagents.elispot.txt
- reagents.mbaa.txt
- reagents.flow_cytometry.txt
- reagents.hai.txt
- reagents.cytof.txt
- reagents.neutralizing_antibody_titer.txt
- reagents.pcr.txt
- reagents.sequencing.txt
- reagents.virus_neutralization.txt
- reagents.hla_typing.txt
- reagents.kir_typing.txt
- reagents.other.txt
- reagent_sets.txt
- treatments.txt
- basic_study_design.txt
- subjectanimals.txt
- subjecthumans.txt
- study_design_edit.txt
- adverseevents.txt
- interventions.txt
- assessments.txt
- biosamples.txt
- labtestpanels.txt
- labtests.txt
- labtest_results.txt
- experiments.txt
- controlsamples.txt
- standardcurves.txt
- experimentsamples.flow_cytometry.txt
- experimentsamples.cytof.txt
- experimentsamples.gene_expression_array.txt
- experimentsamples.genotyping_array.txt
- experimentsamples.hla.txt
- experimentsamples.image_histology.txt
- experimentsamples.kir.txt
- experimentsamples.mbaa.txt
- experimentsamples.rna_sequencing.txt
- experimentsamples.other.txt
- experimentsamples.mass_spectrometry_metabolomics.txt
- experimentsamples.mass_spectrometry_proteomics.txt
- experimentsamples.elisa.txt
- experimentsamples.elispot.txt
- experimentsamples.hai.txt
- experimentsamples.virus_neutralization.txt
- experimentsamples.neutralizing_antibody_titer.txt
- experimentsamples.qrt-pcr.txt
- immuneexposure.txt
- publicrepositories.txt
- elisa_results.txt
- elispot_results.txt
- hai_results.txt
- pcr_results.txt
- virus_neutralization_results.txt
- hla_typing.txt
- kir_typing.txt
- rna_seq_results.txt
- mass_spectrometry_metabolomic_results.txt
- mass_spectrometry_proteomic_results.txt
- mbaa_results.txt
- fcm_derived_data.txt
- cytof_derived_data.txt	


## Upload Table Information

Data in the each Data Row is loaded into the a set of tables by the Batch Uploader for a template. The (internal) table FILE_INFO is loaded first so that its file_info_id values are known to the template processing. The order of loading tables is specified by the order of the upload tables for the template, that is, the Ancillary Tables, Primary Template Table, Workspace Tables, and Linkage Tables. The Primary Table defines the uniqueness of each Data Row in the template ile. Each Data Row can cause a table to load zero or more table rows. If Empty Data Row Columns are specified for a given table, then for given Data Row either the row is load nor not. If all of the Data Row Column values in the Empty Data Row Columns are empty values for the Data Row, then the Data Row is not loaded into the table, otherwise it is. The Multiple Columns allows for a table to load multiple rows to a table for a given template file Data Row. In this case, the database columns that will have varying data for the different table rows needs to be matched with a Data Row Column that represents a list as specified in the Template using List Columns. If there are a set of database column mappings to list Data Row Column, then each list must be the same length and each index in the list represents a database row for the given table. The Column Mappings list provides a mechanism for mapping the database column name to a Data Row Column value so that the database column values can be determined. In most cases, the data row columns already defined for the Template are also database column names for the tables to be loaded. In this case, the DATA ROW COLUMN is a hyphen ('-'). However, there can be cases where this is not possible for the set of tables being loaded for a given Template and they are explicitly specified.  Also, Table column checks include column length restrictions. Finally, the Batch Uploader needs to know which tables contain clob columns to specify the insert correctly.  The audit columns for the tables are not explicitly specified (created_by, last_updated_by, upload_ticket_number) in the requirement document since they are evaluated internally by the Batch Uploader

## Controlled Vocabulary

A controlled vocabulary check (Control) consists of checking an input Data Row Column value with a controlled vocabulary list generated from the Lookup Table Name using the specification for the Table Name in Lookup Tables. The check uses case-insensitive check and returns the controlled vocabulary case spelling into the input Data Row Column value. If the check fails and error message is generated, and the validation fails. The LookupTables are used in conjunction with Controlled Vocabulary/Control XML component for checking (case-insensitive) conformance to a controlled vocabulary and for replacing a conformant value with the correct case spelling. For a given Data Content, the column with Alias column name ‘name’ is associated with a database column from which the controlled vocabulary list is generated. There are also Data Content in Lookup Tables that are used only for preferred population marker parsing (See immport-api-docs Population Marker Parsing Tutorial). Finally, there is the lookup Data Content, lk_template_mapping, specified earlier in the document that is used for the determination of information on result files to load into database table file_info and for the generation of path expressions for storing these files into the file system. There is other database column information in the Data Content. This information is used in the generation of the PDF document describing the ImmPort templates.

## Key and User Defined ID Information

The User Defined ID and Key are used for duplicate check within the template file. If two data rows have the same user defined id column value or key column value, then an error is generated. If the user defined ID is defined, then it is used for duplicate checking, otherwise the Key is used. Also, a the user defined ID is used to determine is the data row has been previously loaded into the database. The user defined ID or key is the catenation (using ‘:’) of the data row column values defining the user defined ID. If a user defined ID is provided, then in most cases a corresponding Accession (exceptions exist in study_design_edit). If Key is provided, then an Accession may be provided.

## Conditions

A condition returns either true or false.  If a value is given, the the conditions tests a data row column against the given value and returns either true satisfying the condition being tested or false if it does not satisfy the condition.  If no value is provided, then the condition tests a characteristic of the data row value.

## Rule

A rule is a test that needs to return 'true' to be satisfied. A rule either succeeds (true) or fails (false). When s rule is executed, it will return either true or false based on the rule type.  A rule is executed only if all it conditions return true or there are not conditions. If a rule fails, then the validation fails, an error message is generated into the log, and the upload will not occur.

## Process

A Process is a function that takes input data row column(s), performs a transformation and optionally outputs data row column(s).  Optionally, a process has a set of conditions.  The process is executed only if all conditions are true or there are no conditions.  For set-to-value Process, it can optionally contain a <ProcessOutput> instead of <Input> data row column(s).  The ProcessOutput specifies an action (currently set) and a value.  Optionally, a Process can have an <AppendOutput> which allows an append string to be append to data row column value(s) specified in the <AppendOutput>

## Validation Queries

Validation Queries are essential for testing the integrity of the upload, ensuring that foreign keys are satisfied before templates can be validated and associated database tables are loaded. Also, validation queries provide for the integrity of table content with respect to user defined IDs and accessions. The Database Table Infos and Validation Queries XML components provide the information for generating SQL queries and processing the results into structures for validation testing in many contexts in the templates as specified below.  All validation Queries require the workspace ID as the parameter input to the SQL query.

The Database Table Infos provide the substitution column names to values in evaluating a validation query into executable SQL. The standard set of substitution column names used in validation queries include the following: TableName, ParentTable, WorkspaceTableName, UserDefinedIdColumn, SelfAccession, ParentAccession, and optionally either OrderColumn or ResultSchemaColumn.

The Validation Queries provide the specification of all the validation queries (Validation Query) used in the Batch Uploader. A validation query (Validation Query) consists of a Name that is used throughout the specification of the Templates to identify a validation query.

The validation query has a SQL string (Sql tag) that contains the Substitution column names defined in Database Table Infos for the given table associated with a validation query in a Template. Also, each SQL query depends on a workspace_id parameter that must be provided to the query for execution. The ColumnNames ColumnName columns map to the columns defined in the SQL query result. Each validation query has an OutParam. This tag defines how to interpret the results of executing the query. The current OutParam tag values include:


 - HashMap
     - The output consists of a HashMap with the key defined by the first ColumnName in ColumnNames, and value consists of the rest of the ColumnName in ColumnNames. If the rest of the ColumnNames ColumnName columns is a single column, then the value is a string defined by this ColumnName. However, if there are several ColumnName columns, then the value is a HashMap where the keys are the ColumnName names, and the values are the column values in the result.

- HashMap_List
     - The output consists of a HashMap with the key defined by the first ColumnName in ColumnNames. The value of the HashMap is a list. The HashMap is constructed as follows. For each result row, the value of the second column is added to the list defined by the first column value.

- List
    - The result is a list of values where each result is a single column value.

## File Info Information

File checks are used by Templates to save files in the file system and record their information in various tables. Result files have differing file types (File Type). This XML component allows result files specified by the DataRowColumn value to be assigned a file_detail. The Template Name, the file_name (DataRowColumn value), File Type determine the file type using this triple (Template Name, file_name, File Type) and the lk_template_mapping table as specified in Lookup Tables XML component. The file_name, file_detail and the study_accession (Study Accession Column value) is used to store these files into file_info table (file_info template) and into the file system.

## Save File Information

File checks are used by Templates to save files in the file system and record their information in various tables. Save a File as Part of the Table Load. The following database tables and their associated templates are processed using the XML structures specified below to identify (File) and save files (SaveFile) into the file system. file_info - ImmPortData/ImmPort.DataUpload.FileInfo.xml, protocol - Templates/ImmPort.DataUpload.protocols.xml, study_file - Templates/ImmPort.DataUpload.basic_study_design.xml and Templates/ImmPort.DataUpload.study_design_edit.xml, and study_image - Templates/ImmPort.DataUpload.study_design_edit.xml. The Path Name is generated using the following processes. in the respective templates: file_info - create-file-info-path-expression, protocol - create-protocol-path-expression, study_file - create-study-file-path-expression, and study_image - create-study-image-path-expression.