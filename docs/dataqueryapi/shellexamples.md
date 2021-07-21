The following examples show examples of using various filter critera and formatting options when using Shell commands.

Any of the shell scripts below can be copied to a .sh file and executed at the command prompt of a terminal and the output can be directed to a file. (Please replace the REPLACE_WITH_USERNAME with your username and REPLACE_WITH_PASSWORD with your password)

## Request Using Multiple Filter Parameters
This request will return PCR results that are from SDY165 and studyTimeCollected greater than or equal to 95.5 and have a subject phenotype of Healthy Volunteer.

!!! example "Shell Script - Request with Multiple Filter Parameters"
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1  | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -H "Authorization: bearer $token" "https://api.immport.org/data/query/result/pcr?studyAccession=SDY165&studyTimeCollectedGte=95.5&subjectPhenotype=Healthy%20volunteer"
    ```

??? example "Results"
    ```
    {
      "resultId" : 40875,
      "ageEvent" : "Other",
      "ageEventSpecify" : "subject is atleast 18 years or older",
      "ageUnit" : "Years",
      "ancestralPopulation" : null,
      "armAccession" : "ARM743",
      "armName" : "Healthy_volunteer",
      "biosampleAccession" : "BS661596",
      "biosampleType" : "Cell",
      "biosampleSubtype" : "undividing B cells",
      "clinical" : "N",
      "comments" : "Legacy data copied from Threshold_Cycles column to Expression_Value column, and Expression_Unit column = Ct (where null). See ID-1609 for details.",
      "ethnicity" : "Other",
      "experimentAccession" : "EXP11754",
      "expsampleAccession" : "ES714478",
      "gender" : "Unknown",
      "geneId" : "6222",
      "geneName" : "ribosomal protein S18",
      "geneSymbol" : "RPS18",
      "maxSubjectAge" : 18.00,
      "measurementTechnique" : "Q-PCR",
      "minSubjectAge" : 18.00,
      "otherGeneAccession" : null,
      "plannedVisitAccession" : "PV3039",
      "race" : "Unknown",
      "raceSpecify" : null,
      "repositoryAccession" : null,
      "repositoryName" : null,
      "species" : "Homo sapiens",
      "strain" : null,
      "studyAccession" : "SDY165",
      "studyTitle" : "Characterization of in vitro Stimulated B Cells from Human Subjects",
      "studyTimeCollected" : 96.00,
      "studyTimeCollectedUnit" : "Hours",
      "studyTimeT0Event" : "Time of initial treatment",
      "studyTimeT0EventSpecify" : null,
      "subjectAccession" : "SUB119214",
      "subjectPhenotype" : "Healthy volunteer",
      "unitPreferred" : null,
      "unitReported" : "Ct",
      "valuePreferred" : null,
      "valueReported" : "15.2938",
      "treatmentAccession" : null
    }, {
      "resultId" : 40876,
      "ageEvent" : "Other",
      "ageEventSpecify" : "subject is atleast 18 years or older",
      "ageUnit" : "Years",
      "ancestralPopulation" : null,
      "armAccession" : "ARM743",
      "armName" : "Healthy_volunteer",
      "biosampleAccession" : "BS661596",
      "biosampleType" : "Cell",
      "biosampleSubtype" : "undividing B cells",
      "clinical" : "N",
      "comments" : "Legacy data copied from Threshold_Cycles column to Expression_Value column, and Expression_Unit column = Ct (where null). See ID-1609 for details.",
      "ethnicity" : "Other",
      "experimentAccession" : "EXP11754",
      "expsampleAccession" : "ES714479",
      "gender" : "Unknown",
      "geneId" : "6222",
      "geneName" : "ribosomal protein S18",
      "geneSymbol" : "RPS18",
      "maxSubjectAge" : 18.00,
      "measurementTechnique" : "Q-PCR",
      "minSubjectAge" : 18.00,
      "otherGeneAccession" : null,
      "plannedVisitAccession" : "PV3039",
      "race" : "Unknown",
      "raceSpecify" : null,
      "repositoryAccession" : null,
      "repositoryName" : null,
      "species" : "Homo sapiens",
      "strain" : null,
      "studyAccession" : "SDY165",
      "studyTitle" : "Characterization of in vitro Stimulated B Cells from Human Subjects",
      "studyTimeCollected" : 96.00,
      "studyTimeCollectedUnit" : "Hours",
      "studyTimeT0Event" : "Time of initial treatment",
      "studyTimeT0EventSpecify" : null,
      "subjectAccession" : "SUB119214",
      "subjectPhenotype" : "Healthy volunteer",
      "unitPreferred" : null,
      "unitReported" : "Ct",
      "valuePreferred" : null,
      "valueReported" : "14.7243",
      "treatmentAccession" : null
    },......
    ```

## Request Passing a Parameter with Multiple Values
!!! example "Shell Script - Filter by Multiple Study Accessions"
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1  | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -H "Authorization: bearer $token" "https://api.immport.org/data/query/result/neutAbTiter?studyAccession=SDY89,SDY180&expsampleAccession=ES588503,ES588504,ES717687"
    ```

