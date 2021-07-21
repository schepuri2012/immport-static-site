## Overview

The following endpoints can be used to retrieve assay results that have been parsed and stored in standardized tables for these types of results. The ImmPort team works with many groups to design these tables to store standarized Immunology assay results. Assay results that can not be parsed, or do not fit into the current set of standardized tables, may be available for download as study files or custom assay results files.

## Endpoints
The Data Query API endpoint is `https://api.immport.org/data/query/result/<endpoint>`, where `<endpoint>` is the name of the endpoint such as `elisa`. The table below represents the API endpoints that return metadata and results for these assay results.

 Endpoint | Description | HTTP URL |
| --- | --- | --- |
| elisa |Enzyme-Linked ImmunoSorbant Assay <a href="http://purl.obolibrary.org/obo/OBI_0000661" target="_blank"><i class="fa fa-external-link"><i></a> | https://api.immport.org/data/query/result/elisa |
| elispot |Enzyme-linked ImmunoSPOT <a href="http://purl.obolibrary.org/obo/OBI_0600031" target="_blank"><i class="fa fa-external-link"><i></a> | https://api.immport.org/data/query/result/elispot |
| fcsAnalyzed |flow and mass cytometry results <a href="http://purl.obolibrary.org/obo/OBI_0002115" target="_blank"><i class="fa fa-external-link"><i></a> |  https://api.immport.org/data/query/result/fcsAnalyzed |
| hai | Hemagglutination Inhibition <a href="http://purl.obolibrary.org/obo/OBI_0000875" target="_blank"><i class="fa fa-external-link"><i></a>| https://api.immport.org/data/query/result/hai |
| hlaTyping | Human Leukocyte Antigen typing <a href="http://purl.obolibrary.org/obo/OBI_0002122" target="_blank"><i class="fa fa-external-link"><i></a> | https://api.immport.org/data/query/result/hlaTyping |
| kirTyping | Killer cell immunoglobulin-like receptors typing <a href="http://purl.obolibrary.org/obo/OBI_0002121" target="_blank"> <i class="fa fa-external-link"><i></a>| https://api.immport.org/data/query/result/kirTyping |
| mbaa | Multiplex Bead Array Assay (Luminex) <a href="http://purl.obolibrary.org/obo/OBI_0000920" target="_blank"> <i class="fa fa-external-link"><i></a>| https://api.immport.org/data/query/result/mbaa |
| neutAbTiter | Neutralizing Antibody Titer Assay <a href="http://purl.obolibrary.org/obo/OBI_0000872" target="_blank"><i class="fa fa-external-link"><i></a> | https://api.immport.org/data/query/result/neutAbTiter |
| pcr | Quantitative Polymerase Chain Reaction <a href="http://purl.obolibrary.org/obo/OBI_0000415" target="_blank"><i class="fa fa-external-link"><i></a> | https://api.immport.org/data/query/result/pcr |
| massSpectrometryResult | An assay that identifies the amount and type of material entities present in a sample by fragmenting the sample and measuring the mass-to-charge ratio of the resulting particles <a href="http://purl.obolibrary.org/obo/OBI_0000470" target="_blank"><i class="fa fa-external-link"><i></a>| https://api.immport.org/data/query/result/massSpectrometryResult |

