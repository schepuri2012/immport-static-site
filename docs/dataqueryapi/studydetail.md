
The following endpoints are primarly used by the ImmPort SharedData application to display the Study detail pages. They may not be useful for general reanalysis or repurposing data projects. These endpoints do not require an ImmPort Access Token to use.

BASE URL = https://api.immport.org/data/query

| Endpoint | Description | BASE URL + Endpoint |
| --- | --- | --- |
| adverseevent summary |	Adverse event summary	| /adverseevent/summary/{studyAccession} |
| adverseevent detail	| Adverse event details	| /adverseevent/detail/{studyAccession} |
| assesmentpanel summary	| Assessment panel summary	| /assessmentpanel/summary/{studyAccession} |
| intervention summary	| Intervention summary	| /intervention/summary/{studyAccession} |
| compoundrolesummary	| Compound (drug, molecule) summary	| /intervention/compoundrolesummary/{studyAccession}/{compoundRole} |
| compoundroledetail	| Compound (drug, molecule) detail	| /intervention/compoundroledetail/{studyAccession}/{compoundRole} |
| labtestpanel summary | Lab test panel summary	| /labtestpanel/summary/{studyAccession} |
| cntByPgmID | Program specfifc shared data counts	| /resrcpgcnt/cntByPgmID?programIds={comma        separated list of program ids} |
| study summary	| Study summary	| /study/summary/{studyAccession} |
| study design	| Study design	| /study/design/{studyAccession} |
| studyfile	| Study files	| /study/studyfile/{studyAccession} |
| study mechanisticAssay	| Experiment or mechanistic assay summary by study	| study/mechanisticAssay/{studyAccession} |
| experiment mechanisticAssay	| Experiment or mechanistic assay summary by experiment |	experiment/mechanisticAssay/{experimentAccession} |
| labtestcomponent	| Lab test components (lab test panel results)	| /study/labtestcomponent/{studyAccession} |
| assessmentcomponent	| Assessment components (assessment panel  results) |	/study/assessmentcomponent/{studyAccession} |
| plannedvisit	| Planned visit	| /study/plannedvisit/{studyAccession}/{pivotTable} |
| findAllStudyAccessions	| Study accessions list	| /study/findAllStudyAccessions |
| demographics	| Demograhics of study subjects	| /subject/demographics/{studyAccession} |
| datarelversion | Latest Study Data Release Version | /studydatarel/datarelver |
| immune_exposure | List of immune exposures | /immune_exposure |
| fcs_header | List of fcs headers | /fcs_header/{studyAccession} |
| fcs_header_marker | List of fcs header markers | /fcs_header_marker/{studyAccession} |
| reagent | List of reagents | /reagent |
| treatment | List of treatments | /treatment |
| downloadCount | download counts for the study list | /study/downloadCount?studyAccession={comma separated list of studies} |
| expsample_public_repository | List of  expsample public repository | /expsample_public_repository |