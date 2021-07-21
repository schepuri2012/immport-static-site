# Template: **cytof_reagents**

| Name | Value |
| --- | --- |
| Template Type | multiple |
| Schema Version | 3.33 |
| Standard File Name | reagents.CyTOF.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Analyte Reported | analyte_reported | The analyte describes what is being measured in an assay. The list of values displays common immunology gene symbol and gene symbol terms on the left and their preferred term on the right, each component separated by a semi-colon. Please select a name from the list provided if the name matches your name or enter a name if there is not an appropriate one provided. This name is visible when the result is shared. | The analyte is the target (e.g protein, DNA, RNA) that is being assayed by the reagent. Please select a name from the list provided if the name matches your name or enter a name if there is not an appropriate one provided. This name is visible when the result is shared. |
| Antibody Registry ID | antibody_registry_id |  | The identifier assigned by the Antibody Registry to the antibody reagent. http://antibodyregistry.org/ |
| Catalog Number | catalog_number | The reagent's catalog ID provides a reference to the reagent source and description. | If the assay reagent is a commercial product, enter the vendor's catalog identifier. If the reagent is a custom preparation enter 'NA'. |
| Clone Name | clone_name | Mass cytometry reagents often consist of a monoclonal antibody linked to a isotope and the antibody binds to the target analyte. | The detector in mass cytometry reagents is often a monoclonal antibody conjugated to an isotope. When there is no antibody in the reagent, enter 'NA'. |
| Contact | contact | If the reagent is from a non-commercial source, the contact information should indicate with whom to communicate to get further details. | The contact information is particularly helpful when the reagent is not from a commercial vendor. |
| Description | description | The assay reagent description provides further details on the nature and purpose of the reagent. | A supplemental description of the assay reagent that expands on its Name and User Defined ID. |
| Lot Number | lot_number | The lot number is helpful to understand possible batch specific differences in assay results. | The lot number is often provided by a reagent source when the reagent is replenished over time. |
| Manufacturer | manufacturer | The source of a reagent may be important for evaluating assay results. | The manufacturer is the source of a reagent and may include commercial vendors as well as non-commercial sources (e.g. collaborating labs). |
| Name | name | The reagent name is not referenced by other data records. | The reagent name is an alternate ID that is shared. |
| Reporter Name | reporter_name | Mass cytometry reagents often consist of a monoclonal antibody linked to an isotope and the isotope provides the signal for the mass spectrometer's detectors. | The reporter in a mass cytometry reagent is the isotope linked to an antibody. |
| User Defined ID | user_defined_id | The reagent user defined ID is an identifier chosen by the data provider to refer to an assay reagent. The nature of the assay reagent is assay specific and may be an array, an antibody or a typing kit. This ID may be referenced by other data records (e.g. experiment sample). The user defined ID is not shared. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |
| Weblink | weblink | The web link is often the vendor's web site. | An internet address that may provide details of an assay reagent. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| user_defined_id | USER_DEFINED_ID | reagent_accession | ESR | reagent_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| user_defined_id | PRIMARY | reagent | getAvailableUserDefinedIdsMap | reagent_accession | ESR | reagent_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| analyte_reported | yes | - | - | lk_analyte | analyte_preferred | - | - | - | - | - | 
| antibody_registry_id | - | - | - | - | - | - | - | - | - | - | 
| catalog_number | yes | - | - | - | - | - | - | - | - | - | 
| clone_name | yes | - | - | - | - | - | - | - | - | - | 
| contact | - | - | - | - | - | - | - | - | - | - | 
| description | - | - | - | - | - | - | - | - | - | - | 
| immunology_symbol | - | - | - | lk_analyte | immunology_symbol | - | - | - | - | - | 
| is_set | - | - | - | - | - | - | - | yes | - | N | 
| lot_number | - | - | - | - | - | - | - | - | - | - | 
| manufacturer | yes | - | - | - | - | - | - | - | - | - | 
| max_components | - | - | - | - | - | - | - | yes | - | 3 | 
| name | - | - | - | - | - | - | - | - | - | - | 
| reporter_name | yes | - | - | - | - | - | - | - | - | - | 
| short_label | - | - | - | lk_analyte | short_label | - | - | - | - | - | 
| type | - | - | lk_reagent_type | - | - | - | - | yes | - | CyTOF | 
| user_defined_id | yes | - | - | - | - | - | - | - | - | - | 
| weblink | - | - | - | - | - | - | - | - | - | - | 

### Upload Table Information

Table: reagent    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| analyte_preferred | varchar | 15 | - | - | - | - | - | 
| analyte_reported | varchar | 200 | yes | - | - | - | - | 
| antibody_registry_id | varchar | 250 | yes | - | - | - | - | 
| catalog_number | varchar | 250 | yes | - | - | - | - | 
| clone_name | varchar | 200 | yes | - | - | - | - | 
| contact | varchar | 1000 | yes | - | - | - | - | 
| description | varchar | 4000 | yes | - | - | - | - | 
| is_set | varchar | 1 | - | - | - | - | - | 
| lot_number | varchar | 250 | yes | - | - | - | - | 
| manufacturer | varchar | 100 | yes | - | - | - | - | 
| name | varchar | 200 | yes | - | - | - | - | 
| reagent_accession | varchar | 15 | - | - | - | - | - | 
| reporter_name | varchar | 200 | yes | - | - | - | - | 
| type | varchar | 50 | - | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | - | - | 
| weblink | varchar | 250 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: workspace_2_reagent    Type: workspace

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| reagent_accession | varchar | 15 | - | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| add-semi-colon-if-needed | - | [analyte_reported, max_components, left] | [analyte_reported] | - | - | - | 


| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| break-into-components | - | [analyte_reported] | [immunology_symbol, short_label, analyte_reported] | - | - | - | 


### Controlled Vocabularies
| lk_reagent_type | lk_reagent_type | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 
### Preferred Vocabularies

#### Column: analyte_reported Table: lk_analyte

|  | REPORTED DATA ROW COLUMN | PREFERRED DATA ROW COLUMN | XML PREFERRED TABLE COLUMN | 
|  --- | --- | --- | --- |
|  | immunology_symbol | immunology_symbol | immunology_symbol | 
|  | short_label | short_label | short_label | 
|  | analyte_reported | analyte_preferred | analyte_preferred | 


### Preferred Vocabulary Tables

#### lk_analyte

| lk_analyte | lk_analyte | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | analyte_preferred | immunology_symbol | official_gene_name | id | gene_symbol | description | short_label | link | 
|  | DATABASE COLUMNS | analyte_accession | immunology_symbol | official_gene_name | gene_id | gene_symbol | protein_ontology_name | protein_ontology_short_label | link | 