## Filter Criteria
Each of the API endpoints mentioned in the table [above](#endpoints) can have the following list of filter criteria fields passed as parameters to filter the data to meet a specific set of requirements. One or more of the filter fields can be passed as parameters to the various API endpoints.

If there is an entry in the **Reference Table** column, this means the values for these filters is limited to a specific set of values. In the ImmPort data model these tables are designated as lookup tables, another common term for these type of tables are controlled vocabulary tables. More information, including the set of values for each table is available [here](
https://www.immport.org/shared/templateDocumentation) under the **Lookup Tables** tab.

<div class="alert alert-block alert-info">
The values passed to the filter fields are case insensitive
</div>

| Filter Field | Description | Reference Table |
| --- | --- | --- |
| ageEvent | Subject's age event. This filter field can take multiple values and it will accept only exact values (case insensitive).|lk_age_event|
| ageEventSpecify | Subject's age event if not a preferred term. This filter field can take multiple values and it will accept only exact values (case insensitive).|NA|
| ageUnit | Subject's age unit. This filter field can take multiple values and it will accept only exact values (case insensitive).|lk_time_unit|
| ancestralPopulation | Subject's ancestral population. This filter field can take multiple values and it will accept only exact values (case insensitive).|lk_ancestral_population|
| armAccession |Study arm accession to which a subject is assigned. This filter field can take multiple values and it will accept only exact values (case insensitive).|NA|
| armName | Study arm name to which a subject is assigned.This filter field can take multiple values and it will accept **partial match ** values (case insensitive).|NA|
| biosampleAccession | Biological sample accession. This filter field can take multiple values and it will accept only exact values (case insensitive).|NA|
| biosampleSubtype | Biological sample type if not a preferred term. This filter field can take multiple values and it will accept only exact values (case insensitive).|NA|
| biosampleType | Biological sample type. This filter field can take multiple values and it will accept only exact values (case insensitive).|lk_sample_type|
| clinical | Flag to indicate clincal trial status. This filter field will take a **single exact** value (case insensitive).|Boolean|
| ethnicity | Subject's ethnicity. This filter field can take multiple values and it will accept only exact values (case insensitive).|lk_ethnicity|
| experimentAccession |Experiment accession. This filter field can take multiple values and it will accept only exact values (case insensitive).|NA|
| expsampleAccession | Experiment sample accession. This filter field can take multiple values and it will accept only exact values (case insensitive).|NA|
| gender | Subject's gender. This filter field can take multiple values and it will accept only exact values (case insensitive).|lk_gender|
| maxSubjectAge | Subject's maximum age value. This filter field will take a **single exact** numeric value and the condition will be "equal to (=)". |NA|
| maxSubjectAgeGte | Subject's maximum age value. This filter field will take a **single exact** numeric value and the condition will be "greater than and equal to (>=)". |NA|
| maxSubjectAgeLte | Subject's maximum age value. This filter field will take a **single exact** numeric value and the condition will be "less than and equal to (<=)".|NA|
| maxSubjectAgeGt | Subject's maximum age value. This filter field will take a **single exact** numeric value and the condition will be "greater than (>)".|NA|
| maxSubjectAgeLt | Subject's maximum age value. This filter field will take a **single exact** numeric value and the condition will be "less than (<)".|NA|
| minSubjectAge | Subject's minimum age value. This filter field will take a **single exact** numeric value and the condition will be "equal to (=)". |NA|
| minSubjectAgeGte | Subject's minimum age value. This filter field will take a **single exact** numeric value and the condition will be "greater than and equal to (>=)". |NA|
| minSubjectAgeLte | Subject's minimum age value. This filter field will take a **single exact** numeric value and the condition will be "less than and equal to (<=)".|NA|
| minSubjectAgeGt | Subject's minimum age value. This filter field will take a **single exact** numeric value and the condition will be "greater than (>)".|NA|
| minSubjectAgeLt | Subject's minimum age value. This filter field will take a **single exact** numeric value and the condition will be "less than (<)".|NA|
| measurementTechnique | Experiment Measurement Technique. This filter field can take multiple values and it will accept only exact values (case insensitive).|lk_exp_measurement_tech|
| plannedVisitAccession | Study Planned Visit Accession. This filter field can take multiple values and it will accept only exact values (case insensitive).|NA|
| race | Subject's race. This filter field can take multiple values and it will accept only exact values (case insensitive).|lk_race|
| raceSpecify | Subject's race if non-preferred values were used. This filter field can take multiple values and it will accept only exact values (case insensitive).|NA|
| species | Subject's species. This filter field can take multiple values and it will accept only exact values (case insensitive).|lk_species|
| strain | Non-human subject strain. This filter field can take multiple values and it will accept only exact values (case insensitive).|NA|
| studyAccession | Study accession. This filter field can take multiple values and it will accept only exact values (case insensitive).|NA|
| studyTimeCollected | Sample's collection time in study timeline normalized per subject. This filter field will take a **single exact** numeric value and the condition will be "equal to (=)". |NA|
| studyTimeCollectedGte | Sample's collection time in study timeline normalized per subject. This filter field will take a **single exact** numeric value and the condition will be "greater than and equal to (>=)". |NA|
| studyTimeCollectedLte | Sample's collection time in study timeline normalized per subject. This filter field will take a **single exact** numeric value and the condition will be "less than and equal to (<=)".|NA|
| studyTimeCollectedGt | Sample's collection time in study timeline normalized per subject. This filter field will take a **single exact** numeric value and the condition will be "greater than (>)".|NA|
| studyTimeCollectedLt | Sample's collection time in study timeline normalized per subject. This filter field will take a **single exact** numeric value and the condition will be "less than (<)".|NA|
| studyTimeCollectedUnit | Sample study time collected unit. This filter field can take multiple values and it will take exact values (case insensitive).|lk_time_unit|
| studyTimeT0Event | Sample study time collected milestone or point of reference. This filter field can take multiple values and it will take exact values (case insensitive).|lk_t0_event|
| studyTimeT0EventSpecify | Sample study time collected milestone or point of reference if non-preferred tersm were used. This filter field can take multiple values and it will take exact values (case insensitive).|NA|
| subjectAccession |Subject accession. This filter field can take multiple values and it will accept only exact values (case insensitive).|NA|
| studyTitle | Study title. This filter field can take multiple values and it will take **partial** values (case insensitive)|NA|
| subjectPhenotype | Subject phenotype or description. This filter field can take multiple values and it will take exact values (case insensitive)|NA|
| treatmentAccession | Treatment accession. This filter field can take multiple values and it will accept **partial match** values (case insensitive).|NA|
| format | Query API format. This filter field will take a **single exact** value. The valid values for this field are: json and tsv.|NA|