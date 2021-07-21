The **filePath** endpoint is a little different than most of the endpoints. This endpoint is used download the file path locations for all the files linked to a study via the experiment to expsample relationship in the relational model. Retrieving the file paths using this endpoint allows the user to use these files with using the File Download tool or file download endpoint, which require the file path as input.

## Example Shell Command - TSV Format
``` shell
#!/bin/bash

export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1  | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

curl -k -H "Authorization: bearer $token" "https://api.immport.org/data/query/result/filePath?format=tsv&studyAccession=SDY208"
```
The request above will return the paths to result files because the endpoint is https://api.immport.org/data/query/result/filePath.
The filter criteria studyAccession=SDY208 that will be executed on the result data will be study_accession = 'SDY208'.

The response will be an array of result file metadata and its corresponding file paths.

This response can be an input into the File Download API which will download all the unique list of files in the response.

??? example "Results"
    ```
    [ {
      "filePathId" : "388647_ES736618_BS689943",
      "fileInfoId" : 388647,
      "fileDetail" : "Virus neutralization result",
      "filesizeBytes" : 615,
      "fileName" : "Virus_Neutralization_Results.388647.txt",
      "originalFileName" : "Virus_Neutralization_Results.txt",
      "sourceType" : "EXPSAMPLE",
      "sourceAccession" : "ES736618",
      "experimentAccession" : "EXP13365",
      "measurementTechnique" : "Hemagglutination Inhibition",
      "studyAccession" : "SDY208",
      "clinical" : "N",
      "studyTitle" : "Serological Memory and Long-term Protection to Novel H1N1 Influenza Virus After Skin Vaccination",
      "biosampleAccession" : "BS689943",
      "biosampleType" : "Tissue",
      "biosampleSubtype" : null,
      "studyTimeCollected" : 154.0,
      "studyTimeCollectedUnit" : "Days",
      "studyTimeT0Event" : "Time of initial vaccine administration",
      "studyTimeT0EventSpecify" : null,
      "plannedVisitAccession" : "PV2442",
      "subjectAccession" : "SUB120519",
      "ethnicity" : null,
      "gender" : "Female",
      "race" : null,
      "raceSpecify" : null,
      "species" : "Mus musculus",
      "strain" : null,
      "armAccession" : "ARM884",
      "armName" : "Microneedle vaccination- 5 ug inactivated A/California/04/09 virus, Challenged: 10x LD50 A/California/04/09 virus",
      "ageEvent" : "Age at enrollment",
      "ageEventSpecify" : null,
      "ageUnit" : "Weeks",
      "maxSubjectAge" : 6.0,
      "minSubjectAge" : 6.0,
      "subjectPhenotype" : "Specific-pathogen free",
      "filePath" : "/SDY208/ResultFiles/Virus_neutralization_result/Virus_Neutralization_Results.388647.txt"
    }, {
      "filePathId" : "388647_ES736619_BS689944",
      "fileInfoId" : 388647,
      "fileDetail" : "Virus neutralization result",
      "filesizeBytes" : 615,
      "fileName" : "Virus_Neutralization_Results.388647.txt",
      "originalFileName" : "Virus_Neutralization_Results.txt",
      "sourceType" : "EXPSAMPLE",
      "sourceAccession" : "ES736619",
      "experimentAccession" : "EXP13365",
      "measurementTechnique" : "Hemagglutination Inhibition",
      "studyAccession" : "SDY208",
      "clinical" : "N",
      "studyTitle" : "Serological Memory and Long-term Protection to Novel H1N1 Influenza Virus After Skin Vaccination",
      "biosampleAccession" : "BS689944",
      "biosampleType" : "Tissue",
      "biosampleSubtype" : null,
      "studyTimeCollected" : 154.0,
      "studyTimeCollectedUnit" : "Days",
      "studyTimeT0Event" : "Time of initial vaccine administration",
      "studyTimeT0EventSpecify" : null,
      "plannedVisitAccession" : "PV2442",
      "subjectAccession" : "SUB120520",
      "ethnicity" : null,
      "gender" : "Female",
      "race" : null,
      "raceSpecify" : null,
      "species" : "Mus musculus",
      "strain" : null,
      "armAccession" : "ARM885",
      "armName" : "Subcutaneous vaccination- 5 ug inactivated A/California/04/09 virus, Challenged: 10x LD50 A/California/04/09 virus",
      "ageEvent" : "Age at enrollment",
      "ageEventSpecify" : null,
      "ageUnit" : "Weeks",
      "maxSubjectAge" : 6.0,
      "minSubjectAge" : 6.0,
      "subjectPhenotype" : "Specific-pathogen free",
      "filePath" : "/SDY208/ResultFiles/Virus_neutralization_result/Virus_Neutralization_Results.388647.txt"
    },.........
    ```