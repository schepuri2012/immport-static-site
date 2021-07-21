
If you are familiar with Python, the following functions may be useful when using the ImmPort Data Query API. The code below is an example of a small utility package that could be imported into your programs to use when accessing the API. 

In the examples following the Python Helper Functions block, we will be using these 2 function to retrieve content from the Data Query API.

### Python Helper Functions
!!! example "Python Helper Functions"
    ``` python
    import sys
    import requests
    import json
    import platform
    import pandas as pd
    from io import StringIO

    API_ENDPOINT_BASE_URL = "https://api.immport.org"
    DATA_QUERY_URL = API_ENDPOINT_BASE_URL + "/data/query"
    ASPERA_TOKEN_URL = API_ENDPOINT_BASE_URL + "/data/download/token"
    IMMPORT_TOKEN_URL = "https://auth.immport.org/auth/token"


    def request_immport_token(username, password):
        '''Request an ImmPort token

           :param username: ImmPort user name.
           :param password: ImmPort user password.

           return immport_token
        '''
        r = requests.post(IMMPORT_TOKEN_URL,
                      data={'username': username, 'password': password})
        if r.status_code == 200:
            return r.json()['token']
        else:
            return None


    def api_data_query(username, password, endpoint, immport_token_url, token=True, format="json"):
        '''Use the Data Query API by first checking ImmPort user credentials,
           retrieving an ImmPort token, then call the API endpoint to retrieve the results.
    
           param user_name: ImmPort username.
           param password: ImmPort password.
           param endpoint: Data Query endpoint
           param token: Indicates if endpoint requires a token
           param format: String (json, tsv)
       

           return: results or None
        '''
        headers = {}
        results = None
    
        if token:
            immport_token = request_immport_token(immport_token_url, username, password)
            if immport_token is None:
                 print("ERROR: Credentials incorrect for ImmPort, unable to retrieve token", file = sys.stderr)
                 return None
            if format == "json":
                headers = {
                    'Authorization': "bearer " + immport_token,
                    'Content-Type': "application/json"
                }
            else:
                headers = {
                    'Authorization': "bearer " + immport_token,
                    'Content-Type': "text/plain"
                }
            
        else:
            if format == "json":
                headers = {
                    'Content-Type': "application/json"
                }
            else:
                headers = {
                    'Content-Type': "text/plain"
                }
            
        results = requests.get(endpoint, headers=headers)
        if results.status_code == 200:
            if results is None:
                 print("ERROR: API Endpoint failed to return results", file = sys.stderr)
                 return None
            if format == "json":
                return results.json()
            else:
                return results.text
        else:
            print("ERROR: API Status Code: " + str(results.status_code), file = sys.stderr)
            return None

    ```


### Retrieving ELISA results in JSON format
The example retrieves the ELISA results for SDY1, then prints one record to show the JSON output, then using Pandas creates a DataFrame.

!!! example "Python - Retrieve ELISA Results for SDY1 (JSON)"
    ``` python
    endpoint = DATA_QUERY_URL + "/result/elisa?studyAccession=SDY1&format=json"
    results = api_data_query(USERNAME, PASSWORD, endpoint, IMMPORT_TOKEN_URL, True, "json" )
    print(json.dumps(results[0],indent=4))
    df = pd.read_json(json.dumps(results))
    df.head(2)
    ```
??? example "Results"
    ```
    {
        "resultId": 1,
        "ageEvent": "Age at enrollment",
        "ageEventSpecify": null,
        "ageUnit": "Years",
        "ancestralPopulation": null,
        "analyteAccession": null,
        "analytePreferred": null,
        "analyteReported": "IgG-a Amb a",
        "armAccession": "ARM2",
        "armName": "Immunotherapy with placebo anti-IgE",
        "biosampleAccession": "BS121576",
        "biosampleType": "Whole blood",
        "biosampleSubtype": "Whole Blood",
        "clinical": "Y",
        "comments": null,
        "ethnicity": "Not Hispanic or Latino",
        "experimentAccession": "EXP14863",
        "expsampleAccession": "ES96611",
        "gender": "Male",
        "maxSubjectAge": 26.0,
        "measurementTechnique": "ELISA",
        "minSubjectAge": 26.0,
        "plannedVisitAccession": "PV66",
        "race": "White",
        "raceSpecify": null,
        "repositoryAccession": null,
        "repositoryName": null,
        "species": "Homo sapiens",
        "strain": null,
        "studyAccession": "SDY1",
        "studyTitle": "Efficacy and Safety Evaluation of Allergen Immunotherapy Co-Administered with Omalizumab (an anti-IgE Monoclonal Antibody) (ITN019AD)",
        "studyTimeCollected": -7.0,
        "studyTimeCollectedUnit": "Days",
        "subjectAccession": "SUB73370",
        "subjectPhenotype": "Ragweed-induced seasonal allergic rhinitis",
        "unitPreferred": null,
        "unitReported": "U/ml",
        "valuePreferred": 114.8,
        "valueReported": "114.8",
        "treatmentAccession": null,
        "studyTimeT0EventSpecify": null,
        "studyTimeT0Event": "Not Specified"
    }

	ageEvent	ageEventSpecify	ageUnit	analyteAccession	analytePreferred	analyteReported	ancestralPopulation	armAccession	armName	biosampleAccession	...	studyTimeT0Event	studyTimeT0EventSpecify	studyTitle	subjectAccession	subjectPhenotype	treatmentAccession	unitPreferred	unitReported	valuePreferred	valueReported
    0	Age at enrollment	NaN	Years	NaN	NaN	IgG-a Amb a	NaN	ARM2	Immunotherapy with placebo anti-IgE	BS121576	...	Not Specified	NaN	Efficacy and Safety Evaluation of Allergen Imm...	SUB73370	Ragweed-induced seasonal allergic rhinitis	NaN	NaN	U/ml	114.8	114.8
    1	Age at enrollment	NaN	Years	NaN	NaN	IgG-a Ragweed	NaN	ARM2	Immunotherapy with placebo anti-IgE	BS121576	...	Not Specified	NaN	Efficacy and Safety Evaluation of Allergen Imm...	SUB73370	Ragweed-induced seasonal allergic rhinitis	NaN	ng/ml	ng/ml	100.0	100.0
    2 rows × 42 columns
    ``` 


