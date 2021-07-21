# Template: **treatments**

| Name | Value |
| --- | --- |
| Template Type | single |
| Schema Version | 3.33 |
| Standard File Name | treatments.txt |


### Template Columns

| Template Column Name | Data Row Column Name | Description | Comment |
| --- | --- | --- | --- |
| Amount Unit | amount_unit | The amount unit preferred terms list has commonly used units. If additional units are needed, please contact the ImmPort HelpDesk. | The unit should be selected from the drop down list. |
| Amount Value | amount_value | The value should be a number. | The Amount Value indicates how much (concentration, mass, volume) of a treatment agent was applied to a sample. |
| Comments | comments | The Comments column allows the data provider to provide additional descriptive information. | Please provide additional comments as needed. |
| Duration Unit | duration_unit | The duration unit preferred terms list has commonly used units. If additional units are needed, please contact the ImmPort HelpDesk. | The unit should be selected from the drop down list. |
| Duration Value | duration_value | The Duration Value indicates how long a treatment agent was applied to a sample. | The value should be a number. |
| Name | name | The treatment name is not referenced directly by other data records. The name should be an informative to a researcher reviewing the data. Treatments may be referenced by more than one biological or experiment sample. There are three categories to describe the molecular content, time and/or temperature applied in a sample treatment. You may enter data for amount, duration or temperature only any combination of these categories (e.g. amount and duration). | Treatments refer to in vitro modifications of samples. The treatment name is an alternate identifier that is visible when the treatment is shared. |
| Temperature Unit | temperature_unit | The temperature unit preferred terms list has commonly used units. If additional units are needed, please contact the ImmPort HelpDesk. | The unit should be selected from the drop down list. |
| Temperature Value | temperature_value | The Temperature Value indicates how long a treatment agent was applied to a sample. | The value should be a number. |
| Use Treatment? | use_treatment | If 'No' is selected, you must enter a value in the Treatment User Defined ID and Name columns and that is all. If 'Yes' is selected, you must enter a value in the Treatment User Defined ID and Name columns and the value/unit pair of columns for amount or duration or temperature. | Was a treatment applied to a sample? |
| User Defined ID | user_defined_id | The treatment user defined ID is an identifier chosen by the data provider to refer to a treatment agent which can be a molecule, time or temperature. This ID may be referenced by other data records (e.g. study). The user defined ID is not shared. | The identifier should be unique to the ImmPort workspace to which the data will be uploaded. |

### Template Key Information
| DATA ROW COLUMN(S) | TYPE | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- |
| user_defined_id | USER_DEFINED_ID | treatment_accession | TRT | treatment_seq | 

### User Defined ID Information
| DATA ROW COLUMN | TYPE | TABLE NAME | VALIDATION QUERY | ACCESSION COLUMN | ACCESSION PREFIX | ACCESSION SEQUENCE | 
|  --- | --- | --- | --- | --- | --- | --- |
| user_defined_id | PRIMARY | treatment | getAvailableUserDefinedIdsMap | treatment_accession | TRT | treatment_seq | 

### Data Row Column Information
| DATA ROW COLUMN NAME | REQUIRED | CONDITIONAL REQUIRED | CONTROLLED VOCABULARY | PREFERRED VOCABULARY | PREFERRED DATA ROW COLUMN | GLOBAL | LIST | CONSTANT | NUMERIC TYPE | VALUE | 
|  --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| amount_unit | - | - | lk_amount_unit | - | - | - | - | - | - | - | 
| amount_value | - | - | - | - | - | - | - | - | - | - | 
| comments | - | - | - | - | - | - | - | - | - | - | 
| duration_unit | - | - | lk_time_unit | - | - | - | - | - | - | - | 
| duration_value | - | - | - | - | - | - | - | - | - | - | 
| name | yes | - | - | - | - | - | - | - | - | - | 
| temperature_unit | - | - | lk_temperature_unit | - | - | - | - | - | - | - | 
| temperature_value | - | - | - | - | - | - | - | - | - | - | 
| use_treatment | yes | - | lk_yes_no | - | - | - | - | - | - | - | 
| user_defined_id | yes | - | - | - | - | - | - | - | - | - | 