The request above will return Neutralizing antibody titer result data (virus neutralization) because the endpoint is https://api.immport.org/data/query/result/neutAbTiter.
The filter criteria studyAccession=SDY89,SDY180&expsampleAccession=ES588503,ES588504,ES717687  that will be treated as **WHERE** clause on the query similar to:  study_accession in ('SDY89','SDY180') and expsample_accession in ('ES588503','ES588504','ES717687').

For any filter condition that can take multiple values, the values specified should be comma separated or you can provide tham using '&' as the seperator. (e.g. studyAccession=SDY89&studyAccession=SDY180). The response will be an array of neutralizing antibody titer result data that satisfy the filter criteria.

??? example "Results"
    ```
    [ {
        "resultId" : 1597,
        "ageEvent" : "Age at enrollment",
        "ageEventSpecify" : null,
        "ageUnit" : "Years",
        "ancestralPopulation" : null,
        "armAccession" : "ARM566",
        "armName" : "Energix-B",
        "biosampleAccession" : "BS632077",
        "biosampleType" : "Serum",
        "biosampleSubtype" : null,
        "clinical" : "N",
        "comments" : null,
        "ethnicity" : "Not Hispanic or Latino",
        "experimentAccession" : "EXP10671",
        "expsampleAccession" : "ES588503",
        "gender" : "Female",
        "maxSubjectAge" : 52.00,
        "measurementTechnique" : "Virus Neutralization",
        "minSubjectAge" : 52.00,
        "plannedVisitAccession" : "PV1872",
        "race" : "White",
        "raceSpecify" : null,
        "repositoryAccession" : null,
        "repositoryName" : null,
        "species" : "Homo sapiens",
        "strain" : null,
        "studyAccession" : "SDY89",
        "studyTitle" : "Systems Biology Analysis of the response to  Licensed Hepatitis B Vaccine (Engerix-B) (see companion study SDY690)",
        "studyTimeCollected" : 28.00,
        "studyTimeCollectedUnit" : "Days",
        "studyTimeT0Event" : "Time of initial vaccine administration",
        "studyTimeT0EventSpecify" : null,
        "subjectAccession" : "SUB114737",
        "subjectPhenotype" : "Healthy",
        "unitPreferred" : null,
        "unitReported" : null,
        "valuePreferred" : null,
        "valueReported" : "1",
        "virusStrainPreferred" : null,
        "virusStrainReported" : "Anti-HBs",
        "treatmentAccession" : "TRT41"
      },.... 
    ```