### Retrieving ELISA results in TSV format
The example retrieves the ELISA results for SDY1, then using Pandas creates a DataFrame.

!!! example "Python - Retrieve ELISA Results for SDY1 (TSV)"
    ``` python
    endpoint = DATA_QUERY_URL + "/result/elisa?studyAccession=SDY1&format=tsv"
    results = api_data_query(USERNAME, PASSWORD, endpoint, IMMPORT_TOKEN_URL, True, "tsv" )
    df = pd.read_csv(StringIO(results), sep="\t")
    df.head(2)
    ```

??? example "Results"
    ```
    ageEvent	ageEventSpecify	ageUnit	analyteAccession	analytePreferred	analyteReported	ancestralPopulation	armAccession	armName	biosampleAccession	...	studyTimeT0Event	studyTimeT0EventSpecify	studyTitle	subjectAccession	subjectPhenotype	treatmentAccession	unitPreferred	unitReported	valuePreferred	valueReported
    0	Age at enrollment	NaN	Years	NaN	NaN	IgG-a Amb a	NaN	ARM2	Immunotherapy with placebo anti-IgE	BS121576	...	Not Specified	NaN	Efficacy and Safety Evaluation of Allergen Imm...	SUB73370	Ragweed-induced seasonal allergic rhinitis	NaN	NaN	U/ml	114.8	114.8
    1	Age at enrollment	NaN	Years	NaN	NaN	IgG-a Ragweed	NaN	ARM2	Immunotherapy with placebo anti-IgE	BS121576	...	Not Specified	NaN	Efficacy and Safety Evaluation of Allergen Imm...	SUB73370	Ragweed-induced seasonal allergic rhinitis	NaN	ng/ml	ng/ml	100.0	100.0
    2 rows × 42 columns
    ```

### Retrieving Study Design Information
This endpoint is used by UI to retrieve study design information and may not be useful for general users. This endpoint does not require and access token.

!!! example "Python - Retrieve Study Design Information"
    ``` python
    endpoint = DATA_QUERY_URL + "/study/summary/SDY1680"
    results = api_data_query(USERNAME, PASSWORD, endpoint, IMMPORT_TOKEN_URL, False, "json" )
    print(json.dumps(results, indent=4))
    ```