### Upload Table Information

Table: treatment    Type: primary

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| amount_unit | varchar | 50 | - | - | - | - | - | 
| amount_value | varchar | 50 | yes | - | - | - | - | 
| comments | varchar | 500 | yes | - | - | - | - | 
| duration_unit | varchar | 50 | - | - | - | - | - | 
| duration_value | varchar | 200 | yes | - | - | - | - | 
| name | varchar | 100 | yes | - | - | - | - | 
| temperature_unit | varchar | 50 | - | - | - | - | - | 
| temperature_value | varchar | 50 | yes | - | - | - | - | 
| treatment_accession | varchar | 15 | - | - | - | - | - | 
| user_defined_id | varchar | 100 | yes | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

Table: workspace_2_treatment    Type: workspace

| COLUMN NAME | COLUMN TYPE | COLUMN LENGTH | COLUMN LEN CHECK | CLOB CHECK | EMPTY DATA ROW COLUMNS | DATA ROW COLUMN | MULITPLE ROWS | 
|  --- | --- | --- | --- | --- | --- | --- | --- |
| treatment_accession | varchar | 15 | - | - | - | - | - | 
| workspace_id | integer | - | - | - | - | - | - | 

### PreRules (in order):

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | all-empty-or-nonempty | - | ['amount_value', 'amount_unit'] | 


| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | all-empty-or-nonempty | - | ['duration_value', 'duration_unit'] | 


| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | all-empty-or-nonempty | - | ['temperature_value', 'temperature_unit'] | 


| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | empty-value | Provided Below | ['amount_value', 'amount_unit', 'duration_value', 'duration_unit', 'temperature_value', 'temperature_unit'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		case-insensitive-equals	use_treatment	'No'

| RULE TYPE | RULE NAME | CONDITIONS | DATA ROW COLUMNS | 
|  --- | --- | --- | --- |
| simple type | at-least-one-nonempty | Provided Below | ['amount_value', 'amount_unit', 'duration_value', 'duration_unit', 'temperature_value', 'temperature_unit'] | 

		CONDITION NAME	DATA ROW COLUMN	VALUE
		case-insensitive-equals	use_treatment	'Yes'

### PreProcesses (in order):

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [] | [amount_value] | [Action = set, Value = Not Specified] | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	empty-value	amount_value	-

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [] | [amount_unit] | [Action = set, Value = Not Specified] | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	empty-value	amount_unit	-

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [] | [duration_value] | [Action = set, Value = Not Specified] | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	empty-value	duration_value	-

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [] | [duration_unit] | [Action = set, Value = Not Specified] | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	empty-value	duration_unit	-

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [] | [temperature_value] | [Action = set, Value = Not Specified] | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	empty-value	temperature_value	-

| PROCESS NAME | CONDITIONS | INPUT DATA ROW COLUMNS | OUTPUT DATA ROW COLUMNS | PROCESS RULE | APPEND OUTPUT | SHOW INFORMATION | 
|  --- | --- | --- | --- | --- | --- | --- |
| set-to-value | Provided Below | [] | [temperature_unit] | [Action = set, Value = Not Specified] | - | - | 

	CONDITION NAME	DATA ROW COLUMN	VALUE
	empty-value	temperature_unit	-

### Controlled Vocabularies
| lk_amount_unit | lk_unit_of_measure | database | type in ('concentration','mass','volume','Not_Specified') | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 
| lk_temperature_unit | lk_unit_of_measure | database | type in ('temperature','Not_Specified') | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 
| lk_time_unit | lk_time_unit | database | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | link | 
|  | DATABASE COLUMNS | name | description | link | 
| lk_yes_no | - | static | - | 
|  --- | --- | --- | --- |
|  | XML COLUMNS | name | description | 
|  | DATABASE COLUMNS | name | description | 
	DATA VALUES	No	No
		Yes	Yes

