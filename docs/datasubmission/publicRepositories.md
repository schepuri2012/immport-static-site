# Template: **public_repositories**

| Name | Value |
| --- | --- |
| Template Type | single |
| Schema Version | 3.33 |
| Standard File Name | publicRepositories.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Expsample ID | expsample_id | The experiment sample user defined ID is an identifier chosen by the data provider to refer to this sample. This ID may be referenced by other data records (e.g. assay results). The user defined ID is not shared. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |
| Repository Accession | repository_accession | The public repository accession should be the most granular or highest resolution provided (e.g. sample level accession, not sample group accession). | Enter the accession that links to the assay result file(s). |
| Repository Name | repository_name | ImmPort expects array gene expression results to be deposited in NCBI GEO since this is a prerequisite for publication. Please choose this repository name from the list. | Array gene expression results are expected to be deposited in NCBI GEO Please choose this repository name from the list. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| [expsample_accession, repository_accession] | KEY | result_id | - | expsample_public_repos_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| expsample_id | yes | - | - | - | - | - | - | - | - | - | 
| repository_accession | yes | - | - | - | - | - | - | - | - | - | 
| repository_name | yes | - | lk_public_repository | - | - | - | - | - | - | - | 

### Foreign Key Information
FOREIGN KEY TYPE:	user-defined-id	Input column is a User Defined ID and the Output column is the Accession associated with User Defined ID in the given table if the input is a user defined ID

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | expsample_id | expsample_accession | expsample | getAvailableUserDefinedIdsMap | 

FOREIGN KEY TYPE:	accession	Input column is an Accession and the Output column is the Accession in the given table if the input is defined and an accession

|  | INPUT COLUMN | OUTPUT COLUMN | TABLE NAME | VALIDATION QUERY | 
|  --- | --- | --- | --- | --- |
|  | expsample_id | expsample_accession | expsample | getAvailableAccsToParentMap | 

### Upload Table Information

Table: expsample_public_repository    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| expsample_accession | varchar | 15 | - | - | - | - | - | 
| repository_accession | varchar | 20 | - | - | - | - | - | 
| repository_name | varchar | 50 | - | - | - | - | - | 
| result_id | integer | - | - | - | - | - | - | 

### PostRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | LIST INPUT COLUMNS | LIST TABLE NAME | LIST VALIDATION QUERY NAME | 
|  --- | --- | --- | --- | --- | --- | --- |
| list type | check-value-not-in-entity | - | ['repository_accession', 'expsample_accession', 'expsample_public_repository'] | [expsample_accession] | expsample_public_repository | getPublicRepositoriesForExpsampleAccession | 


### Controlled Vocabularies
| lk_public_repository | lk_public_repository | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 