??? example "Results"
    ```
    {
        "studyAccession": "SDY1680",
        "doi": "10.21430/M3OCS4VQWY",
        "title": "Comorbid illnesses are associated with altered adaptive immune responses to SARS-CoV-2",
        "pi": "Chetan Seshadri - University of Washington",
        "conditionStudied": "COVID-19",
        "briefDescription": "FCS and workspace files from ICS and Surface Marker Staining Experiments",
        "startDate": "2020-03-01",
        "detailedDescription": "Intracellular Cytokine Staining data and Surface Marker Phenotyping data from convalescent COVID-19 infected individuals who were previously either hospitalized or not hospitalized. Both the magnitude and functional breadth of antigen-specific CD4 T cell responses were consistently higher among hospitalized subjects, particularly those with medical comorbidities. CD4 T cell responses to all antigens were driven by IFN-g-independent poyfunctional profiles that are not typically the focus of vaccine studies.",
        "objectives": "Characterize T cell responses and immune subpopulations which are enriched or decreased in hospitalized convalescent individuals",
        "endpoints": "Flow Cytometry data characterizing immune subpopulations",
        "genderIncluded": "Female, Male, Not Specified",
        "subjectsNumber": 68,
        "downloadPackages": null,
        "contractGrant": "Qualification Of Assays To Measure Human T-Cell Responses Against Mycobacterial Lipid Antigens",
        "program": "NIH Program",
        "dataCompleteness": "0 - Descriptive data and results as originally received from the data provider.",
        "hypothesis": "Hospitalized and Non-hospitalized convalescent COVID-19 infected  individuals exhibit unique T cell responses",
        "studyLinks": [
            {
                "studyLinkId": 1345,
                "name": "Github",
                "type": null,
                "value": "https://github.com/seshadrilab"
            },
            {
                "studyLinkId": 1423,
                "name": "Correlates Severe COVID19 Surface Markers",
                "type": null,
                "value": "https://github.com/seshadrilab/Correlates_Severe_COVID19_Surface_Markers"
            },
            {
                "studyLinkId": 1424,
                "name": "Correlates Severe COVID19 ICS",
                "type": null,
                "value": "https://github.com/seshadrilab/Correlates_Severe_COVID19_ICS"
            }
        ],
        "studyPubmeds": [
            {
                "id": {
                    "studyAccession": "SDY1680",
                    "pubmedId": "33621211"
                },
                "authors": "Yu KK, Fischinger S, Smith MT, Atyeo C, Cizmeci D, Wolf CR, Layton ED, Logue JK, Aguilar MS, Shuey K, Loos C, Yu J, Franko NM, Choi RY, Wald A, Barouch DH, Koelle DM, Lauffenburger D, Chu HY, Alter G, Seshadri C",
                "doi": "10.1172/jci.insight.146242",
                "issue": null,
                "journal": "JCI insight",
                "month": "Feb",
                "pages": null,
                "title": "Comorbid illnesses are associated with altered adaptive immune responses to SARS-CoV-2.",
                "year": "2021"
            },
            {
                "id": {
                    "studyAccession": "SDY1680",
                    "pubmedId": "TBD"
                },
                "authors": null,
                "doi": null,
                "issue": null,
                "journal": null,
                "month": null,
                "pages": null,
                "title": null,
                "year": null
            }
        ],
        "studyGlossarys": []
    }
    ```

### Retrieve LK_DISEASE
The way data is returned for the LK tables is a little complex. The example below shows one way to extract information from the results.

!!! example "Python - Retrieve LK_DISEASE Information"
    ``` python
    pd.set_option('max_colwidth', 200)
    endpoint = DATA_QUERY_URL + "/lk_disease"
    results = api_data_query(USERNAME, PASSWORD, endpoint, IMMPORT_TOKEN_URL, True, "json")
    df = pd.read_json(json.dumps(results['content']), orient="columns")[['name','description','link']]
    df.head(10)
    ```

??? example "Results"
    ```
    name	description	link
    0	acquired immunodeficiency syndrome	A Human immunodeficiency virus infectious disease that results_in reduction in the numbers of CD4-bearing helper T cells below 200 per microliter of blood or 14% of all lymphocytes thereby renderi...	http://purl.obolibrary.org/obo/DOID_635
    1	acute disseminated encephalomyelitis	An encephalomyelitis characterized by inflammation located in brain and located in spinal cord that damages myelin. It usually occurs after viral infection, but also following vaccination, bacteri...	http://purl.obolibrary.org/obo/DOID_639
    2	Addison's disease	An adrenal cortical hypofunction that is characterized by insufficient steroid hormone production by the adrenal glands.	http://purl.obolibrary.org/obo/DOID_13774
    3	Aging	The process of change in the structure and function of an organism that occurs with the passage of time.	http://purl.obolibrary.org/obo/NCIT_C16269
    4	alcohol use disorder	A substance abuse that involves the recurring use of alcoholic beverages despite negative consequences.	http://purl.obolibrary.org/obo/DOID_1574
    5	allergic hypersensitivity disease	An immune system disease that is an exaggerated immune response to allergens, such as insect venom, dust mites, pollen, pet dander, drugs or some foods.	http://purl.obolibrary.org/obo/DOID_1205
    6	allergic rhinitis	A rhinitis that is an allergic inflammation and irritation of the nasal airways involving sneezing, runny nose, nasal congestion, itching and tearing of the eyes caused by exposure to an allergen ...	http://purl.obolibrary.org/obo/DOID_4481
    7	alopecia areata	An autoimmune disease resulting in the loss of hair on the scalp and elsewhere on the body initially causing bald spots.	http://purl.obolibrary.org/obo/DOID_986
    8	Alzheimer's disease	A tauopathy that is characterized by memory lapses, confusion, emotional instability and progressive loss of mental ability and results in progressive memory loss, impaired thinking, disorientatio...	http://purl.obolibrary.org/obo/DOID_10652
    9	anemia	A hematopoietic system disease that is characterized by a decrease in the normal number of red blood cells.	http://purl.obolibrary.org/obo/DOID_2355
    ```