## Request Passing a Numeric Parameter
!!! example "Shell Script - Filter on Age"
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1  | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -H "Authorization: bearer $token" "https://api.immport.org/data/query/result/mbaa?studyAccession=SDY111&minSubjectAgeGte=63.9"

    ```

The request above will return MBAA result data because the endpoint is https://api.immport.org/data/query/result/mbaa.
The filter criteria studyAccession=SDY111&minSubjectAgeGte=63.9 that will be executed on the MBAA result data will be study_accession = 'SDY111' and min_subject_age >= 63.9.

For any filter condition that can take numeric value, the values specified should be a number and depending on the suffix Gte (Greater than and equal to), Lte (Less than and equal to), Gt (Greater than), Lt (Less than ) the operation will be determined. The response will be an array of MBAA result data that satisfy the filter criteria.

??? example "Results"
    ```
    [ {
      "resultId" : 9589,
      "ageEvent" : "Age at initial vaccine administration",
      "ageEventSpecify" : null,
      "ageUnit" : "Years",
      "ancestralPopulation" : null,
      "analytePreferred" : "CD40LG",
      "analyteReported" : "CD40L",
      "armAccession" : "ARM641",
      "armName" : "Vaccine cohort 2011",
      "assayGroupId" : null,
      "assayId" : "P01",
      "biosampleAccession" : "BS689619",
      "biosampleType" : "Other",
      "biosampleSubtype" : null,
      "clinical" : "N",
      "comments" : null,
      "concentrationUnitPreferred" : null,
      "concentrationUnitReported" : "pg/ml",
      "concentrationValuePreferred" : null,
      "concentrationValueReported" : "35.92",
      "ethnicity" : "Not Hispanic or Latino",
      "experimentAccession" : "EXP13361",
      "gender" : "Male",
      "maxSubjectAge" : 63.90,
      "measurementTechnique" : "Luminex xMAP",
      "mfi" : "347.75",
      "mfiCoordinate" : null,
      "minSubjectAge" : 63.90,
      "plannedVisitAccession" : "PV1945",
      "race" : "White",
      "raceSpecify" : null,
      "repositoryAccession" : null,
      "repositoryName" : null,
      "species" : "Homo sapiens",
      "strain" : null,
      "studyAccession" : "SDY111",
      "studyTitle" : "VZV vaccination in the elderly",
      "studyTimeCollected" : 0.00,
      "studyTimeCollectedUnit" : "Days",
      "studyTimeT0Event" : "Time of initial vaccine administration",
      "studyTimeT0EventSpecify" : null,
      "sourceAccession" : "ES736348",
      "sourceType" : "EXPSAMPLE",
      "subjectAccession" : "SUB116437",
      "subjectPhenotype" : "Non-twin",
      "treatmentAccession" : "TRT255"
    }, {
      "resultId" : 9590,
      "ageEvent" : "Age at initial vaccine administration",
      "ageEventSpecify" : null,
      "ageUnit" : "Years",
      "ancestralPopulation" : null,
      "analytePreferred" : "CXCL5",
      "analyteReported" : "ENA78",
      "armAccession" : "ARM641",
      "armName" : "Vaccine cohort 2011",
      "assayGroupId" : null,
      "assayId" : "P01",
      "biosampleAccession" : "BS689619",
      "biosampleType" : "Other",
      "biosampleSubtype" : null,
      "clinical" : "N",
      "comments" : null,
      "concentrationUnitPreferred" : null,
      "concentrationUnitReported" : "pg/ml",
      "concentrationValuePreferred" : null,
      "concentrationValueReported" : "47",
      "ethnicity" : "Not Hispanic or Latino",
      "experimentAccession" : "EXP13361",
      "gender" : "Male",
      "maxSubjectAge" : 63.90,
      "measurementTechnique" : "Luminex xMAP",
      "mfi" : "202",
      "mfiCoordinate" : null,
      "minSubjectAge" : 63.90,
      "plannedVisitAccession" : "PV1945",
      "race" : "White",
      "raceSpecify" : null,
      "repositoryAccession" : null,
      "repositoryName" : null,
      "species" : "Homo sapiens",
      "strain" : null,
      "studyAccession" : "SDY111",
      "studyTitle" : "VZV vaccination in the elderly",
      "studyTimeCollected" : 0.00,
      "studyTimeCollectedUnit" : "Days",
      "studyTimeT0Event" : "Time of initial vaccine administration",
      "studyTimeT0EventSpecify" : null,
      "sourceAccession" : "ES736348",
      "sourceType" : "EXPSAMPLE",
      "subjectAccession" : "SUB116437",
      "subjectPhenotype" : "Non-twin",
      "treatmentAccession" : "TRT255"
    },....
    ```   

## Request Passing Partial Value
!!! example "Shell Script - Filter on Study Title"
    ``` shell
    #!/bin/bash

    export token=`curl -X POST https://auth.immport.org/auth/token -d username="REPLACE_WITH_USERNAME" -d password="REPLACE_WITH_PASSWORD" 2>&1  | fgrep '"token"' | sed -e 's/^.*"token" : "//;s/".*$//'`

    curl -k -H "Authorization: bearer $token" "https://api.immport.org/data/query/result/hlaTyping?studyTitle=smallpox%20vaccine"
    ```

The request above will return HLA typing result data because the endpoint is https://api.immport.org/data/query/result/hlaTyping.
The filter criteria studyTitle=smallpox%20vaccine that will be executed on the HLA typing result data will be study_title like '%smallpox vaccine%'.

The search will be case insensitive and any HLA typing where the study title has 'smallpox vaccine' will be returned in the response.

The response will be an array of HLA typing result data that satisfy the filter criteria.

??? example "Results"
    ```
    [ {
      "resultId" : 68533,
      "allele1" : "A*020101",
      "allele2" : "A*020101",
      "ageEvent" : "Age at enrollment",
      "ageEventSpecify" : null,
      "ageUnit" : "Years",
      "ancestralPopulation" : null,
      "armAccession" : "ARM51",
      "armName" : "Control Group",
      "biosampleAccession" : "BS255367",
      "biosampleType" : "DNA",
      "biosampleSubtype" : null,
      "clinical" : "N",
      "comments" : null,
      "ethnicity" : "Not Specified",
      "experimentAccession" : "EXP4730",
      "expsampleAccession" : "ES145152",
      "gender" : "Female",
      "maxSubjectAge" : 25.00,
      "measurementTechnique" : "HLA Typing",
      "minSubjectAge" : 25.00,
      "plannedVisitAccession" : "PV1250",
      "race" : "White",
      "raceSpecify" : null,
      "repositoryAccession" : null,
      "repositoryName" : null,
      "resultSetId" : 107322,
      "species" : "Homo sapiens",
      "strain" : null,
      "studyAccession" : "SDY26",
      "studyTitle" : "Identify polymorphisms associated with risk for the development of myopericarditis following smallpox vaccine",
      "studyTimeCollected" : 1.00,
      "studyTimeCollectedUnit" : "Days",
      "studyTimeT0Event" : "Not Specified",
      "studyTimeT0EventSpecify" : null,
      "subjectAccession" : "SUB82339",
      "subjectPhenotype" : "Control",
      "treatmentAccession" : null
    }, {
      "resultId" : 68534,
      "allele1" : "B*4001",
      "allele2" : "B*440201",
      "ageEvent" : "Age at enrollment",
      "ageEventSpecify" : null,
      "ageUnit" : "Years",
      "ancestralPopulation" : null,
      "armAccession" : "ARM51",
      "armName" : "Control Group",
      "biosampleAccession" : "BS255367",
      "biosampleType" : "DNA",
      "biosampleSubtype" : null,
      "clinical" : "N",
      "comments" : null,
      "ethnicity" : "Not Specified",
      "experimentAccession" : "EXP4730",
      "expsampleAccession" : "ES145152",
      "gender" : "Female",
      "maxSubjectAge" : 25.00,
      "measurementTechnique" : "HLA Typing",
      "minSubjectAge" : 25.00,
      "plannedVisitAccession" : "PV1250",
      "race" : "White",
      "raceSpecify" : null,
      "repositoryAccession" : null,
      "repositoryName" : null,
      "resultSetId" : 107322,
      "species" : "Homo sapiens",
      "strain" : null,
      "studyAccession" : "SDY26",
      "studyTitle" : "Identify polymorphisms associated with risk for the development of myopericarditis following smallpox vaccine",
      "studyTimeCollected" : 1.00,
      "studyTimeCollectedUnit" : "Days",
      "studyTimeT0Event" : "Not Specified",
      "studyTimeT0EventSpecify" : null,
      "subjectAccession" : "SUB82339",
      "subjectPhenotype" : "Control",
      "treatmentAccession" : null
    },....
    ```
