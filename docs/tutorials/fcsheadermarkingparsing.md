# Introduction

This tutorial describes how the ImmPort Data Uploader parses the fcs-file text
header for PNN and PNS markers reported in the templates upload templates
**experimentSamples.Flow_Cytometry.txt** (**.Fcs Result File**)and
**experimentSamples.CYTOF.txt** (**Result File Name**) to generate the content
of the fcs_header_marker database table and determination of the
fcs_header.panel_preferred database column.  The Uploader uses a **BNF**
(Backus-Naur form) grammar for parsing the PNN/PNS reported markers.  The BNF
grammar is specified below.  Once a column is parsed, then it is processed the
Uploader uses the provided Appendices,
[Appendix A Analyte Markers](#appendix-a-analyte-markers),
[Appendix B Non-Analyte Markers](#appendix-b-non-analyte-markers), and
[Appendix C Species Mapping](#appendix-c-species-mapping)
to map the parse form into the fcs_analyzed_result_marker table and to generate
a preferred form if all the components have preferred values. Several parsing
examples are provided in the [Parsing Examples](#parsing-examples) Section for
human. Only preferred analytes associated with a given species group
(human--9606 or mouse--10090) are considered in a given parse. Non-analyte
markers apply to all species equally.  Note that both analyte and non-analyte
marker names are case-sensitive.

# BNF Grammar for PNN/PNS Reported Markers

The basic grammar for the PNN/PNS marker data is
specified as follows. BNF categories are always identified by the angle-bracket
notation (**<..>**). Several BNF specifications below contain
**regular-expressions** defining the tokens of the grammar.  These elements use
single quoted expressions (**'...'**).

To see how a PNN/PNS marker is processed by the following BNF grammar,
see the [NOTES](#notes).

### Preprocessing Patterns BNF
```
<preProcessingPattern1> ::=   '^.*(CD)( |\-)(\d+).*$'
<preProcessingPattern2> ::=   '^.*\((CD.+)\).*$'
                            | '^.*\((Cd.+)\).*$'
```
### 
For preprocessing patterns see Notes 1 and 2 below. See [Example 6](#example-6)
for Preprocessing Pattern 1, and [Example 7](#example-7) for Preprocessing Pattern 2.
### Preferred Marker BNF
[Appendix A Analyte Markers](#appendix-a-analyte-markers) contains the current
list of analyte markers partitioned by human (9606) and mouse (10090).

[Appendix B Non-Analyte Markers](#appendix-b-non-analyte-markers) contains the
list of current non-analyte markers.

[Appendix C Species Mapping](#appendix-c-species-mapping) contains the species
that are considered in the human (9606) or mouse (10090) species group

See Note 3, for applying the test to determine an analyte or non-analyte marker.
```
<analyte_marker>     ::=   lk_analyte.immunology_symbol
                         | lk_analyte.gene_symbol 
                         | lk_analyte.protein_ontology_short_label
                         | lk_analyte_pref_mapping.analyte_reported 
<non_analyte_marker> ::=   lk_cell_population_marker.name
                         | lk_cell_pop_pref_mapping.marker_reported
<unknown_marker>     ::= '.+'
<marker>             ::=   <analyte_marker>
                         | <non_analyte_marker>
                         | <unknown_marker>
```
### Split Pattern BNF
```
<splitPattern> ::= ' +|_|/'
```
###
For splitting PNN/PNS marker into components see Note 4 below.  See
[Example 8](#example-8) for splitting into components.
### HLA Patterns BNF
```
<hlaPatterns> ::=   '^.*(HLADR|HLA\-DR|HLA DR|HLA-Dr).*$'
                  | '^.*(HLA\-.+)$'
```
###
To check a component for an HLA pattern, see Note 5 and 
see [Example 9](#example-9) for handling HLA components.
### Component Separator BNF
```
<componentSeparators> ::=  ' +or +' | '\-' | '\+' | '&'
```
###
To split a component into subcomponents, see Note 6 see [Example 10](#example-10)
for handling subcomponents.
### Special Patterns BNF
```
<specialPatterns> ::=   <specialCase1>
                      | <specialCase2>
                      | <specialCase3>
                      | <specialCase4>
                      | <specialCase5>

<specialCase1>     ::=  '^CD\d+( +\d+)+.*$'
<specialCase2>     ::=  '^CD\d\d\d\d\d\d$'
<specialCase3>     ::=  '^.+(CD.+)$'
<specialCase4>     ::=  '^(Cd\d+)Di$'
<specialCase5>     ::=  '^CD\d+(CD\d+)+.*$'
```
### 
For special cases see Notes 7, 8, 9, 10 and 11 below, respectively.  For examples
of these cases, see Examples 1 through 5, respectively.
That is, Case 1 [Example 1](#example-1), Special Case 2 [Example 2](#example-2),
Special Case 3 [Example 3](#example-3), Special Case 4 [Example 4](#example-4),
and Special Case 5 [Example 5](#example-5).
### CD and Other Marker Patterns BNF
```
<cdMarkerPattern> ::=   '^CD\d+[a-zA-Z]?$'

<markerPatterns>  ::=   '^(CD.+)\(.+$'
                      | '^(CD\d+).+$'
                      | '^(CCR.+)\-.*$'
                      | '^V(CCR\d+)$'
```
### 
To check subcomponent for a CD or Other Marker Pattern, see Note 12 and 
See [Example 11](#example-11).

## NOTES
1.  Fix CD marker patterns by removing space or hyphen (-) characters the between
CD prefix and numeric portion of PNN/PNS marker

2.  Remove parentheses around a CD/Cd marker of the PNN/PNS marker.

3.  Now determine whether the PNN/PNS marker equals an analyte marker or a
longest non-analyte marker. If this step succeeds, then the preferred marker is
determined, add it to the list of analytes for the PNN/PNS marker, and processing
for the PNN/PNS marker is completed.  If not proceed, then proceed to Note 4.
See [Appendix A Analyte Markers](#appendix-a-analyte-markers) and
[Appendix B Non-Analyte Markers](#appendix-b-non-analyte-markers) for the values
of known analyte and non-analyte markers and their corresponding preferred values.

4.  Split the PNN/PNS marker into components. For each component, replace **cD**
or **cd** with **CD**. For each component, apply Note 3 to it.  If a preferred
analyte is determined, add it uniquely into the list of analytes for the PNN/PNS
marker.  Otherwise continue processing with the following Notes for each
component.  At this point, create a list of final components that will be finally
checked in Note 13.

5.  For a component, determine if it contains an HLA marker, then replace it with
placeholder pattern and keep the value of the HLA marker.

6.  For a component, split into subcomponents.  For each subcomponent, replace
the HLA placeholder pattern with the HLA marker as found in Note 5 and also
remove any empty subcomponents. Now check special cases (Notes 7..11) for each
each subcomponent, and then determine CD markers in the subcomponent (Note 12).
If the special cases or Note 12 do not apply to a subcomponent, then add it to
the final components.

7.  Special case 1:  If the subcomponent has the format **^CD\d+( +\d+)+.*$**, then
create a set of CD markers that are added into the final components.

8.  Special case 2:  If the subcomponent has the format **^CD\d\d\d\d\d\d$**, then
create three (3) CD markers that are added into the final components.

9.  Special case 3:  If the subcomponent has the format **^.+(CD.+)$**, then add
the CD marker to the final components.

10. Special case 4:  If the subcomponent has the format **^(Cd\d+)Di$**, then add
the CD marker to the final components.

11. Special case 5:  If the subcomponent has the format **^CD\d+(CD\d+)+.*$**, then
add all the CD markers to the final components.

12. For a subcomponent, determine the CD or Other marker pattern and place it
into the final components, or else the final component.

13. For each final component, apply Note 3.  If it applies, add the preferred
analyte uniquely to the list of analytes for the PNN/PNS marker, otherwise add
the final subcomponent to the list.

# Parsing Examples

The following parsing examples are provided for illustrative purposes.

### Example 1

**All (PNN, PNS) Marker Pairs**:

**(FSC-A, FSC-A)(FSC-H, FSC-H)(SSC-A, SSC-A)(SSC-H, SSC-H)(FITC-A, CD3-19-20-15)(Pacific Orange-A, CD45)(APC-A, Slan)(APC-Cy7-A, CD16)(PE-A, CD11b)(PE-Texas Red-A, PE-Texas Red-A)(PE-Cy5-A, PE-Cy5-A)(PE-Cy7-A, CD2)(Pacific Blue-A, CD86)(Alexa Fluor 700-A, HLA-DR)(PerCP-Cy5-5-A, CD14)(Time, Time)**

**fcs_header_marker**:

| PARAMETER_NUMBER | PNN_REPORTED | PNN_PREFERRED | PNS_REPORTED | PNS_PREFERRED |
| ---------------------------|-----------------------------|-----------------------------|-----------------------------|-----------------------------|
| 1 | FSC-A | FSC-A | FSC-A | FSC-A |
| 2 | FSC-H | FSC-H | FSC-H | FSC-H |
| 3 | SSC-A | SSC | SSC-A | SSC |
| 4 | SSC-H | SSC | SSC-H | SSC |
| 5 | FITC-A | FITC-A | CD3-19-20-15 | hCD3E, hCD19, hMS4A1, hFUT4 |
| 6 | Pacific Orange-A | Pacific Orange-A | CD45 | PTPRC/iso:CD45RO |
| 7 | APC-A | APC-A | Slan | hSECISBP2L |
| 8 | APC-Cy7-A | APC-Cy7-A | CD16 | hFCGR3A |
| 9 | PE-A | PE-A | CD11b | hITGAM |
| 10 | PE-Texas Red-A | PE-Texas Red-A | PE-Texas Red-A | PE-Texas Red-A |
| 11 | PE-Cy5-A | PE-Cy5-A | PE-Cy5-A | PE-Cy5-A |
| 12 | PE-Cy7-A | PE-Cy7-A | CD2 | hCD2 |
| 13 | Pacific Blue-A | Pacific Blue-A | CD86 | hCD86 |
| 14 | Alexa Fluor 700-A | Alexa Fluor 700-A | HLA-DR | hHLA-DRA |
| 15 | PerCP-Cy5-5-A | PerCP-Cy5-5-A | CD14 | hCD14 |
| 16 | Time | Time | Time | Time |

**fcs_header.panel_preferred**:

**FSC-A|FSC-H|SSC|SSC|hCD3E, hCD19, hMS4A1, hFUT4|PTPRC/iso:CD45RO|hSECISBP2L|hFCGR3A|hITGAM|PE-Texas Red-A|PE-Cy5-A|hCD2|hCD86|hHLA-DRA|hCD14|Time**

### Example 2

**All (PNN, PNS) Marker Pairs**:

**(FSC-A, FSC-A)(FSC-H, FSC-H)(FSC-W, FSC-W)(SSC-A, SSC-A)(SSC-H, SSC-H)(SSC-W, SSC-W)(Pacific Blue-A, Foxp3)(AmCyan-A, CD141619dead)(560/40 Violet-A, CD57)(585/42 Violet-A, CD3)(610/20 Violet-A, CD45RA)(660/40 Violet-A, CD8)(710/50 Violet-A, PD1)(780/60 Violet-A, CD27)(APC-A, CXCR5)(AF 700-A, Ki67)(APC-Cy7-A, CXCR3)(FITC-A, Tbet)(PerCP-A, PerCP-A)(PE-A, Eomes)(PE-TxRed-A, CD38)(PE-Cy5-A, P16INK4a)(PE-Cy5-5-A, CD4)(PE-Cy7-A, ICOS)(Time, Time)**

**fcs_header_marker**:

| PARAMETER_NUMBER | PNN_REPORTED | PNN_PREFERRED | PNS_REPORTED | PNS_PREFERRED |
| ---------------------------|-----------------------------|-----------------------------|-----------------------------|-----------------------------|
| 1 | FSC-A | FSC-A | FSC-A | FSC-A |
| 2 | FSC-H | FSC-H | FSC-H | FSC-H |
| 3 | FSC-W | FSC-W | FSC-W | FSC-W |
| 4 | SSC-A | SSC | SSC-A | SSC |
| 5 | SSC-H | SSC | SSC-H | SSC |
| 6 | SSC-W | SSC | SSC-W | SSC |
| 7 | Pacific Blue-A | Pacific Blue-A | Foxp3 | Foxp3 |
| 8 | AmCyan-A | AmCyan-A | CD141619dead | dead, hCD14, hFCGR3A, hCD19 |
| 9 | 560/40 Violet-A | 560/40 Violet-A | CD57 | hB3GAT1 |
| 10 | 585/42 Violet-A | 585/42 Violet-A | CD3 | hCD3E |
| 11 | 610/20 Violet-A | 610/20 Violet-A | CD45RA | hPTPRC/iso:h6 |
| 12 | 660/40 Violet-A | 660/40 Violet-A | CD8 | hCD8A |
| 13 | 710/50 Violet-A | 710/50 Violet-A | PD1 | hPDCD1 |
| 14 | 780/60 Violet-A | 780/60 Violet-A | CD27 | hCD27 |
| 15 | APC-A | APC-A | CXCR5 | hCXCR5 |
| 16 | AF 700-A | AF 700-A | Ki67 | hMKI67 |
| 17 | APC-Cy7-A | APC-Cy7-A | CXCR3 | hCXCR3 |
| 18 | FITC-A | FITC-A | Tbet | Tbet |
| 19 | PerCP-A | PerCP-A | PerCP-A | PerCP-A |
| 20 | PE-A | PE-A | Eomes | Eomes |
| 21 | PE-TxRed-A | PE-TxRed-A | CD38 | hCD38 |
| 22 | PE-Cy5-A | PE-Cy5-A | P16INK4a | P16INK4a |
| 23 | PE-Cy5-5-A | PE-Cy5-5-A | CD4 | hCD4 |
| 24 | PE-Cy7-A | PE-Cy7-A | ICOS | hICOS |
| 25 | Time | Time | Time | Time |

**fcs_header.panel_preferred**:

**FSC-A|FSC-H|FSC-W|SSC|SSC|SSC|Foxp3|dead, hCD14, hFCGR3A, hCD19|hB3GAT1|hCD3E|hPTPRC/iso:h6|hCD8A|hPDCD1|hCD27|hCXCR5|hMKI67|hCXCR3|Tbet|PerCP-A|Eomes|hCD38|P16INK4a|hCD4|hICOS|Time**

### Example 3

**All (PNN, PNS) Marker Pairs**:

**(FSC-A, FSC-A)(FSC-H, FSC-H)(FSC-W, FSC-W)(SSC-A, SSC-A)(SSC-H, SSC-H)(SSC-W, SSC-W)(Red C 660/20-A, CD303-APC)(Red B 710/50-A, CD14-AF700)(Blue B 515/20-A, CD141-FITC)(Blue A 710/50-A, Dump(CD3CD19CD20CD56))(Violet H 450/50-A, CD1c-BV421)(Violet G 550/40-A, Live/Dead-Aqua)(Violet D 605/40-A, HLA-DR-BV605)(Violet B 705/70-A, CD16-BV711)(Green E 575/26-A, Clec9A-PE)(Green D 610/20-A, CD86-PECF594)(Green A 780/40-A, CD11c-PECy7)(Time, Time)**

**fcs_header_marker**:

| PARAMETER_NUMBER | PNN_REPORTED | PNN_PREFERRED | PNS_REPORTED | PNS_PREFERRED |
| ---------------------------|-----------------------------|-----------------------------|-----------------------------|-----------------------------|
| 1 | FSC-A | FSC-A | FSC-A | FSC-A |
| 2 | FSC-H | FSC-H | FSC-H | FSC-H |
| 3 | FSC-W | FSC-W | FSC-W | FSC-W |
| 4 | SSC-A | SSC | SSC-A | SSC |
| 5 | SSC-H | SSC | SSC-H | SSC |
| 6 | SSC-W | SSC | SSC-W | SSC |
| 7 | Red C 660/20-A | Red C 660/20-A | CD303-APC | hCLEC4C, APC |
| 8 | Red B 710/50-A | Red B 710/50-A | CD14-AF700 | hCD14, AF700 |
| 9 | Blue B 515/20-A | Blue B 515/20-A | CD141-FITC | hTHBD, FITC |
| 10 | Blue A 710/50-A | Blue A 710/50-A | Dump(CD3CD19CD20CD56) | hNCAM1 |
| 11 | Violet H 450/50-A | Violet H 450/50-A | CD1c-BV421 | hCD1C, BV421 |
| 12 | Violet G 550/40-A | Violet G 550/40-A | Live/Dead-Aqua | viable, Aqua |
| 13 | Violet D 605/40-A | Violet D 605/40-A | HLA-DR-BV605 | hHLA-DRA, BV605 |
| 14 | Violet B 705/70-A | Violet B 705/70-A | CD16-BV711 | hFCGR3A, BV711 |
| 15 | Green E 575/26-A | Green E 575/26-A | Clec9A-PE | Clec9A-PE |
| 16 | Green D 610/20-A | Green D 610/20-A | CD86-PECF594 | hCD86, PECF594 |
| 17 | Green A 780/40-A | Green A 780/40-A | CD11c-PECy7 | hITGAX, PECy7 |
| 18 | Time | Time | Time | Time |

**fcs_header.panel_preferred**:

**FSC-A|FSC-H|FSC-W|SSC|SSC|SSC|hCLEC4C, APC|hCD14, AF700|hTHBD, FITC|hNCAM1|hCD1C, BV421|viable, Aqua|hHLA-DRA, BV605|hFCGR3A, BV711|Clec9A-PE|hCD86, PECF594|hITGAX, PECy7|Time**

### Example 4

**All (PNN, PNS) Marker Pairs**:

**(Time, Time)(Event_length, Event_length)(Y89Di, 89Y_CD45)(Pd102Di, 102Pd)(Rh103Di, 103Rh)(Pd104Di, 104Pd)(Pd105Di, 105Pd)(Pd106Di, 106Pd)(Pd108Di, 108Pd)(Pd110Di, 110Pd)(Cd110Di, 110Cd_CD45_Q-dot)(Cd111Di, 111Cd_CD45_Q-dot)(Cd112Di, 112Cd_CD45_Q-dot)(Cd113Di, 113Cd_CD45_Q-dot)(Cd114Di, 114Cd_CD45_Q-dot)(Sn120Di, 120Sn)(I127Di, 127I)(Xe131Di, 131Xe)(Cs133Di, 133Cs)(Ba138Di, 138Ba)(Ce140Di, 140Ce)(Pr141Di, 141Pr_CD27)(Ce142Di, 142Ce)(Nd142Di, 142Nd_CD19)(Nd143Di, 143Nd_CD45RA)(Nd144Di, 144Nd_TNFa)(Nd145Di, 145Nd_CD16)(Nd146Di, 146Nd_CD8a)(Sm147Di, 147Sm_HLA-DR)(Nd148Di, 148Nd_CCR4)(Sm149Di, 149Sm_CD25)(Nd150Di, 150Nd_MIP-1b)(Eu151Di, 151Eu_CD123)(Sm152Di, 152Sm_CD14)(Eu153Di, 153Eu_CD69)(Sm154Di, 154Sm_CD185)(Gd155Di, 155Gd_CD4)(Gd156Di, 156Gd_IL-6)(Gd158Di, 158Gd_CD3)(Tb159Di, 159Tb_CD11c)(Gd160Di, 160Gd_IFNg)(Dy161Di, 161Dy_CD152)(Dy162Di, 162Dy_CD56)(Dy163Di, 163Dy_CD183)(Dy164Di, 164Dy_CD45RO)(Ho165Di, 165Ho_Foxp3)(Er166Di, 166Er_CD24)(Er167Di, 167Er_CD38)(Er168Di, 168Er_IFNb)(Tm169Di, 169Tm_TCRgd)(Er170Di, 170Er_CCR7)(Yb171Di, 171Yb_CCR6)(Yb172Di, 172Yb_IgM)(Yb173Di, 173Yb_CD57)(Yb174Di, 174Yb_CD86)(Lu175Di, 175Lu_CD279)(Lu176Di, 176Lu)(Yb176Di, 176Yb_Perforin)(BCKG190Di, 190BCKG)(Ir191Di, 191Ir_DNA1)(Ir193Di, 193Ir_DNA2)(Pt194Di, 194Pt)(Pt195Di, 195Pt_Live-Dead)(Pt198Di, 198Pt)(Pb208Di, 208Pb)(Center, Center)(Offset, Offset)(Width, Width)(Residual, Residual)**

**fcs_header_marker**:

| PARAMETER_NUMBER | PNN_REPORTED | PNN_PREFERRED | PNS_REPORTED | PNS_PREFERRED |
| ---------------------------|-----------------------------|-----------------------------|-----------------------------|-----------------------------|
| 1 | Time | Time | Time | Time |
| 2 | Event_length | Event_length | Event_length | Event_length |
| 3 | Y89Di | Y89Di | 89Y_CD45 | PTPRC/iso:CD45RO, 89Y |
| 4 | Pd102Di | Pd102Di | 102Pd | 102Pd |
| 5 | Rh103Di | Rh103Di | 103Rh | 103Rh |
| 6 | Pd104Di | Pd104Di | 104Pd | 104Pd |
| 7 | Pd105Di | Pd105Di | 105Pd | 105Pd |
| 8 | Pd106Di | Pd106Di | 106Pd | 106Pd |
| 9 | Pd108Di | Pd108Di | 108Pd | 108Pd |
| 10 | Pd110Di | Pd110Di | 110Pd | 110Pd |
| 11 | Cd110Di | Cd110Di | 110Cd_CD45_Q-dot | PTPRC/iso:CD45RO, 110Cd, dot |
| 12 | Cd111Di | Cd111Di | 111Cd_CD45_Q-dot | PTPRC/iso:CD45RO, 111Cd, dot |
| 13 | Cd112Di | Cd112Di | 112Cd_CD45_Q-dot | PTPRC/iso:CD45RO, 112Cd, dot |
| 14 | Cd113Di | Cd113Di | 113Cd_CD45_Q-dot | PTPRC/iso:CD45RO, 113Cd, dot |
| 15 | Cd114Di | Cd114Di | 114Cd_CD45_Q-dot | PTPRC/iso:CD45RO, 114Cd, dot |
| 16 | Sn120Di | Sn120Di | 120Sn | 120Sn |
| 17 | I127Di | I127Di | 127I | 127I |
| 18 | Xe131Di | Xe131Di | 131Xe | 131Xe |
| 19 | Cs133Di | Cs133Di | 133Cs | 133Cs |
| 20 | Ba138Di | Ba138Di | 138Ba | 138Ba |
| 21 | Ce140Di | Ce140Di | 140Ce | 140Ce |
| 22 | Pr141Di | Pr141Di | 141Pr_CD27 | hCD27, 141Pr |
| 23 | Ce142Di | Ce142Di | 142Ce | 142Ce |
| 24 | Nd142Di | Nd142Di | 142Nd_CD19 | hCD19, 142Nd |
| 25 | Nd143Di | Nd143Di | 143Nd_CD45RA | hPTPRC/iso:h6, 143Nd |
| 26 | Nd144Di | Nd144Di | 144Nd_TNFa | hTNF, 144Nd |
| 27 | Nd145Di | Nd145Di | 145Nd_CD16 | hFCGR3A, 145Nd |
| 28 | Nd146Di | Nd146Di | 146Nd_CD8a | hCD8A, 146Nd |
| 29 | Sm147Di | Sm147Di | 147Sm_HLA-DR | hHLA-DRA, 147Sm |
| 30 | Nd148Di | Nd148Di | 148Nd_CCR4 | hCCR4, 148Nd |
| 31 | Sm149Di | Sm149Di | 149Sm_CD25 | hIL2RA, 149Sm |
| 32 | Nd150Di | Nd150Di | 150Nd_MIP-1b | hCCL4, 150Nd |
| 33 | Eu151Di | Eu151Di | 151Eu_CD123 | hIL3RA, 151Eu |
| 34 | Sm152Di | Sm152Di | 152Sm_CD14 | hCD14, 152Sm |
| 35 | Eu153Di | Eu153Di | 153Eu_CD69 | hCD69, 153Eu |
| 36 | Sm154Di | Sm154Di | 154Sm_CD185 | hCXCR5, 154Sm |
| 37 | Gd155Di | Gd155Di | 155Gd_CD4 | hCD4, 155Gd |
| 38 | Gd156Di | Gd156Di | 156Gd_IL-6 | hIL6, 156Gd |
| 39 | Gd158Di | Gd158Di | 158Gd_CD3 | hCD3E, 158Gd |
| 40 | Tb159Di | Tb159Di | 159Tb_CD11c | hITGAX, 159Tb |
| 41 | Gd160Di | Gd160Di | 160Gd_IFNg | hIFNG, 160Gd |
| 42 | Dy161Di | Dy161Di | 161Dy_CD152 | hCTLA4, 161Dy |
| 43 | Dy162Di | Dy162Di | 162Dy_CD56 | hNCAM1, 162Dy |
| 44 | Dy163Di | Dy163Di | 163Dy_CD183 | hCXCR3, 163Dy |
| 45 | Dy164Di | Dy164Di | 164Dy_CD45RO | PTPRC/iso:CD45RO, 164Dy |
| 46 | Ho165Di | Ho165Di | 165Ho_Foxp3 | 165Ho_Foxp3 |
| 47 | Er166Di | Er166Di | 166Er_CD24 | hCD24, 166Er |
| 48 | Er167Di | Er167Di | 167Er_CD38 | hCD38, 167Er |
| 49 | Er168Di | Er168Di | 168Er_IFNb | hIFNB1, 168Er |
| 50 | Tm169Di | Tm169Di | 169Tm_TCRgd | 169Tm_TCRgd |
| 51 | Er170Di | Er170Di | 170Er_CCR7 | hCCR7, 170Er |
| 52 | Yb171Di | Yb171Di | 171Yb_CCR6 | hCCR6, 171Yb |
| 53 | Yb172Di | Yb172Di | 172Yb_IgM | hIGHM, 172Yb |
| 54 | Yb173Di | Yb173Di | 173Yb_CD57 | hB3GAT1, 173Yb |
| 55 | Yb174Di | Yb174Di | 174Yb_CD86 | hCD86, 174Yb |
| 56 | Lu175Di | Lu175Di | 175Lu_CD279 | hPDCD1, 175Lu |
| 57 | Lu176Di | Lu176Di | 176Lu | 176Lu |
| 58 | Yb176Di | Yb176Di | 176Yb_Perforin | hPRF1, 176Yb |
| 59 | BCKG190Di | BCKG190Di | 190BCKG | 190BCKG |
| 60 | Ir191Di | Ir191Di | 191Ir_DNA1 | 191Ir_DNA1 |
| 61 | Ir193Di | Ir193Di | 193Ir_DNA2 | 193Ir_DNA2 |
| 62 | Pt194Di | Pt194Di | 194Pt | 194Pt |
| 63 | Pt195Di | Pt195Di | 195Pt_Live-Dead | dead, 195Pt, Live |
| 64 | Pt198Di | Pt198Di | 198Pt | 198Pt |
| 65 | Pb208Di | Pb208Di | 208Pb | 208Pb |
| 66 | Center | Center | Center | Center |
| 67 | Offset | Offset | Offset | Offset |
| 68 | Width | Width | Width | Width |
| 69 | Residual | Residual | Residual | Residual |

**fcs_header.panel_preferred**:

**Time|Event_length|PTPRC/iso:CD45RO, 89Y|102Pd|103Rh|104Pd|105Pd|106Pd|108Pd|110Pd|PTPRC/iso:CD45RO, 110Cd, dot|PTPRC/iso:CD45RO, 111Cd, dot|PTPRC/iso:CD45RO, 112Cd, dot|PTPRC/iso:CD45RO, 113Cd, dot|PTPRC/iso:CD45RO, 114Cd, dot|120Sn|127I|131Xe|133Cs|138Ba|140Ce|hCD27, 141Pr|142Ce|hCD19, 142Nd|hPTPRC/iso:h6, 143Nd|hTNF, 144Nd|hFCGR3A, 145Nd|hCD8A, 146Nd|hHLA-DRA, 147Sm|hCCR4, 148Nd|hIL2RA, 149Sm|hCCL4, 150Nd|hIL3RA, 151Eu|hCD14, 152Sm|hCD69, 153Eu|hCXCR5, 154Sm|hCD4, 155Gd|hIL6, 156Gd|hCD3E, 158Gd|hITGAX, 159Tb|hIFNG, 160Gd|hCTLA4, 161Dy|hNCAM1, 162Dy|hCXCR3, 163Dy|PTPRC/iso:CD45RO, 164Dy|165Ho_Foxp3|hCD24, 166Er|hCD38, 167Er|hIFNB1, 168Er|169Tm_TCRgd|hCCR7, 170Er|hCCR6, 171Yb|hIGHM, 172Yb|hB3GAT1, 173Yb|hCD86, 174Yb|hPDCD1, 175Lu|176Lu|hPRF1, 176Yb|190BCKG|191Ir_DNA1|193Ir_DNA2|194Pt|dead, 195Pt, Live|198Pt|208Pb|Center|Offset|Width|Residual**

### Example 5

**All (PNN, PNS) Marker Pairs**:

**(FSC-A, FSC-A)(FSC-H, FSC-H)(FSC-W, FSC-W)(SSC-A, SSC-A)(SSC-H, SSC-H)(SSC-W, SSC-W)(R 670/30-A, CD11c -APC)(R720/40-A, CD16-ALEXA700)(R 780/60-A, CD45-APCCY7)(B 530/30-A, CD20CD3CD8-FITC)(B 710/50-A, CD123-PERPCP)(V 450/50-A, CD14-PB)(V 525/50-A, HLADR-V500)(YG 582/15-A, CD83-PE)(YG 610/20-A, CD86-PE TR)(YG 780/60-A, CD80-PE CY7)(Time, Time)**

**fcs_header_marker**:

| PARAMETER_NUMBER | PNN_REPORTED | PNN_PREFERRED | PNS_REPORTED | PNS_PREFERRED |
| ---------------------------|-----------------------------|-----------------------------|-----------------------------|-----------------------------|
| 1 | FSC-A | FSC-A | FSC-A | FSC-A |
| 2 | FSC-H | FSC-H | FSC-H | FSC-H |
| 3 | FSC-W | FSC-W | FSC-W | FSC-W |
| 4 | SSC-A | SSC | SSC-A | SSC |
| 5 | SSC-H | SSC | SSC-H | SSC |
| 6 | SSC-W | SSC | SSC-W | SSC |
| 7 | R 670/30-A | R 670/30-A | CD11c -APC | hITGAX, APC |
| 8 | R720/40-A | R720/40-A | CD16-ALEXA700 | hFCGR3A, ALEXA700 |
| 9 | R 780/60-A | R 780/60-A | CD45-APCCY7 | PTPRC/iso:CD45RO, APCCY7 |
| 10 | B 530/30-A | B 530/30-A | CD20CD3CD8-FITC | hMS4A1, hCD3E, hCD8A, FITC |
| 11 | B 710/50-A | B 710/50-A | CD123-PERPCP | hIL3RA, PERPCP |
| 12 | V 450/50-A | V 450/50-A | CD14-PB | hCD14, PB |
| 13 | V 525/50-A | V 525/50-A | HLADR-V500 | hHLA-DRA, V500 |
| 14 | YG 582/15-A | YG 582/15-A | CD83-PE | hCD83, PE |
| 15 | YG 610/20-A | YG 610/20-A | CD86-PE TR | hCD86, PE, TR |
| 16 | YG 780/60-A | YG 780/60-A | CD80-PE CY7 | hCD80, PE, CY7 |
| 17 | Time | Time | Time | Time |

**fcs_header.panel_preferred**:

**FSC-A|FSC-H|FSC-W|SSC|SSC|SSC|hITGAX, APC|hFCGR3A, ALEXA700|PTPRC/iso:CD45RO, APCCY7|hMS4A1, hCD3E, hCD8A, FITC|hIL3RA, PERPCP|hCD14, PB|hHLA-DRA, V500|hCD83, PE|hCD86, PE, TR|hCD80, PE, CY7|Time**

### Example 6

**All (PNN, PNS) Marker Pairs**:

**(FSC-H, FSC-Height)(SSC-H, SSC-Height)(FL1-H, CFSE)(FL2-H, PE HLA-DR or IgG2b)(FL4-H, APC CD 4)(Event #, Event #)(SampleID, SampleID)**

**fcs_header_marker**:

| PARAMETER_NUMBER | PNN_REPORTED | PNN_PREFERRED | PNS_REPORTED | PNS_PREFERRED |
| ---------------------------|-----------------------------|-----------------------------|-----------------------------|-----------------------------|
| 1 | FSC-H | FSC-H | FSC-Height | FSC-Height |
| 2 | SSC-H | SSC | SSC-Height | SSC, Height |
| 3 | FL1-H | FL1-H | CFSE | CFSE |
| 4 | FL2-H | FL2-H | PE HLA-DR or IgG2b | hHLA-DRA, PE, or, IgG2b |
| 5 | FL4-H | FL4-H | APC CD 4 | hCD4, APC |
| 6 | Event # | Event # | Event # | Event # |
| 7 | SampleID | SampleID | SampleID | SampleID |

**fcs_header.panel_preferred**:

**FSC-Height|SSC, Height|CFSE|hHLA-DRA, PE, or, IgG2b|hCD4, APC|Event #|SampleID**

### Example 7

**All (PNN, PNS) Marker Pairs**:

**(FSC-A, FSC-A)(FSC-H, FSC-H)(FSC-W, FSC-W)(SSC-A, SSC-A)(SSC-H, SSC-H)(SSC-W, SSC-W)(FITC-A, PD-1)(PE-A, EpCam)(PE-Texas Red-A, L/D)(PerCP-Cy5-5-A, CD4)(PE-Cy7-A, CD45RA)(APC-A, TCRgd)(Alexa Fluor 700-A, CD14)(APC-Cy7-A, CD8)(Pacific Blue-A, CD3)(AmCyan-A, HLA-DR)(QDot 545-A, QDot 545-A)(Qdot 585-A, BV605(CD11c))(Qdot 605-A, BV650(CD69))(Qdot 655-A, BV711(CD56))(Qdot 705-A, BV705(CD27))(Time, Time)**

**fcs_header_marker**:

| PARAMETER_NUMBER | PNN_REPORTED | PNN_PREFERRED | PNS_REPORTED | PNS_PREFERRED |
| ---------------------------|-----------------------------|-----------------------------|-----------------------------|-----------------------------|
| 1 | FSC-A | FSC-A | FSC-A | FSC-A |
| 2 | FSC-H | FSC-H | FSC-H | FSC-H |
| 3 | FSC-W | FSC-W | FSC-W | FSC-W |
| 4 | SSC-A | SSC | SSC-A | SSC |
| 5 | SSC-H | SSC | SSC-H | SSC |
| 6 | SSC-W | SSC | SSC-W | SSC |
| 7 | FITC-A | FITC-A | PD-1 | hPDCD1 |
| 8 | PE-A | PE-A | EpCam | EpCam |
| 9 | PE-Texas Red-A | PE-Texas Red-A | L/D | L/D |
| 10 | PerCP-Cy5-5-A | PerCP-Cy5-5-A | CD4 | hCD4 |
| 11 | PE-Cy7-A | PE-Cy7-A | CD45RA | hPTPRC/iso:h6 |
| 12 | APC-A | APC-A | TCRgd | TCRgd |
| 13 | Alexa Fluor 700-A | Alexa Fluor 700-A | CD14 | hCD14 |
| 14 | APC-Cy7-A | APC-Cy7-A | CD8 | hCD8A |
| 15 | Pacific Blue-A | Pacific Blue-A | CD3 | hCD3E |
| 16 | AmCyan-A | AmCyan-A | HLA-DR | hHLA-DRA |
| 17 | QDot 545-A | QDot 545-A | QDot 545-A | QDot 545-A |
| 18 | Qdot 585-A | Qdot 585-A | BV605(CD11c) | hITGAX |
| 19 | Qdot 605-A | Qdot 605-A | BV650(CD69) | hCD69 |
| 20 | Qdot 655-A | Qdot 655-A | BV711(CD56) | hNCAM1 |
| 21 | Qdot 705-A | Qdot 705-A | BV705(CD27) | hCD27 |
| 22 | Time | Time | Time | Time |

**fcs_header.panel_preferred**:

**FSC-A|FSC-H|FSC-W|SSC|SSC|SSC|hPDCD1|EpCam|L/D|hCD4|hPTPRC/iso:h6|TCRgd|hCD14|hCD8A|hCD3E|hHLA-DRA|QDot 545-A|hITGAX|hCD69|hNCAM1|hCD27|Time**

### Example 8

**All (PNN, PNS) Marker Pairs**:

**(FSC-A, FSC-A)(SSC-A, SSC-A)(Blue F 530/30-A, FITC CCR4)(Blue E 576/26-A, PE CXCR3)(Blue D 610/20-A, PE TX RD CD8)(Blue C 670/14-A, DUMP)(Blue B 695/40-A, PE CY 5-5 CD3)(Blue A 780/60-A, PE CY7 VCCR7)(Violet C 450/50-A, PAC BLUE CD4)(Violet B 525/50-A, PAC ORANGE CD45-RA)(Red C 660/20-A, ALEXA 647 CXCR5)(Red B 720/40-A, ALEXA 700 CD62L)(Red A 780/60-A, APC CY 7 CD25)(Time, Time)**

**fcs_header_marker**:

| PARAMETER_NUMBER | PNN_REPORTED | PNN_PREFERRED | PNS_REPORTED | PNS_PREFERRED |
| ---------------------------|-----------------------------|-----------------------------|-----------------------------|-----------------------------|
| 1 | FSC-A | FSC-A | FSC-A | FSC-A |
| 2 | SSC-A | SSC | SSC-A | SSC |
| 3 | Blue F 530/30-A | Blue F 530/30-A | FITC CCR4 | hCCR4, FITC |
| 4 | Blue E 576/26-A | Blue E 576/26-A | PE CXCR3 | hCXCR3, PE |
| 5 | Blue D 610/20-A | Blue D 610/20-A | PE TX RD CD8 | hCD8A, PE, TX, RD |
| 6 | Blue C 670/14-A | Blue C 670/14-A | DUMP | DUMP |
| 7 | Blue B 695/40-A | Blue B 695/40-A | PE CY 5-5 CD3 | hCD3E, PE, CY |
| 8 | Blue A 780/60-A | Blue A 780/60-A | PE CY7 VCCR7 | PE, CY7, hCCR7 |
| 9 | Violet C 450/50-A | Violet C 450/50-A | PAC BLUE CD4 | hCD4, PAC, BLUE |
| 10 | Violet B 525/50-A | Violet B 525/50-A | PAC ORANGE CD45-RA | PAC, ORANGE, PTPRC/iso:CD45RO, RA |
| 11 | Red C 660/20-A | Red C 660/20-A | ALEXA 647 CXCR5 | hCXCR5, ALEXA |
| 12 | Red B 720/40-A | Red B 720/40-A | ALEXA 700 CD62L | hSELL, ALEXA |
| 13 | Red A 780/60-A | Red A 780/60-A | APC CY 7 CD25 | hIL2RA, APC, CY |
| 14 | Time | Time | Time | Time |

**fcs_header.panel_preferred**:

**FSC-A|SSC|hCCR4, FITC|hCXCR3, PE|hCD8A, PE, TX, RD|DUMP|hCD3E, PE, CY|PE, CY7, hCCR7|hCD4, PAC, BLUE|PAC, ORANGE, PTPRC/iso:CD45RO, RA|hCXCR5, ALEXA|hSELL, ALEXA|hIL2RA, APC, CY|Time**

### Example 9

**All (PNN, PNS) Marker Pairs**:

**(FSC-H, FSC-Height)(SSC-H, SSC-Height)(FL1-H, CFSE)(FL2-H, PE HLA-DRor IgG2b)(FL3-H, FL3-H)(FL2-A, FL2-A)(FL4-H, FL4-H)**

**fcs_header_marker**:

| PARAMETER_NUMBER | PNN_REPORTED | PNN_PREFERRED | PNS_REPORTED | PNS_PREFERRED |
| ---------------------------|-----------------------------|-----------------------------|-----------------------------|-----------------------------|
| 1 | FSC-H | FSC-H | FSC-Height | FSC-Height |
| 2 | SSC-H | SSC | SSC-Height | SSC, Height |
| 3 | FL1-H | FL1-H | CFSE | CFSE |
| 4 | FL2-H | FL2-H | PE HLA-DRor IgG2b | PE, hHLA-DRA, or, IgG2b |
| 5 | FL3-H | FL3-H | FL3-H | FL3-H |
| 6 | FL2-A | FL2-A | FL2-A | FL2-A |
| 7 | FL4-H | FL4-H | FL4-H | FL4-H |

**fcs_header.panel_preferred**:

**FSC-Height|SSC, Height|CFSE|PE, hHLA-DRA, or, IgG2b|FL3-H|FL2-A|FL4-H**

### Example 10

**All (PNN, PNS) Marker Pairs**:

**(FSC-A, FSC-A)(SSC-A, SSC-A)(Blue F 530/30-A, FITC CCR4)(Blue E 576/26-A, PE CCR3)(Blue D 610/20-A, PE TEXAS RED CD8)(Blue C 670/14-A, 7AAD DUMP)(Blue B 695/40-A, PE CY 5-5 CD3)(Blue A 780/60-A, PE CY 7 CCR7)(Violet B 440/40-A, PACIFIC BLUE CD4)(Violet A 525/50-A, PAC ORANGE CD45-RA)(Red C 660/20-A, ALEXA 647 CXCR5)(Red B 720/40-A, ALEXA 700 CD62L)(Red A 780/60-A, APC CY 7 CD25)(Time, Time)**

**fcs_header_marker**:

| PARAMETER_NUMBER | PNN_REPORTED | PNN_PREFERRED | PNS_REPORTED | PNS_PREFERRED |
| ---------------------------|-----------------------------|-----------------------------|-----------------------------|-----------------------------|
| 1 | FSC-A | FSC-A | FSC-A | FSC-A |
| 2 | SSC-A | SSC | SSC-A | SSC |
| 3 | Blue F 530/30-A | Blue F 530/30-A | FITC CCR4 | hCCR4, FITC |
| 4 | Blue E 576/26-A | Blue E 576/26-A | PE CCR3 | hCCR3, PE |
| 5 | Blue D 610/20-A | Blue D 610/20-A | PE TEXAS RED CD8 | hCD8A, PE, TEXAS, RED |
| 6 | Blue C 670/14-A | Blue C 670/14-A | 7AAD DUMP | 7AAD DUMP |
| 7 | Blue B 695/40-A | Blue B 695/40-A | PE CY 5-5 CD3 | hCD3E, PE, CY |
| 8 | Blue A 780/60-A | Blue A 780/60-A | PE CY 7 CCR7 | hCCR7, PE, CY |
| 9 | Violet B 440/40-A | Violet B 440/40-A | PACIFIC BLUE CD4 | hCD4, PACIFIC, BLUE |
| 10 | Violet A 525/50-A | Violet A 525/50-A | PAC ORANGE CD45-RA | PAC, ORANGE, PTPRC/iso:CD45RO, RA |
| 11 | Red C 660/20-A | Red C 660/20-A | ALEXA 647 CXCR5 | hCXCR5, ALEXA |
| 12 | Red B 720/40-A | Red B 720/40-A | ALEXA 700 CD62L | hSELL, ALEXA |
| 13 | Red A 780/60-A | Red A 780/60-A | APC CY 7 CD25 | hIL2RA, APC, CY |
| 14 | Time | Time | Time | Time |

**fcs_header.panel_preferred**:

**FSC-A|SSC|hCCR4, FITC|hCCR3, PE|hCD8A, PE, TEXAS, RED|7AAD DUMP|hCD3E, PE, CY|hCCR7, PE, CY|hCD4, PACIFIC, BLUE|PAC, ORANGE, PTPRC/iso:CD45RO, RA|hCXCR5, ALEXA|hSELL, ALEXA|hIL2RA, APC, CY|Time**

### Example 11

**All (PNN, PNS) Marker Pairs**:

**(FSC-A, FSC-A)(FSC-H, FSC-H)(FSC-W, FSC-W)(SSC-A, SSC-A)(SSC-H, SSC-H)(SSC-W, SSC-W)(R 670/30-A, CD11c -APC)(R720/40-A, CD16-ALEXA700)(R 780/60-A, CD45-APCCY7)(B 530/30-A, CD20CD3CD8-FITC)(B 710/50-A, CD123-PERPCP)(V 450/50-A, CD14-PB)(V 525/50-A, HLADR-V500)(YG 582/15-A, CD83-PE)(YG 610/20-A, CD86-PE TR)(YG 780/60-A, CD80-PE CY7)(Time, Time)**

**fcs_header_marker**:

| PARAMETER_NUMBER | PNN_REPORTED | PNN_PREFERRED | PNS_REPORTED | PNS_PREFERRED |
| ---------------------------|-----------------------------|-----------------------------|-----------------------------|-----------------------------|
| 1 | FSC-A | FSC-A | FSC-A | FSC-A |
| 2 | FSC-H | FSC-H | FSC-H | FSC-H |
| 3 | FSC-W | FSC-W | FSC-W | FSC-W |
| 4 | SSC-A | SSC | SSC-A | SSC |
| 5 | SSC-H | SSC | SSC-H | SSC |
| 6 | SSC-W | SSC | SSC-W | SSC |
| 7 | R 670/30-A | R 670/30-A | CD11c -APC | hITGAX, APC |
| 8 | R720/40-A | R720/40-A | CD16-ALEXA700 | hFCGR3A, ALEXA700 |
| 9 | R 780/60-A | R 780/60-A | CD45-APCCY7 | PTPRC/iso:CD45RO, APCCY7 |
| 10 | B 530/30-A | B 530/30-A | CD20CD3CD8-FITC | hMS4A1, hCD3E, hCD8A, FITC |
| 11 | B 710/50-A | B 710/50-A | CD123-PERPCP | hIL3RA, PERPCP |
| 12 | V 450/50-A | V 450/50-A | CD14-PB | hCD14, PB |
| 13 | V 525/50-A | V 525/50-A | HLADR-V500 | hHLA-DRA, V500 |
| 14 | YG 582/15-A | YG 582/15-A | CD83-PE | hCD83, PE |
| 15 | YG 610/20-A | YG 610/20-A | CD86-PE TR | hCD86, PE, TR |
| 16 | YG 780/60-A | YG 780/60-A | CD80-PE CY7 | hCD80, PE, CY7 |
| 17 | Time | Time | Time | Time |

**fcs_header.panel_preferred**:

**FSC-A|FSC-H|FSC-W|SSC|SSC|SSC|hITGAX, APC|hFCGR3A, ALEXA700|PTPRC/iso:CD45RO, APCCY7|hMS4A1, hCD3E, hCD8A, FITC|hIL3RA, PERPCP|hCD14, PB|hHLA-DRA, V500|hCD83, PE|hCD86, PE, TR|hCD80, PE, CY7|Time**

# Appendix A Analyte Markers

The following table defines all the reported analyte markers that have have
corresponding preferred analyte marker and analyte accession values.  This table
is derived from lk_analyte (immunology_symbol, and gene_symbol,
protein_ontology_short_label) and lk_analyte_pref_mapping (analyte_reported)
tables. Analytes are partitioned by taxonomy ID.  Currently, the only species
supported include human (9606) and mouse (10090).  See
[Appendix C Species Mapping](#appendix-c-species-mapping)
for other species that are grouped into human or mouse.

| Analyte Reported | Analyte Preferred | Analyte Accession | Taxonomy ID |
| -----------------|-------------------|-------------------|-------------------|
| AA4 | hCD93 | ANA918 | 9606 |
| ABCB1 | hABCB1 | ANA996 | 9606 |
| ABCG2 | hABCG2 | ANA1260 | 9606 |
| ACE | hACE | ANA1019 | 9606 |
| ACKR1 | hACKR1 | ANA1161 | 9606 |
| ACKR3 | hACKR3 | ANA1 | 9606 |
| ADAM10 | hADAM10 | ANA948 | 9606 |
| ADAM17 | hADAM17 | ANA1133 | 9606 |
| ADAM8 | hADAM8 | ANA1131 | 9606 |
| ADGRE2 | hADGRE2 | ANA1253 | 9606 |
| ADGRE5 | hADGRE5 | ANA1120 | 9606 |
| AFP | AFP | ANA704 | 9606 |
| ALCAM | hALCAM | ANA1154 | 9606 |
| ALK | hALK | ANA1258 | 9606 |
| ANPEP | hANPEP | ANA1033 | 9606 |
| ART1 | hART1 | ANA1123 | 9606 |
| ART4 | hART4 | ANA1220 | 9606 |
| ATP1B3 | hATP1B3 | ANA1124 | 9606 |
| Ackr3 | mACKR3 | ANA475 | 10090 |
| Annexin | hANXA5 | ANA909 | 9606 |
| Anti-HLA-DR | hHLA-DRA | ANA812 | 9606 |
| B220 | PTPRC/iso:CD45RO | ANA822 | 9606 |
| B3GAT1 | hB3GAT1 | ANA823 | 9606 |
| B7 | hCD80 | ANA866 | 9606 |
| B7-1 | hCD80 | ANA866 | 9606 |
| B7-2 | hCD86 | ANA868 | 9606 |
| B7.1 | hCD80 | ANA866 | 9606 |
| B7.2 | hCD86 | ANA868 | 9606 |
| B70 | hCD86 | ANA868 | 9606 |
| BAFF | hTNFSF13B | ANA241 | 9606 |
| BCAM | hBCAM | ANA1122 | 9606 |
| BCL2 | hBCL2 | ANA904 | 9606 |
| BCL6 | hBCL6 | ANA910 | 9606 |
| BDCA-1 | hCD1C | ANA895 | 9606 |
| BDCA-2 | hCLEC4C | ANA870 | 9606 |
| BDCA-3 | hTHBD | ANA894 | 9606 |
| BDCA1 | hCD1C | ANA895 | 9606 |
| BDCA2 | hCLEC4C | ANA870 | 9606 |
| BDCA2, CD303 | hCLEC4C | ANA870 | 9606 |
| BDCA3 | hTHBD | ANA894 | 9606 |
| BDNF | BDNF | ANA701 | 9606 |
| BMPR1A | hBMPR1A | ANA1101 | 9606 |
| BMPR1B | hBMPR1B | ANA945 | 9606 |
| BOB | hGPR15 | ANA896 | 9606 |
| BSG | hBSG | ANA1098 | 9606 |
| BST1 | hBST1 | ANA1149 | 9606 |
| BST2 | hBST2 | ANA1150 | 9606 |
| BTLA | hBTLA | ANA1191 | 9606 |
| BTN3A1 | hBTN3A1 | ANA946 | 9606 |
| Bcl-2 | mBCL2 | ANA1005 | 10090 |
| Bcl-6 | mBCL6 | ANA1110 | 10090 |
| Bcl2 | mBCL2 | ANA1005 | 10090 |
| Bcl6 | mBCL6 | ANA1110 | 10090 |
| C5AR1 | hC5AR1 | ANA1063 | 9606 |
| CCL1 | hCCL1 | ANA2 | 9606 |
| CCL11 | hCCL11 | ANA3 | 9606 |
| CCL13 | hCCL13 | ANA4 | 9606 |
| CCL14 | hCCL14 | ANA5 | 9606 |
| CCL15 | hCCL15 | ANA6 | 9606 |
| CCL16 | hCCL16 | ANA7 | 9606 |
| CCL17 | CCL17 | ANA478 | 10090 |
| CCL18 | hCCL18 | ANA9 | 9606 |
| CCL19 | hCCL19 | ANA10 | 9606 |
| CCL2 | hCCL2 | ANA11 | 9606 |
| CCL20 | hCCL20 | ANA12 | 9606 |
| CCL21 | hCCL21 | ANA13 | 9606 |
| CCL22 | hCCL22 | ANA14 | 9606 |
| CCL23 | hCCL23 | ANA15 | 9606 |
| CCL24 | hCCL24 | ANA16 | 9606 |
| CCL25 | hCCL25 | ANA17 | 9606 |
| CCL26 | hCCL26 | ANA18 | 9606 |
| CCL27 | hCCL27 | ANA19 | 9606 |
| CCL3 | hCCL3 | ANA20 | 9606 |
| CCL3L1 | CCL3L1 | ANA21 | 9606 |
| CCL3L3 | hCCL3L | ANA22 | 9606 |
| CCL3P1 | CCL3 | ANA23 | 9606 |
| CCL4 | hCCL4 | ANA24 | 9606 |
| CCL4L1 | CCL4L1 | ANA25 | 9606 |
| CCL4L2 | hCCL4L | ANA26 | 9606 |
| CCL5 | hCCL5 | ANA27 | 9606 |
| CCL7 | hCCL7 | ANA28 | 9606 |
| CCL8 | hCCL8 | ANA29 | 9606 |
| CCR-9 | hCCR9 | ANA824 | 9606 |
| CCR1 | hCCR1 | ANA30 | 9606 |
| CCR10 | hCCR10 | ANA31 | 9606 |
| CCR2 | hCCR2 | ANA32 | 9606 |
| CCR3 | hCCR3 | ANA33 | 9606 |
| CCR4 | hCCR4 | ANA34 | 9606 |
| CCR5 | hCCR5 | ANA35 | 9606 |
| CCR6 | hCCR6 | ANA36 | 9606 |
| CCR7 | hCCR7 | ANA37 | 9606 |
| CCR7(Gd160)Dd | hCCR7 | ANA37 | 9606 |
| CCR8 | hCCR8 | ANA38 | 9606 |
| CCR9 | hCCR9 | ANA824 | 9606 |
| CCRL1 | hCX3CR1 | ANA59 | 9606 |
| CD10 | hMME | ANA930 | 9606 |
| CD100 | hSEMA4D | ANA1218 | 9606 |
| CD101 | hCD101 | ANA1219 | 9606 |
| CD102 | hICAM2 | ANA1025 | 9606 |
| CD103 | hITGAE | ANA877 | 9606 |
| CD104 | hITGB4 | ANA1043 | 9606 |
| CD105 | hENG | ANA1050 | 9606 |
| CD106 | VCAM1 | ANA702 | 9606 |
| CD107A | hLAMP1 | ANA887 | 9606 |
| CD107a | hLAMP1 | ANA887 | 9606 |
| CD107b | hLAMP2 | ANA1024 | 9606 |
| CD108 | hSEMA7A | ANA965 | 9606 |
| CD109 | hCD109 | ANA1188 | 9606 |
| CD110 | hMPL | ANA196 | 9606 |
| CD111 | hNECTIN1 | ANA1158 | 9606 |
| CD112 | hNECTIN2 | ANA1217 | 9606 |
| CD114 | hCSF3R | ANA57 | 9606 |
| CD115 | hCSF1R | ANA52 | 9606 |
| CD116 | hCSF2RA | ANA54 | 9606 |
| CD117 | hKIT | ANA185 | 9606 |
| CD118 | hLIFR | ANA191 | 9606 |
| CD119 | hIFNGR1 | ANA111 | 9606 |
| CD11B | hITGAM | ANA878 | 9606 |
| CD11C V450-A | hITGAX | ANA814 | 9606 |
| CD11a | hITGAL | ANA1059 | 9606 |
| CD11b | hITGAM | ANA878 | 9606 |
| CD11c | hITGAX | ANA814 | 9606 |
| CD11d | hITGAD | ANA1153 | 9606 |
| CD120a | hTNFRSF1A | ANA231 | 9606 |
| CD120b | hTNFRSF1B | ANA232 | 9606 |
| CD121A | hIL1R1 | ANA145 | 9606 |
| CD121b | hIL1R2 | ANA146 | 9606 |
| CD122 | hIL2RB | ANA164 | 9606 |
| CD123 | hIL3RA | ANA173 | 9606 |
| CD124 | hIL4R | ANA175 | 9606 |
| CD126 | hIL6R | ANA179 | 9606 |
| CD127 | hIL7R | ANA182 | 9606 |
| CD129 | hIL9R | ANA184 | 9606 |
| CD13 | hANPEP | ANA1033 | 9606 |
| CD130 | hIL6ST | ANA180 | 9606 |
| CD131 | hCSF2RB | ANA55 | 9606 |
| CD132 | hIL2RG | ANA165 | 9606 |
| CD133 | hPROM1 | ANA954 | 9606 |
| CD134 | hTNFRSF4 | ANA234 | 9606 |
| CD135 | hFLT3 | ANA89 | 9606 |
| CD136 | hMST1R | ANA198 | 9606 |
| CD137 | hTNFRSF9 | ANA236 | 9606 |
| CD138 | hSDC1 | ANA891 | 9606 |
| CD14 | hCD14 | ANA804 | 9606 |
| CD14 APC C7-A | hCD14 | ANA804 | 9606 |
| CD14(Sm154)Dd | hCD14 | ANA804 | 9606 |
| CD14/CD3 | hCD14 | ANA804 | 9606 |
| CD140a | hPDGFRA | ANA203 | 9606 |
| CD140b | hPDGFRB | ANA204 | 9606 |
| CD141 | hTHBD | ANA894 | 9606 |
| CD142 | hF3 | ANA1028 | 9606 |
| CD143 | hACE | ANA1019 | 9606 |
| CD144 | hCDH5 | ANA1095 | 9606 |
| CD146 | hMCAM | ANA1115 | 9606 |
| CD147 | hBSG | ANA1098 | 9606 |
| CD148 | hPTPRJ | ANA1151 | 9606 |
| CD15 | hFUT4 | ANA875 | 9606 |
| CD150 | hSLAMF1 | ANA1152 | 9606 |
| CD151 | hCD151 | ANA1119 | 9606 |
| CD152 | hCTLA4 | ANA871 | 9606 |
| CD153 | hTNFSF8 | ANA246 | 9606 |
| CD154 | hCD40LG | ANA43 | 9606 |
| CD155 | hPVR | ANA1034 | 9606 |
| CD156A | hADAM8 | ANA1131 | 9606 |
| CD156B | hADAM17 | ANA1133 | 9606 |
| CD156c | hADAM10 | ANA948 | 9606 |
| CD157 | hBST1 | ANA1149 | 9606 |
| CD158A | hKIR2DL1 | ANA879 | 9606 |
| CD158B1 | hKIR2DL2 | ANA880 | 9606 |
| CD158B2 | hKIR2DL3 | ANA881 | 9606 |
| CD158D | hKIR2DL4 | ANA1224 | 9606 |
| CD158E1 | hKIR3DL1 | ANA882 | 9606 |
| CD158F | hKIR2DL5A | ANA1199 | 9606 |
| CD158G | hKIR2DS5 | ANA1156 | 9606 |
| CD158H | hKIR2DS1 | ANA1157 | 9606 |
| CD158J | hKIR2DS2 | ANA1117 | 9606 |
| CD158a | hKIR2DL1 | ANA879 | 9606 |
| CD158b1 | hKIR2DL2 | ANA880 | 9606 |
| CD158b2 | hKIR2DL3 | ANA881 | 9606 |
| CD158e | mKir3dl1 | ANA1134 | 10090 |
| CD158e1 | hKIR3DL1 | ANA882 | 9606 |
| CD158e1/2 | hKIR3DL1 | ANA882 | 9606 |
| CD158i | hKIR2DS4 | ANA1118 | 9606 |
| CD158k | hKIR3DL2 | ANA1116 | 9606 |
| CD158z | hKIR3DL3 | ANA1204 | 9606 |
| CD159A | hKLRC1 | ANA861 | 9606 |
| CD159a | hKLRC1 | ANA861 | 9606 |
| CD159c | hKLRC2 | ANA1080 | 9606 |
| CD16 | hFCGR3A | ANA811 | 9606 |
| CD16 PE Cy7-A | hFCGR3A | ANA811 | 9606 |
| CD16(Sm149)Dd | hFCGR3A | ANA811 | 9606 |
| CD160 | hCD160 | ANA973 | 9606 |
| CD161 | hKLRB1 | ANA883 | 9606 |
| CD162 | hSELPLG | ANA903 | 9606 |
| CD163 | hCD163 | ANA1192 | 9606 |
| CD164 | hCD164 | ANA1141 | 9606 |
| CD166 | hALCAM | ANA1154 | 9606 |
| CD167 | hDDR1 | ANA1145 | 9606 |
| CD168 | hHMMR | ANA966 | 9606 |
| CD169 | hSIGLEC1 | ANA1227 | 9606 |
| CD16a | hFCGR3A | ANA811 | 9606 |
| CD16b | hFCGR3B | ANA960 | 9606 |
| CD170 | hSIGLEC5 | ANA951 | 9606 |
| CD171 | hL1CAM | ANA1092 | 9606 |
| CD172a | hSIRPA | ANA1130 | 9606 |
| CD172b | hSIRPB1 | ANA935 | 9606 |
| CD172g | hSIRPG | ANA1247 | 9606 |
| CD174 | hFUT3 | ANA1061 | 9606 |
| CD177 | hCD177 | ANA1203 | 9606 |
| CD178 | hFASLG | ANA86 | 9606 |
| CD179B | hIGLL1 | ANA1040 | 9606 |
| CD179a | hVPREB1 | ANA1017 | 9606 |
| CD18 | hITGB2 | ANA985 | 9606 |
| CD180 | hCD180 | ANA1223 | 9606 |
| CD181 | hCXCR1 | ANA74 | 9606 |
| CD182 | hCXCR2 | ANA75 | 9606 |
| CD183 | hCXCR3 | ANA76 | 9606 |
| CD184 | hCXCR4 | ANA77 | 9606 |
| CD185 | hCXCR5 | ANA78 | 9606 |
| CD186 | hCXCR6 | ANA79 | 9606 |
| CD19 | hCD19 | ANA805 | 9606 |
| CD19(Nd142)Dd | hCD19 | ANA805 | 9606 |
| CD191 | hCCR1 | ANA30 | 9606 |
| CD192 | hCCR2 | ANA32 | 9606 |
| CD193 | hCCR3 | ANA33 | 9606 |
| CD194 | hCCR4 | ANA34 | 9606 |
| CD194 PE Cy7-A | hCCR4 | ANA34 | 9606 |
| CD195 | hCCR5 | ANA35 | 9606 |
| CD196 | hCCR6 | ANA36 | 9606 |
| CD197 | hCCR7 | ANA37 | 9606 |
| CD1A | hCD1A | ANA988 | 9606 |
| CD1B | hCD1B | ANA1084 | 9606 |
| CD1C | hCD1C | ANA895 | 9606 |
| CD1D | hCD1D | ANA1039 | 9606 |
| CD1E | hCD1E | ANA1038 | 9606 |
| CD1a | hCD1A | ANA988 | 9606 |
| CD1b | hCD1B | ANA1084 | 9606 |
| CD1c | hCD1C | ANA895 | 9606 |
| CD1d | hCD1D | ANA1039 | 9606 |
| CD1e | hCD1E | ANA1038 | 9606 |
| CD2 | hCD2 | ANA860 | 9606 |
| CD20 | hMS4A1 | ANA806 | 9606 |
| CD20 PerCP Cy 5-5-A | hMS4A1 | ANA806 | 9606 |
| CD20(Dy164)Dd | hMS4A1 | ANA806 | 9606 |
| CD200 | hCD200 | ANA1111 | 9606 |
| CD201 | hPROCR | ANA1259 | 9606 |
| CD202b | hTEK | ANA1139 | 9606 |
| CD203c | hENPP3 | ANA947 | 9606 |
| CD204 | hMSR1 | ANA1064 | 9606 |
| CD205 | hLY75 | ANA937 | 9606 |
| CD206 | hMRC1 | ANA1072 | 9606 |
| CD207 | hCD207 | ANA1255 | 9606 |
| CD208 | hLAMP3 | ANA1261 | 9606 |
| CD209 | hCD209 | ANA869 | 9606 |
| CD21 | hCR2 | ANA919 | 9606 |
| CD210 | hIL10RA | ANA119 | 9606 |
| CD212 | hIL12RB1 | ANA125 | 9606 |
| CD213 | hIL13RA1 | ANA128 | 9606 |
| CD213A1 | hIL13RA1 | ANA128 | 9606 |
| CD213A2 | hIL13RA2 | ANA129 | 9606 |
| CD213a1 | hIL13RA1 | ANA128 | 9606 |
| CD213a2 | hIL13RA2 | ANA129 | 9606 |
| CD215 | hIL15RA | ANA131 | 9606 |
| CD22 | hCD22 | ANA862 | 9606 |
| CD220 | hINSR | ANA989 | 9606 |
| CD221 | hIGF1R | ANA993 | 9606 |
| CD222 | hIGF2R | ANA1013 | 9606 |
| CD223 | hLAG3 | ANA1054 | 9606 |
| CD224 | hGGT1 | ANA1058 | 9606 |
| CD225 | hIFITM1 | ANA1021 | 9606 |
| CD226 | hCD226 | ANA1160 | 9606 |
| CD227 | hMUC1 | ANA1041 | 9606 |
| CD228 | hMELTF | ANA998 | 9606 |
| CD229 | hLY9 | ANA1235 | 9606 |
| CD23 | hFCER2 | ANA922 | 9606 |
| CD230 | hPRNP | ANA936 | 9606 |
| CD231 | hTSPAN7 | ANA1113 | 9606 |
| CD232 | hPLXNC1 | ANA958 | 9606 |
| CD233 | hSLC4A1 | ANA977 | 9606 |
| CD234 | hACKR1 | ANA1161 | 9606 |
| CD235a | hGYPA | ANA976 | 9606 |
| CD235b | hGYPB | ANA987 | 9606 |
| CD236R | hGYPC | ANA983 | 9606 |
| CD238 | hKEL | ANA1073 | 9606 |
| CD239 | hBCAM | ANA1122 | 9606 |
| CD24 | hCD24 | ANA807 | 9606 |
| CD24(Er168)Dd | hCD24 | ANA807 | 9606 |
| CD240CE | hRHCE | ANA1053 | 9606 |
| CD240D | hRHD | ANA1138 | 9606 |
| CD241 | hRHAG | ANA1137 | 9606 |
| CD242 | hICAM4 | ANA1155 | 9606 |
| CD243 | hABCB1 | ANA996 | 9606 |
| CD244 | hCD244 | ANA1226 | 9606 |
| CD246 | hALK | ANA1258 | 9606 |
| CD247 | hCD247 | ANA1060 | 9606 |
| CD248 | hCD248 | ANA1236 | 9606 |
| CD249 | hENPEP | ANA1142 | 9606 |
| CD25 | hIL2RA | ANA163 | 9606 |
| CD25 407A-A | hIL2RA | ANA163 | 9606 |
| CD25(Yb176)Dd | hIL2RA | ANA163 | 9606 |
| CD252 | hTNFSF4 | ANA245 | 9606 |
| CD253 | hTNFSF10 | ANA237 | 9606 |
| CD254 | hTNFSF11 | ANA238 | 9606 |
| CD256 | hTNFSF13 | ANA240 | 9606 |
| CD257 | hTNFSF13B | ANA241 | 9606 |
| CD258 | hTNFSF14 | ANA242 | 9606 |
| CD26 | hDPP4 | ANA1081 | 9606 |
| CD261 | hTNFRSF10A | ANA221 | 9606 |
| CD262 | hTNFRSF10B | ANA222 | 9606 |
| CD263 | hTNFRSF10C | ANA223 | 9606 |
| CD264 | hTNFRSF10D | ANA224 | 9606 |
| CD265 | hTNFRSF11A | ANA225 | 9606 |
| CD266 | hTNFRSF12A | ANA1240 | 9606 |
| CD267 | hTNFRSF13B | ANA227 | 9606 |
| CD268 | hTNFRSF13C | ANA1222 | 9606 |
| CD269 | hTNFRSF17 | ANA229 | 9606 |
| CD27 | hCD27 | ANA40 | 9606 |
| CD27(Sm152)Dd | hCD27 | ANA40 | 9606 |
| CD270 | hTNFRSF14 | ANA228 | 9606 |
| CD271 | hNGFR | ANA994 | 9606 |
| CD272 | hBTLA | ANA1191 | 9606 |
| CD273 | hPDCD1LG2 | ANA931 | 9606 |
| CD274 | hCD274 | ANA1246 | 9606 |
| CD275 | hICOSLG | ANA964 | 9606 |
| CD276 | hCD276 | ANA1169 | 9606 |
| CD277 | hBTN3A1 | ANA946 | 9606 |
| CD278 | hICOS | ANA898 | 9606 |
| CD279 | hPDCD1 | ANA818 | 9606 |
| CD28 | hCD28 | ANA863 | 9606 |
| CD280 | hMRC2 | ANA1251 | 9606 |
| CD281 | hTLR1 | ANA1159 | 9606 |
| CD282 | hTLR2 | ANA959 | 9606 |
| CD283 | hTLR3 | ANA952 | 9606 |
| CD284 | hTLR4 | ANA944 | 9606 |
| CD286 | hTLR6 | ANA867 | 9606 |
| CD288 | hTLR8 | ANA1245 | 9606 |
| CD289 | hTLR9 | ANA1244 | 9606 |
| CD28LG | hCD80 | ANA866 | 9606 |
| CD28LG1 | hCD80 | ANA866 | 9606 |
| CD28LG2 | hCD86 | ANA868 | 9606 |
| CD29 | hITGB1 | ANA986 | 9606 |
| CD290 | hTLR10 | ANA1225 | 9606 |
| CD292 | hBMPR1A | ANA1101 | 9606 |
| CD294 | hPTGDR2 | ANA1264 | 9606 |
| CD295 | hLEPR | ANA899 | 9606 |
| CD296 | hART1 | ANA1123 | 9606 |
| CD297 | hART4 | ANA1220 | 9606 |
| CD298 | hATP1B3 | ANA1124 | 9606 |
| CD299 | hCLEC4M | ANA1233 | 9606 |
| CD3 | hCD3E | ANA809 | 9606 |
| CD3 407E-A | hCD3E | ANA809 | 9606 |
| CD3 APC Cy7-A | hCD3E | ANA809 | 9606 |
| CD3(Nd150)Dd | hCD3E | ANA809 | 9606 |
| CD30 | hTNFRSF8 | ANA235 | 9606 |
| CD300A | hCD300A | ANA1252 | 9606 |
| CD300C | hCD300C | ANA1146 | 9606 |
| CD300E | hCD300E | ANA1167 | 9606 |
| CD300a | hCD300A | ANA1252 | 9606 |
| CD300c | hCD300C | ANA1146 | 9606 |
| CD300e | hCD300E | ANA1167 | 9606 |
| CD301 | hCLEC10A | ANA1195 | 9606 |
| CD302 | hCD302 | ANA1196 | 9606 |
| CD303 | hCLEC4C | ANA870 | 9606 |
| CD304 | hNRP1 | ANA949 | 9606 |
| CD305 | hLAIR1 | ANA1180 | 9606 |
| CD306 | hLAIR2 | ANA1181 | 9606 |
| CD309 | hKDR | ANA1100 | 9606 |
| CD31 | hPECAM1 | ANA1044 | 9606 |
| CD312 | hADGRE2 | ANA1253 | 9606 |
| CD314 | hKLRK1 | ANA886 | 9606 |
| CD315 | hPTGFRN | ANA1248 | 9606 |
| CD316 | hIGSF8 | ANA1221 | 9606 |
| CD317 | hBST2 | ANA1150 | 9606 |
| CD318 | hCDCP1 | ANA1234 | 9606 |
| CD319 | hSLAMF7 | ANA1242 | 9606 |
| CD320 | hCD320 | ANA1241 | 9606 |
| CD321 | hF11R | ANA1265 | 9606 |
| CD322 | hJAM2 | ANA1126 | 9606 |
| CD324 | hCDH1 | ANA1020 | 9606 |
| CD326 | hEPCAM | ANA1045 | 9606 |
| CD32A | hFCGR2A | ANA1018 | 9606 |
| CD32B | hFCGR2B | ANA1088 | 9606 |
| CD32C | hFCGR2C | ANA1089 | 9606 |
| CD33 | hCD33 | ANA864 | 9606 |
| CD331 | hFGFR1 | ANA1009 | 9606 |
| CD332 | hFGFR2 | ANA1065 | 9606 |
| CD333 | hFGFR3 | ANA1070 | 9606 |
| CD334 | hFGFR4 | ANA1069 | 9606 |
| CD335 | hNCR1 | ANA967 | 9606 |
| CD336 | hNCR2 | ANA885 | 9606 |
| CD337 | hNCR3 | ANA950 | 9606 |
| CD339 | hJAG1 | ANA1132 | 9606 |
| CD34 | hCD34 | ANA1083 | 9606 |
| CD340 | hERBB2 | ANA982 | 9606 |
| CD344 | hFZD4 | ANA1256 | 9606 |
| CD349 | hFZD9 | ANA943 | 9606 |
| CD35 | hCR1 | ANA1051 | 9606 |
| CD350 | hFZD10 | ANA1257 | 9606 |
| CD36 | hCD36 | ANA1047 | 9606 |
| CD37 | hCD37 | ANA1008 | 9606 |
| CD38 | hCD38 | ANA808 | 9606 |
| CD38 532D-A | hCD38 | ANA808 | 9606 |
| CD38 PE-A | hCD38 | ANA808 | 9606 |
| CD38(Eu151)Dd | hCD38 | ANA808 | 9606 |
| CD39 | hENTPD1 | ANA921 | 9606 |
| CD3D | hCD3D | ANA979 | 9606 |
| CD3E | hCD3E | ANA809 | 9606 |
| CD3G | hCD3G | ANA1003 | 9606 |
| CD3d | hCD3D | ANA979 | 9606 |
| CD3e | hCD3E | ANA809 | 9606 |
| CD3g | hCD3G | ANA1003 | 9606 |
| CD4 | hCD4 | ANA41 | 9606 |
| CD4 407B-A | hCD4 | ANA41 | 9606 |
| CD4 Alexa700-A | hCD4 | ANA41 | 9606 |
| CD4 PerCP Cy 5-5-A | hCD4 | ANA41 | 9606 |
| CD4(Nd143)Dd | hCD4 | ANA41 | 9606 |
| CD40 | hCD40 | ANA42 | 9606 |
| CD40L | hCD40LG | ANA43 | 9606 |
| CD40LG | hCD40LG | ANA43 | 9606 |
| CD41 | hITGA2B | ANA997 | 9606 |
| CD42a | hGP9 | ANA1032 | 9606 |
| CD42b | hGP1BA | ANA992 | 9606 |
| CD42c | hGP1BB | ANA1022 | 9606 |
| CD42d | hGP5 | ANA1103 | 9606 |
| CD43 | hSPN | ANA893 | 9606 |
| CD44 | hCD44 | ANA914 | 9606 |
| CD44R | hCD44 | ANA914 | 9606 |
| CD45 | PTPRC/iso:CD45RO | ANA822 | 9606 |
| CD45RA | hPTPRC/iso:h6 | ANA816 | 9606 |
| CD45RA(Dy162)Dd | hPTPRC/iso:h6 | ANA816 | 9606 |
| CD45RO | PTPRC/iso:CD45RO | ANA822 | 9606 |
| CD45RO FITC-A | PTPRC/iso:CD45RO | ANA822 | 9606 |
| CD45RO_old | PTPRC/iso:CD45RO | ANA822 | 9606 |
| CD46 | hCD46 | ANA1036 | 9606 |
| CD47 | hCD47 | ANA1147 | 9606 |
| CD48 | hCD48 | ANA1001 | 9606 |
| CD49 | hITGA6 | ANA876 | 9606 |
| CD49a | hITGA1 | ANA927 | 9606 |
| CD49b | hITGA2 | ANA1048 | 9606 |
| CD49c | hITGA3 | ANA1079 | 9606 |
| CD49d | hITGA4 | ANA1026 | 9606 |
| CD49e | hITGA5 | ANA999 | 9606 |
| CD49f | hITGA6 | ANA876 | 9606 |
| CD5 | hCD5 | ANA915 | 9606 |
| CD50 | hICAM3 | ANA1094 | 9606 |
| CD51 | hITGAV | ANA991 | 9606 |
| CD52 | hCD52 | ANA1087 | 9606 |
| CD53 | hCD53 | ANA1057 | 9606 |
| CD54 | ICAM1 | ANA705 | 9606 |
| CD55 | hCD55 | ANA995 | 9606 |
| CD56 | hNCAM1 | ANA815 | 9606 |
| CD56 PE-A | hNCAM1 | ANA815 | 9606 |
| CD56(Yb174)Dd | hNCAM1 | ANA815 | 9606 |
| CD57 | hB3GAT1 | ANA823 | 9606 |
| CD58 | hCD58 | ANA1056 | 9606 |
| CD59 | hCD59 | ANA1030 | 9606 |
| CD6 | hCD6 | ANA1085 | 9606 |
| CD61 | hITGB3 | ANA984 | 9606 |
| CD62E | hSELE | ANA1046 | 9606 |
| CD62L | hSELL | ANA712 | 9606 |
| CD62P | hSELP | ANA1042 | 9606 |
| CD63 | hCD63 | ANA902 | 9606 |
| CD64 | hFCGR1A | ANA873 | 9606 |
| CD64A | hFCGR1A | ANA873 | 9606 |
| CD66a | hCEACAM1 | ANA1027 | 9606 |
| CD66b | hCEACAM8 | ANA1091 | 9606 |
| CD66c | hCEACAM6 | ANA1105 | 9606 |
| CD66d | hCEACAM3 | ANA1104 | 9606 |
| CD66e | hCEACAM5 | ANA990 | 9606 |
| CD66f | hPSG1 | ANA1010 | 9606 |
| CD68 | hCD68 | ANA1096 | 9606 |
| CD69 | hCD69 | ANA865 | 9606 |
| CD7 | hCD7 | ANA1002 | 9606 |
| CD70 | hCD70 | ANA44 | 9606 |
| CD71 | hTFRC | ANA932 | 9606 |
| CD71a | hTFRC | ANA932 | 9606 |
| CD72 | hCD72 | ANA1066 | 9606 |
| CD73 | hNT5E | ANA1062 | 9606 |
| CD74 | hCD74 | ANA978 | 9606 |
| CD79A | hCD79A | ANA1015 | 9606 |
| CD79B | hCD79B | ANA1109 | 9606 |
| CD79a | hCD79A | ANA1015 | 9606 |
| CD79b | hCD79B | ANA1109 | 9606 |
| CD8 | hCD8A | ANA810 | 9606 |
| CD8 407F-A | hCD8A | ANA810 | 9606 |
| CD8(Nd144)Dd | hCD8A | ANA810 | 9606 |
| CD80 | hCD80 | ANA866 | 9606 |
| CD81 | hCD81 | ANA1129 | 9606 |
| CD82 | hCD82 | ANA1082 | 9606 |
| CD83 | hCD83 | ANA916 | 9606 |
| CD84 | hCD84 | ANA1254 | 9606 |
| CD85J | hLILRB1 | ANA888 | 9606 |
| CD85a | hLILRB3 | ANA962 | 9606 |
| CD85b | hLILRA6 | ANA1182 | 9606 |
| CD85c | hLILRB5 | ANA963 | 9606 |
| CD85d | hLILRB2 | ANA1201 | 9606 |
| CD85e | hLILRA3 | ANA1202 | 9606 |
| CD85f | hLILRA5 | ANA941 | 9606 |
| CD85g | hLILRA4 | ANA1128 | 9606 |
| CD85h | hLILRA2 | ANA1200 | 9606 |
| CD85i | hLILRA1 | ANA961 | 9606 |
| CD85j | hLILRB1 | ANA888 | 9606 |
| CD85k | hLILRB4 | ANA1205 | 9606 |
| CD86 | hCD86 | ANA868 | 9606 |
| CD86-2 | hCD86 | ANA868 | 9606 |
| CD87 | hPLAUR | ANA1140 | 9606 |
| CD88 | hC5AR1 | ANA1063 | 9606 |
| CD89 | hFCAR | ANA1075 | 9606 |
| CD8A | hCD8A | ANA810 | 9606 |
| CD8B | hCD8B | ANA1007 | 9606 |
| CD8_new | hCD8A | ANA810 | 9606 |
| CD8a | mCD8A | ANA974 | 10090 |
| CD8b | hCD8B | ANA1007 | 9606 |
| CD9 | hCD9 | ANA1068 | 9606 |
| CD90 | hTHY1 | ANA934 | 9606 |
| CD91 | hLRP1 | ANA1144 | 9606 |
| CD93 | hCD93 | ANA918 | 9606 |
| CD94 | hKLRD1 | ANA884 | 9606 |
| CD95 | hFAS | ANA85 | 9606 |
| CD96 | hCD96 | ANA1106 | 9606 |
| CD97 | hADGRE5 | ANA1120 | 9606 |
| CD98 | hSLC7A5 | ANA1136 | 9606 |
| CD99 | hCD99 | ANA1031 | 9606 |
| CDCP1 | hCDCP1 | ANA1234 | 9606 |
| CDH1 | hCDH1 | ANA1020 | 9606 |
| CDH2 | hCDH2 | ANA1055 | 9606 |
| CDH5 | hCDH5 | ANA1095 | 9606 |
| CDW210B | hIL10RB | ANA120 | 9606 |
| CDW92 | hSLC44A1 | ANA1211 | 9606 |
| CDw113 | hNECTIN3 | ANA1243 | 9606 |
| CDw125 | hIL5RA | ANA177 | 9606 |
| CDw198 | hCCR8 | ANA38 | 9606 |
| CDw199 | hCCR9 | ANA824 | 9606 |
| CDw217 | hIL17RA | ANA138 | 9606 |
| CDw218a | hIL18R1 | ANA140 | 9606 |
| CDw218b | hIL18RAP | ANA972 | 9606 |
| CDw293 | hBMPR1B | ANA945 | 9606 |
| CDw325 | hCDH2 | ANA1055 | 9606 |
| CDw327 | hSIGLEC6 | ANA955 | 9606 |
| CDw328 | hSIGLEC7 | ANA1262 | 9606 |
| CDw329 | hSIGLEC9 | ANA1263 | 9606 |
| CDw338 | hABCG2 | ANA1260 | 9606 |
| CEACAM1 | hCEACAM1 | ANA1027 | 9606 |
| CEACAM3 | hCEACAM3 | ANA1104 | 9606 |
| CEACAM5 | hCEACAM5 | ANA990 | 9606 |
| CEACAM6 | hCEACAM6 | ANA1105 | 9606 |
| CEACAM8 | hCEACAM8 | ANA1091 | 9606 |
| CENPB | hCENPB | ANA821 | 9606 |
| CKLF | hCKLF | ANA45 | 9606 |
| CLA | hSELPLG | ANA903 | 9606 |
| CLA, CD162 | hSELPLG | ANA903 | 9606 |
| CLCF1 | hCLCF1 | ANA46 | 9606 |
| CLEC10A | hCLEC10A | ANA1195 | 9606 |
| CLEC4C | hCLEC4C | ANA870 | 9606 |
| CLEC4M | hCLEC4M | ANA1233 | 9606 |
| CMTM1 | hCMTM1 | ANA47 | 9606 |
| CMTM6 | hCMTM6 | ANA48 | 9606 |
| CMTM7 | hCMTM7 | ANA49 | 9606 |
| CNTFR | hCNTFR | ANA50 | 9606 |
| CR1 | hCR1 | ANA1051 | 9606 |
| CSF1 | hCSF1 | ANA51 | 9606 |
| CSF1R | hCSF1R | ANA52 | 9606 |
| CSF2 | hCSF2 | ANA53 | 9606 |
| CSF2RA | hCSF2RA | ANA54 | 9606 |
| CSF2RB | hCSF2RB | ANA55 | 9606 |
| CSF3 | hCSF3 | ANA56 | 9606 |
| CSF3R | hCSF3R | ANA57 | 9606 |
| CTACK | hCCL27 | ANA19 | 9606 |
| CTLA4 | hCTLA4 | ANA871 | 9606 |
| CX3CL1 | hCX3CL1 | ANA58 | 9606 |
| CX3CR1 | hCX3CR1 | ANA59 | 9606 |
| CX3CR1-2 | hCX3CR1 | ANA59 | 9606 |
| CXCL1 | hCXCL1 | ANA60 | 9606 |
| CXCL10 | hCXCL10 | ANA61 | 9606 |
| CXCL11 | hCXCL11 | ANA62 | 9606 |
| CXCL12 | hCXCL12 | ANA63 | 9606 |
| CXCL13 | hCXCL13 | ANA64 | 9606 |
| CXCL14 | hCXCL14 | ANA65 | 9606 |
| CXCL16 | hCXCL16 | ANA66 | 9606 |
| CXCL17 | hCXCL17 | ANA67 | 9606 |
| CXCL2 | hCXCL2 | ANA68 | 9606 |
| CXCL3 | hCXCL3 | ANA69 | 9606 |
| CXCL5 | hCXCL5 | ANA70 | 9606 |
| CXCL6 | hCXCL6 | ANA71 | 9606 |
| CXCL8 | hCXCL8 | ANA72 | 9606 |
| CXCL9 | hCXCL9 | ANA73 | 9606 |
| CXCR1 | hCXCR1 | ANA74 | 9606 |
| CXCR2 | hCXCR2 | ANA75 | 9606 |
| CXCR3 | hCXCR3 | ANA76 | 9606 |
| CXCR4 | hCXCR4 | ANA77 | 9606 |
| CXCR5 | hCXCR5 | ANA78 | 9606 |
| CXCR6 | hCXCR6 | ANA79 | 9606 |
| Caspase-3 | hCASP3 | ANA911 | 9606 |
| Ccl1 | mCCL1 | ANA476 | 10090 |
| Ccl11 | mCCL11 | ANA477 | 10090 |
| Ccl17 | CCL17 | ANA478 | 10090 |
| Ccl19 | mCcl19 | ANA479 | 10090 |
| Ccl2 | mCCL2 | ANA480 | 10090 |
| Ccl20 | mCCL20 | ANA481 | 10090 |
| Ccl21a | mCcl21a | ANA482 | 10090 |
| Ccl22 | mCCL22 | ANA483 | 10090 |
| Ccl24 | mCCL24 | ANA484 | 10090 |
| Ccl25 | mCcl25 | ANA485 | 10090 |
| Ccl26 | CCL26 | ANA486 | 10090 |
| Ccl27a | mCCL27 | ANA487 | 10090 |
| Ccl3 | mCCL3 | ANA488 | 10090 |
| Ccl4 | mCCL4 | ANA489 | 10090 |
| Ccl5 | mCCL5 | ANA490 | 10090 |
| Ccl7 | mCCL7 | ANA491 | 10090 |
| Ccl8 | mCcl8 | ANA492 | 10090 |
| Ccr1 | mCCR1 | ANA493 | 10090 |
| Ccr10 | mCCR10 | ANA494 | 10090 |
| Ccr2 | mCCR2 | ANA495 | 10090 |
| Ccr3 | mCCR3 | ANA496 | 10090 |
| Ccr4 | mCCR4 | ANA497 | 10090 |
| Ccr5 | mCCR5 | ANA498 | 10090 |
| Ccr6 | mCCR6 | ANA499 | 10090 |
| Ccr7 | mCCR7 | ANA500 | 10090 |
| Ccr8 | mCCR8 | ANA501 | 10090 |
| Ccr9 | mCCR9 | ANA502 | 10090 |
| Cd101 | mCD101 | ANA942 | 10090 |
| Cd109 | mCD109 | ANA1207 | 10090 |
| Cd110 | mMPL | ANA650 | 10090 |
| Cd111 | mNECTIN1 | ANA1237 | 10090 |
| Cd112 | mNECTIN2 | ANA1093 | 10090 |
| Cd113 | mNECTIN3 | ANA1238 | 10090 |
| Cd114 | mCSF3R | ANA520 | 10090 |
| Cd116 | mCSF2RA | ANA517 | 10090 |
| Cd11a | mITGAL | ANA1074 | 10090 |
| Cd127 | mIL7R | ANA636 | 10090 |
| Cd14 | mCD14 | ANA1006 | 10090 |
| Cd151 | mCD151 | ANA953 | 10090 |
| Cd160 | mCD160 | ANA970 | 10090 |
| Cd163 | mCD163 | ANA1164 | 10090 |
| Cd164 | mCD164 | ANA1250 | 10090 |
| Cd164l2 | mCD164L2 | ANA1229 | 10090 |
| Cd177 | mCd177 | ANA1206 | 10090 |
| Cd180 | mCD180 | ANA1176 | 10090 |
| Cd19 | mCD19 | ANA1078 | 10090 |
| Cd1d1 | mCD1D | ANA1011 | 10090 |
| Cd1d2 | mCd1d2 | ANA1012 | 10090 |
| Cd2 | mCD2 | ANA1000 | 10090 |
| Cd200 | mCD200 | ANA956 | 10090 |
| Cd200r1 | mCd200r1 | ANA1232 | 10090 |
| Cd200r2 | mCD200R1L | ANA1187 | 10090 |
| Cd200r3 | mCd200r3 | ANA1168 | 10090 |
| Cd200r4 | mCd200r4 | ANA1186 | 10090 |
| Cd207 | mCD207 | ANA1208 | 10090 |
| Cd209a | mCd209a | ANA1216 | 10090 |
| Cd209b | mCd209b | ANA1194 | 10090 |
| Cd209c | mCd209c | ANA1215 | 10090 |
| Cd209d | mCd209d | ANA1214 | 10090 |
| Cd209e | mCd209e | ANA1213 | 10090 |
| Cd22 | mCD22 | ANA1097 | 10090 |
| Cd226 | mCD226 | ANA1198 | 10090 |
| Cd244a | mCD244 | ANA1143 | 10090 |
| Cd247 | mCD247 | ANA1076 | 10090 |
| Cd248 | mCD248 | ANA1212 | 10090 |
| Cd24a | mCD24 | ANA1077 | 10090 |
| Cd27 | mCD27 | ANA503 | 10090 |
| Cd274 | mCD274 | ANA1231 | 10090 |
| Cd276 | mCD276 | ANA1210 | 10090 |
| Cd28 | mCD28 | ANA1086 | 10090 |
| Cd2ap | mCD2AP | ANA1239 | 10090 |
| Cd2bp2 | mCD2BP2 | ANA1228 | 10090 |
| Cd300a | mCD300A | ANA1183 | 10090 |
| Cd300c | mCD300C | ANA940 | 10090 |
| Cd300c2 | mClm | ANA1190 | 10090 |
| Cd300e | mCD300E | ANA1197 | 10090 |
| Cd300lb | mCD300LB | ANA1166 | 10090 |
| Cd300ld | mClm5 | ANA1209 | 10090 |
| Cd300ld3 | mClm3 | ANA1184 | 10090 |
| Cd300lf | mCD300LF | ANA1185 | 10090 |
| Cd300lg | mCd300lg | ANA1163 | 10090 |
| Cd302 | mCD302 | ANA1230 | 10090 |
| Cd320 | mCD320 | ANA1266 | 10090 |
| Cd33 | mCD33 | ANA1177 | 10090 |
| Cd34 | mCD34 | ANA1178 | 10090 |
| Cd36 | mCD36 | ANA1148 | 10090 |
| Cd37 | mCD37 | ANA1172 | 10090 |
| Cd38 | mCD38 | ANA1125 | 10090 |
| Cd3d | mCD3D | ANA980 | 10090 |
| Cd3e | mCD3E | ANA1071 | 10090 |
| Cd3eap | mCD3EAP | ANA1189 | 10090 |
| Cd3g | mCD3G | ANA1016 | 10090 |
| Cd4 | mCD4 | ANA504 | 10090 |
| Cd40 | mCD40 | ANA505 | 10090 |
| Cd40lg | mCD40LG | ANA506 | 10090 |
| Cd44 | mCD44 | ANA1035 | 10090 |
| Cd46 | mCD46 | ANA968 | 10090 |
| Cd47 | mCD47 | ANA1175 | 10090 |
| Cd48 | mCD48 | ANA1052 | 10090 |
| Cd5 | mCD5 | ANA1023 | 10090 |
| Cd52 | mCD52 | ANA1179 | 10090 |
| Cd53 | mCD53 | ANA1171 | 10090 |
| Cd55 | mCd55 | ANA1173 | 10090 |
| Cd55b | mCd55b | ANA1174 | 10090 |
| Cd59a | mCd59a | ANA957 | 10090 |
| Cd59b | mCd59b | ANA1127 | 10090 |
| Cd5l | mCD5L | ANA1249 | 10090 |
| Cd6 | mCD6 | ANA1170 | 10090 |
| Cd63 | mCD63 | ANA1112 | 10090 |
| Cd68 | mCD68 | ANA1090 | 10090 |
| Cd69 | mCD69 | ANA1102 | 10090 |
| Cd7 | mCD7 | ANA1121 | 10090 |
| Cd70 | mCD70 | ANA507 | 10090 |
| Cd72 | mCD72 | ANA1067 | 10090 |
| Cd74 | mCD74 | ANA981 | 10090 |
| Cd79a | mCD79A | ANA1014 | 10090 |
| Cd79b | mCD79B | ANA1037 | 10090 |
| Cd80 | mCD80 | ANA1135 | 10090 |
| Cd81 | mCD81 | ANA1099 | 10090 |
| Cd82 | mCD82 | ANA1107 | 10090 |
| Cd83 | mCD83 | ANA969 | 10090 |
| Cd84 | mCD84 | ANA1162 | 10090 |
| Cd86 | mCD86 | ANA1114 | 10090 |
| Cd8a | mCD8A | ANA974 | 10090 |
| Cd8b1 | mCD8B | ANA1004 | 10090 |
| Cd9 | mCD9 | ANA1108 | 10090 |
| Cd93 | mCD93 | ANA971 | 10090 |
| Cd96 | mCD96 | ANA1165 | 10090 |
| Cd99l2 | mCD99L2 | ANA1193 | 10090 |
| Cklf | mCKLF | ANA508 | 10090 |
| Clcf1 | mCLCF1 | ANA509 | 10090 |
| Cmtm1 | CMTM1 | ANA510 | 10090 |
| Cmtm6 | mCMTM6 | ANA511 | 10090 |
| Cmtm7 | mCMTM7 | ANA512 | 10090 |
| Cntfr | mCNTFR | ANA513 | 10090 |
| Csf1 | mCSF1 | ANA514 | 10090 |
| Csf1r | mCSF1R | ANA515 | 10090 |
| Csf2 | mCSF2 | ANA516 | 10090 |
| Csf2ra | mCSF2RA | ANA517 | 10090 |
| Csf2rb | mCsf2rb | ANA518 | 10090 |
| Csf3 | mCSF3 | ANA519 | 10090 |
| Csf3r | mCSF3R | ANA520 | 10090 |
| Cx3cl1 | mCX3CL1 | ANA521 | 10090 |
| Cx3cr1 | mCX3CR1 | ANA522 | 10090 |
| Cxcl1 | mCXCL1 | ANA523 | 10090 |
| Cxcl10 | mCXCL10 | ANA524 | 10090 |
| Cxcl11 | mCxcl11 | ANA525 | 10090 |
| Cxcl12 | mCXCL12 | ANA526 | 10090 |
| Cxcl13 | mCXCL13 | ANA527 | 10090 |
| Cxcl14 | mCXCL14 | ANA528 | 10090 |
| Cxcl16 | mCXCL16 | ANA529 | 10090 |
| Cxcl17 | mCXCL17 | ANA530 | 10090 |
| Cxcl2 | mCxcl2 | ANA531 | 10090 |
| Cxcl3 | mCxcl3 | ANA532 | 10090 |
| Cxcl5 | mCXCL5 | ANA533 | 10090 |
| Cxcl9 | mCXCL9 | ANA534 | 10090 |
| Cxcr1 | mCxcr1 | ANA535 | 10090 |
| Cxcr2 | mCXCR2 | ANA536 | 10090 |
| Cxcr3 | mCXCR3 | ANA537 | 10090 |
| Cxcr4 | mCXCR4 | ANA538 | 10090 |
| Cxcr5 | mCXCR5 | ANA539 | 10090 |
| Cxcr6 | mCXCR6 | ANA540 | 10090 |
| DC-SIGN1 | hCD209 | ANA869 | 9606 |
| DDR1 | hDDR1 | ANA1145 | 9606 |
| DPP4 | hDPP4 | ANA1081 | 9606 |
| DR | hHLA-DRA | ANA812 | 9606 |
| E-Selectin | hSELL | ANA712 | 9606 |
| EBI3 | hEBI3 | ANA80 | 9606 |
| EGF | hEGF | ANA81 | 9606 |
| EGFR | hEGFR | ANA82 | 9606 |
| ENA78 | hCXCL5 | ANA70 | 9606 |
| ENG | hENG | ANA1050 | 9606 |
| ENPEP | hENPEP | ANA1142 | 9606 |
| ENPP3 | hENPP3 | ANA947 | 9606 |
| EOTAXIN | hCCL11 | ANA3 | 9606 |
| EPCAM | hEPCAM | ANA1045 | 9606 |
| EPO | hEPO | ANA83 | 9606 |
| EPOR | hEPOR | ANA84 | 9606 |
| ERBB2 | hERBB2 | ANA982 | 9606 |
| Ebi3 | mEBI3 | ANA541 | 10090 |
| Ecotanin_3 | hCCL11 | ANA3 | 9606 |
| Egf | mEGF | ANA542 | 10090 |
| Egfr | mEGFR | ANA543 | 10090 |
| Eotaxin | hCCL11 | ANA3 | 9606 |
| Epo | mEPO | ANA544 | 10090 |
| Epor | mEPOR | ANA545 | 10090 |
| Exotaxin | hCCL11 | ANA3 | 9606 |
| F11R | hF11R | ANA1265 | 9606 |
| F3 | hF3 | ANA1028 | 9606 |
| FAS | hFAS | ANA85 | 9606 |
| FASL | hFASLG | ANA86 | 9606 |
| FASLG | hFASLG | ANA86 | 9606 |
| FCAR | hFCAR | ANA1075 | 9606 |
| FCG3A | hFCGR3A | ANA811 | 9606 |
| FCGR1A | hFCGR1A | ANA873 | 9606 |
| FCGR2A | hFCGR2A | ANA1018 | 9606 |
| FCGR2B | hFCGR2B | ANA1088 | 9606 |
| FCGR2C | hFCGR2C | ANA1089 | 9606 |
| FCGR3B | hFCGR3B | ANA960 | 9606 |
| FGF basic | hFGF2 | ANA88 | 9606 |
| FGF-2 | hFGF2 | ANA88 | 9606 |
| FGF1 | hFGF1 | ANA87 | 9606 |
| FGF2 | hFGF2 | ANA88 | 9606 |
| FGFB | hFGF2 | ANA88 | 9606 |
| FGFBasic | hFGF2 | ANA88 | 9606 |
| FGFR1 | hFGFR1 | ANA1009 | 9606 |
| FGFR2 | hFGFR2 | ANA1065 | 9606 |
| FGFR3 | hFGFR3 | ANA1070 | 9606 |
| FGFR4 | hFGFR4 | ANA1069 | 9606 |
| FGFb | hFGF2 | ANA88 | 9606 |
| FIGF | hVEGFD | ANA710 | 9606 |
| FLT 3 LIGAND | hFLT3LG | ANA90 | 9606 |
| FLT3 | hFLT3 | ANA89 | 9606 |
| FLT3LG | hFLT3LG | ANA90 | 9606 |
| FOXP3 | hFOXP3 | ANA874 | 9606 |
| FRACTALKINE | hCX3CL1 | ANA58 | 9606 |
| FUT3 | hFUT3 | ANA1061 | 9606 |
| FUT4 | hFUT4 | ANA875 | 9606 |
| FZD10 | hFZD10 | ANA1257 | 9606 |
| FZD4 | hFZD4 | ANA1256 | 9606 |
| FZD9 | hFZD9 | ANA943 | 9606 |
| Fas | mFAS | ANA546 | 10090 |
| Fasl | mFASLG | ANA547 | 10090 |
| Fgf1 | mFGF1 | ANA548 | 10090 |
| Fgf2 | mFGF2 | ANA549 | 10090 |
| Fgfb | mFGF2 | ANA549 | 10090 |
| Flt3 | mFLT3 | ANA550 | 10090 |
| Flt3l | mFLT3LG | ANA551 | 10090 |
| FoxP3 | hFOXP3 | ANA874 | 9606 |
| Fractalkine | mCX3CL1 | ANA521 | 10090 |
| G-CSF | hCSF3 | ANA56 | 9606 |
| GCSF | hCSF3 | ANA56 | 9606 |
| GDF15 | hGDF15 | ANA91 | 9606 |
| GGT1 | hGGT1 | ANA1058 | 9606 |
| GM-CSF | hCSF2 | ANA53 | 9606 |
| GMCSF | hCSF2 | ANA53 | 9606 |
| GM_CSF | hCSF2 | ANA53 | 9606 |
| GP1BA | hGP1BA | ANA992 | 9606 |
| GP1BB | hGP1BB | ANA1022 | 9606 |
| GP5 | hGP5 | ANA1103 | 9606 |
| GP9 | hGP9 | ANA1032 | 9606 |
| GPR15 | hGPR15 | ANA896 | 9606 |
| GRO | hCXCL1 | ANA60 | 9606 |
| GRO ALPHA | hCXCL1 | ANA60 | 9606 |
| GROA | hCXCL1 | ANA60 | 9606 |
| GYPA | hGYPA | ANA976 | 9606 |
| GYPB | hGYPB | ANA987 | 9606 |
| GYPC | hGYPC | ANA983 | 9606 |
| GZMB | hGZMB | ANA897 | 9606 |
| Gdf15 | mGDF15 | ANA552 | 10090 |
| GranB | hGZMB | ANA897 | 9606 |
| GranzymeB | hGZMB | ANA897 | 9606 |
| GzB | hGZMB | ANA897 | 9606 |
| HGF | hHGF | ANA92 | 9606 |
| HLA DR | hHLA-DRA | ANA812 | 9606 |
| HLA DR Alexa700-A | hHLA-DRA | ANA812 | 9606 |
| HLA-A | hHLA-A | ANA938 | 9606 |
| HLA-A2 | hHLA-A*2 | ANA975 | 9606 |
| HLA-Bw4 | hKIR3DL1 | ANA882 | 9606 |
| HLA-C | hHLA-C | ANA939 | 9606 |
| HLA-DR | hHLA-DRA | ANA812 | 9606 |
| HLA-DR 407E-A | hHLA-DRA | ANA812 | 9606 |
| HLA-DR+(?) | hHLA-DRA | ANA812 | 9606 |
| HLA-DRA | hHLA-DRA | ANA812 | 9606 |
| HLA-Dr | hHLA-DRA | ANA812 | 9606 |
| HLA-E | hHLA-E | ANA1029 | 9606 |
| HLA-G | hHLA-G | ANA1049 | 9606 |
| HLADR | hHLA-DRA | ANA812 | 9606 |
| HLADR(Lu175)Dd | hHLA-DRA | ANA812 | 9606 |
| HMMR | hHMMR | ANA966 | 9606 |
| Hgf | mHGF | ANA553 | 10090 |
| Hu Eotaxin (43) | hCCL11 | ANA3 | 9606 |
| Hu FGF basic (44) | hFGF2 | ANA88 | 9606 |
| Hu G-CSF (57) | hCSF3 | ANA56 | 9606 |
| Hu GM-CSF (34) | hCSF2 | ANA53 | 9606 |
| Hu IFN-g (21) | hIFNG | ANA110 | 9606 |
| Hu IL-10 (56) | hCXCL10 | ANA61 | 9606 |
| Hu IL-12(p70) (75) | hIL12 | ANA800 | 9606 |
| Hu IL-13 (51) | hIL13 | ANA127 | 9606 |
| Hu IL-15 (73) | hIL15 | ANA130 | 9606 |
| Hu IL-17 (76) | hIL17F-17A | ANA801 | 9606 |
| Hu IL-1b (39) | hIL1B | ANA143 | 9606 |
| Hu IL-1ra (25) | hIL1R1 | ANA145 | 9606 |
| Hu IL-2 (38) | hIL2 | ANA148 | 9606 |
| Hu IL-4 (52) | hIL4 | ANA174 | 9606 |
| Hu IL-5 (33) | hIL5 | ANA176 | 9606 |
| Hu IL-6 (19) | hIL6 | ANA178 | 9606 |
| Hu IL-7 (74) | hIL7 | ANA181 | 9606 |
| Hu IL-8 (54) | hCXCL8 | ANA72 | 9606 |
| Hu IL-9 (77) | hIL9 | ANA183 | 9606 |
| Hu IP-10 (48) | hCXCL10 | ANA61 | 9606 |
| Hu MCP-1(MCAF) (53) | hCCL2 | ANA11 | 9606 |
| Hu MIP-1a (55) | hCCL3 | ANA20 | 9606 |
| Hu MIP-1b (18) | hCCL4 | ANA24 | 9606 |
| Hu PDGF-bb (47) | hPDGFB | ANA202 | 9606 |
| Hu RANTES (37) | hCCL5 | ANA27 | 9606 |
| Hu TNF-a (36) | hTNF | ANA220 | 9606 |
| Hu VEGF (45) | VEGFA | ANA709 | 9606 |
| Human CCL17 (TARC) | hCCL17 | ANA8 | 9606 |
| Human CCL27 (CTACK) | hCCL27 | ANA19 | 9606 |
| Human CXCL10 (IP-10) | hCXCL10 | ANA61 | 9606 |
| ICAM-1 | ICAM1 | ANA705 | 9606 |
| ICAM1 | ICAM1 | ANA705 | 9606 |
| ICAM2 | hICAM2 | ANA1025 | 9606 |
| ICAM3 | hICAM3 | ANA1094 | 9606 |
| ICAM4 | hICAM4 | ANA1155 | 9606 |
| ICOS | hICOS | ANA898 | 9606 |
| ICOSLG | hICOSLG | ANA964 | 9606 |
| IFITM1 | hIFITM1 | ANA1021 | 9606 |
| IFN G | hIFNG | ANA110 | 9606 |
| IFN alpha | fam:hIFNA | ANA717 | 9606 |
| IFN gamma | hIFNG | ANA110 | 9606 |
| IFN-G | hIFNG | ANA110 | 9606 |
| IFN-a | fam:hIFNA | ANA717 | 9606 |
| IFN-alpha | fam:hIFNA | ANA717 | 9606 |
| IFN-alpha2 | hIFNA2 | ANA99 | 9606 |
| IFN-b | hIFNB1 | ANA108 | 9606 |
| IFN-g | hIFNG | ANA110 | 9606 |
| IFN-g APC Cy7-A | hIFNG | ANA110 | 9606 |
| IFN-gamma | hIFNG | ANA110 | 9606 |
| IFN-r | hTNFRSF18 | ANA230 | 9606 |
| IFN1@ | fam:hIFNA | ANA717 | 9606 |
| IFNA | fam:hIFNA | ANA717 | 9606 |
| IFNA1 | Ifna1 | ANA93 | 9606 |
| IFNA10 | IFNA10 | ANA555 | 10090 |
| IFNA13 | Ifna13 | ANA95 | 9606 |
| IFNA14 | IFNA14 | ANA557 | 10090 |
| IFNA16 | IFNA16 | ANA558 | 10090 |
| IFNA17 | hIFNA17 | ANA98 | 9606 |
| IFNA2 | hIFNA2 | ANA99 | 9606 |
| IFNA21 | hIFNA21 | ANA100 | 9606 |
| IFNA4 | hIFNA4 | ANA101 | 9606 |
| IFNA5 | hIFNA5 | ANA102 | 9606 |
| IFNA6 | hIFNA6 | ANA103 | 9606 |
| IFNA7 | hIFNA7 | ANA104 | 9606 |
| IFNA8 | hIFNA8 | ANA105 | 9606 |
| IFNAR1 | hIFNAR1 | ANA106 | 9606 |
| IFNAR2 | hIFNAR2 | ANA107 | 9606 |
| IFNB | hIFNB1 | ANA108 | 9606 |
| IFNB1 | hIFNB1 | ANA108 | 9606 |
| IFNE | hIFNE | ANA109 | 9606 |
| IFNG | hIFNG | ANA110 | 9606 |
| IFNGR1 | hIFNGR1 | ANA111 | 9606 |
| IFNGR2 | hIFNGR2 | ANA112 | 9606 |
| IFNK | hIFNK | ANA113 | 9606 |
| IFNL1 | hIFNL1 | ANA114 | 9606 |
| IFNL2 | hIFNL2 | ANA115 | 9606 |
| IFNL3 | hIFNL3 | ANA116 | 9606 |
| IFNLR1 | hIFNLR1 | ANA117 | 9606 |
| IFNa | fam:hIFNA | ANA717 | 9606 |
| IFNa2 | hIFNA2 | ANA99 | 9606 |
| IFNa2b | hIFNA2 | ANA99 | 9606 |
| IFNb | hIFNB1 | ANA108 | 9606 |
| IFNg | hIFNG | ANA110 | 9606 |
| IFNgamma | hIFNG | ANA110 | 9606 |
| IGF-1 | IGF1 | ANA713 | 9606 |
| IGF1 | IGF1 | ANA713 | 9606 |
| IGF1R | hIGF1R | ANA993 | 9606 |
| IGF2R | hIGF2R | ANA1013 | 9606 |
| IGFBP-3 | IGFBP3 | ANA706 | 9606 |
| IGFBP3 | IGFBP3 | ANA706 | 9606 |
| IGHA1 | hIGHA1 | ANA820 | 9606 |
| IGHA2 | hIGHA2 | ANA819 | 9606 |
| IGHD | hIGHD | ANA813 | 9606 |
| IGHM | hIGHM | ANA817 | 9606 |
| IGLL1 | hIGLL1 | ANA1040 | 9606 |
| IGSF8 | hIGSF8 | ANA1221 | 9606 |
| IL-10 | hIL10 | ANA118 | 9606 |
| IL-12 p70 | hIL12 | ANA800 | 9606 |
| IL-12(p40) | hIL12B | ANA124 | 9606 |
| IL-12(p70) | hIL12 | ANA800 | 9606 |
| IL-12-P70 | hIL12 | ANA800 | 9606 |
| IL-12P40 | hIL12B | ANA124 | 9606 |
| IL-12p40 | hIL12B | ANA124 | 9606 |
| IL-12p70 | hIL12 | ANA800 | 9606 |
| IL-13 | hIL13 | ANA127 | 9606 |
| IL-15 | hIL15 | ANA130 | 9606 |
| IL-17 | hIL17F-17A | ANA801 | 9606 |
| IL-17A | hIL17A | ANA133 | 9606 |
| IL-17F | hIL17F | ANA137 | 9606 |
| IL-18 | hIL18 | ANA139 | 9606 |
| IL-1B | hIL1B | ANA143 | 9606 |
| IL-1RA | hIL1R1 | ANA145 | 9606 |
| IL-1Ra | hIL1R1 | ANA145 | 9606 |
| IL-1a | hIL1A | ANA142 | 9606 |
| IL-1alpha | hIL1A | ANA142 | 9606 |
| IL-1b | hIL1B | ANA143 | 9606 |
| IL-1beta | hIL1B | ANA143 | 9606 |
| IL-1ra | hIL1R1 | ANA145 | 9606 |
| IL-2 | hIL2 | ANA148 | 9606 |
| IL-2 FITC-A | hIL2 | ANA148 | 9606 |
| IL-21 | hIL21 | ANA152 | 9606 |
| IL-23 | hIL23A | ANA157 | 9606 |
| IL-28A | hIFNL2 | ANA115 | 9606 |
| IL-3 | hIL3 | ANA166 | 9606 |
| IL-4 | hIL4 | ANA174 | 9606 |
| IL-5 | hIL5 | ANA176 | 9606 |
| IL-6 | hIL6 | ANA178 | 9606 |
| IL-7 | hIL7 | ANA181 | 9606 |
| IL-8 | hCXCL8 | ANA72 | 9606 |
| IL-9 | hIL9 | ANA183 | 9606 |
| IL1 alpha | hIL1A | ANA142 | 9606 |
| IL1 beta | hIL1B | ANA143 | 9606 |
| IL1-A | hIL1A | ANA142 | 9606 |
| IL1-B | hIL1B | ANA143 | 9606 |
| IL10 | hIL10 | ANA118 | 9606 |
| IL10RA | hIL10RA | ANA119 | 9606 |
| IL10RB | hIL10RB | ANA120 | 9606 |
| IL11 | hIL11 | ANA121 | 9606 |
| IL11RA | hIL11RA | ANA122 | 9606 |
| IL12 | hIL12 | ANA800 | 9606 |
| IL12 P40 | hIL12B | ANA124 | 9606 |
| IL12 P70 | hIL12 | ANA800 | 9606 |
| IL12A | hIL12A | ANA123 | 9606 |
| IL12B | hIL12B | ANA124 | 9606 |
| IL12P40 | hIL12B | ANA124 | 9606 |
| IL12P70 | hIL12 | ANA800 | 9606 |
| IL12RB1 | hIL12RB1 | ANA125 | 9606 |
| IL12RB2 | hIL12RB2 | ANA126 | 9606 |
| IL12p35 | hIL12A | ANA123 | 9606 |
| IL12p40 | hIL12B | ANA124 | 9606 |
| IL12p70 | hIL12 | ANA800 | 9606 |
| IL13 | hIL13 | ANA127 | 9606 |
| IL13RA1 | hIL13RA1 | ANA128 | 9606 |
| IL13RA2 | hIL13RA2 | ANA129 | 9606 |
| IL15 | hIL15 | ANA130 | 9606 |
| IL15RA | hIL15RA | ANA131 | 9606 |
| IL16 | hIL16 | ANA132 | 9606 |
| IL17 | hIL17F-17A | ANA801 | 9606 |
| IL17A | hIL17A | ANA133 | 9606 |
| IL17B | hIL17B | ANA134 | 9606 |
| IL17C | hIL17C | ANA135 | 9606 |
| IL17D | hIL17D | ANA136 | 9606 |
| IL17F | hIL17F | ANA137 | 9606 |
| IL17RA | hIL17RA | ANA138 | 9606 |
| IL17a | hIL17A | ANA133 | 9606 |
| IL18 | hIL18 | ANA139 | 9606 |
| IL18R1 | hIL18R1 | ANA140 | 9606 |
| IL18RAP | hIL18RAP | ANA972 | 9606 |
| IL19 | hIL19 | ANA141 | 9606 |
| IL1A | hIL1A | ANA142 | 9606 |
| IL1B | hIL1B | ANA143 | 9606 |
| IL1F10 | hIL1F10 | ANA144 | 9606 |
| IL1R1 | hIL1R1 | ANA145 | 9606 |
| IL1R2 | hIL1R2 | ANA146 | 9606 |
| IL1RA | hIL1R1 | ANA145 | 9606 |
| IL1RN | hIL1RN | ANA147 | 9606 |
| IL1a | hIL1A | ANA142 | 9606 |
| IL1b | hIL1B | ANA143 | 9606 |
| IL2 | hIL2 | ANA148 | 9606 |
| IL20 | hIL20 | ANA149 | 9606 |
| IL20RA | hIL20RA | ANA150 | 9606 |
| IL20RB | hIL20RB | ANA151 | 9606 |
| IL21 | hIL21 | ANA152 | 9606 |
| IL21R | hIL21R | ANA153 | 9606 |
| IL22 | hIL22 | ANA154 | 9606 |
| IL22RA1 | hIL22RA1 | ANA155 | 9606 |
| IL22RA2 | hIL22RA2 | ANA156 | 9606 |
| IL23 | hIL23 | ANA802 | 9606 |
| IL23A | hIL23A | ANA157 | 9606 |
| IL23R | hIL23R | ANA158 | 9606 |
| IL23r | hIL23R | ANA158 | 9606 |
| IL24 | hIL24 | ANA159 | 9606 |
| IL25 | hIL25 | ANA160 | 9606 |
| IL26 | hIL26 | ANA161 | 9606 |
| IL27 | hIL27 | ANA162 | 9606 |
| IL28A | hIFNL2 | ANA115 | 9606 |
| IL2RA | hIL2RA | ANA163 | 9606 |
| IL2RB | hIL2RB | ANA164 | 9606 |
| IL2RG | hIL2RG | ANA165 | 9606 |
| IL2r | hIL2RA | ANA163 | 9606 |
| IL3 | hIL3 | ANA166 | 9606 |
| IL31 | hIL31 | ANA167 | 9606 |
| IL32 | hIL32 | ANA168 | 9606 |
| IL33 | hIL33 | ANA169 | 9606 |
| IL34 | hIL34 | ANA170 | 9606 |
| IL36G | hIL36G | ANA171 | 9606 |
| IL36RN | hIL36RN | ANA172 | 9606 |
| IL3RA | hIL3RA | ANA173 | 9606 |
| IL4 | hIL4 | ANA174 | 9606 |
| IL4R | hIL4R | ANA175 | 9606 |
| IL5 | hIL5 | ANA176 | 9606 |
| IL5RA | hIL5RA | ANA177 | 9606 |
| IL6 | hIL6 | ANA178 | 9606 |
| IL6R | hIL6R | ANA179 | 9606 |
| IL6ST | hIL6ST | ANA180 | 9606 |
| IL7 | hIL7 | ANA181 | 9606 |
| IL7R | hIL7R | ANA182 | 9606 |
| IL8 | hCXCL8 | ANA72 | 9606 |
| IL9 | hIL9 | ANA183 | 9606 |
| IL9R | hIL9R | ANA184 | 9606 |
| IL_10 | hIL10 | ANA118 | 9606 |
| IL_12p70 | hIL12 | ANA800 | 9606 |
| IL_13 | hIL13 | ANA127 | 9606 |
| IL_1B | hIL1B | ANA143 | 9606 |
| IL_1a | hIL1A | ANA142 | 9606 |
| IL_2 | hIL2 | ANA148 | 9606 |
| IL_4 | hIL4 | ANA174 | 9606 |
| IL_5 | hIL5 | ANA176 | 9606 |
| IL_6 | hIL6 | ANA178 | 9606 |
| IL_7 | hIL7 | ANA181 | 9606 |
| IL_8 | hCXCL8 | ANA72 | 9606 |
| INF-gamma | hIFNG | ANA110 | 9606 |
| INSR | hINSR | ANA989 | 9606 |
| IP-10 | mCXCL10 | ANA524 | 10090 |
| IP10 | hCXCL10 | ANA61 | 9606 |
| IP_10 | hCXCL10 | ANA61 | 9606 |
| ITAX | hITGAX | ANA814 | 9606 |
| ITGA2 | hITGA2 | ANA1048 | 9606 |
| ITGA2B | hITGA2B | ANA997 | 9606 |
| ITGA3 | hITGA3 | ANA1079 | 9606 |
| ITGA4 | hITGA4 | ANA1026 | 9606 |
| ITGA5 | hITGA5 | ANA999 | 9606 |
| ITGA6 | hITGA6 | ANA876 | 9606 |
| ITGAD | hITGAD | ANA1153 | 9606 |
| ITGAE | hITGAE | ANA877 | 9606 |
| ITGAL | hITGAL | ANA1059 | 9606 |
| ITGAM | hITGAM | ANA878 | 9606 |
| ITGAV | hITGAV | ANA991 | 9606 |
| ITGB1 | hITGB1 | ANA986 | 9606 |
| ITGB2 | hITGB2 | ANA985 | 9606 |
| ITGB3 | hITGB3 | ANA984 | 9606 |
| ITGB4 | hITGB4 | ANA1043 | 9606 |
| Ifna1 | mIfna1 | ANA554 | 10090 |
| Ifna10 | IFNA10 | ANA555 | 10090 |
| Ifna13 | mIfna13 | ANA556 | 10090 |
| Ifna14 | IFNA14 | ANA557 | 10090 |
| Ifna16 | IFNA16 | ANA558 | 10090 |
| Ifna2 | mIfna2 | ANA559 | 10090 |
| Ifna4 | mIfna4 | ANA560 | 10090 |
| Ifna5 | mIfna5 | ANA561 | 10090 |
| Ifna6 | mIfna6 | ANA562 | 10090 |
| Ifna7 | mIfna7 | ANA563 | 10090 |
| Ifna8 | mIfna6 | ANA562 | 10090 |
| Ifnar1 | mIFNAR1 | ANA565 | 10090 |
| Ifnar2 | mIFNAR2 | ANA566 | 10090 |
| Ifnb1 | mIFNB1 | ANA567 | 10090 |
| Ifne | mIFNE | ANA568 | 10090 |
| Ifng | mIFNG | ANA569 | 10090 |
| Ifngr1 | mIFNGR1 | ANA570 | 10090 |
| Ifngr2 | IFNGR2 | ANA571 | 10090 |
| Ifnk | mIFNK | ANA572 | 10090 |
| Ifnl2 | mIfnl2 | ANA573 | 10090 |
| Ifnl3 | mIfnl3 | ANA574 | 10090 |
| Ifnlr1 | mIFNLR1 | ANA575 | 10090 |
| IgA1 | hIGHA1 | ANA820 | 9606 |
| IgA2 | hIGHA2 | ANA819 | 9606 |
| IgA_inhouse | hIGHA1 | ANA820 | 9606 |
| IgD | hIGHD | ANA813 | 9606 |
| IgD(Nd146)Dd | hIGHD | ANA813 | 9606 |
| IgM | hIGHM | ANA817 | 9606 |
| Il10 | mIL10 | ANA576 | 10090 |
| Il10ra | mIL10RA | ANA577 | 10090 |
| Il10rb | mIL10RB | ANA578 | 10090 |
| Il11 | mIL11 | ANA579 | 10090 |
| Il11ra1 | mIl11ra1 | ANA580 | 10090 |
| Il12a | mIL12A | ANA581 | 10090 |
| Il12b | mIL12B | ANA582 | 10090 |
| Il12p35 | mIL12A | ANA581 | 10090 |
| Il12rb1 | mIL12RB1 | ANA583 | 10090 |
| Il12rb2 | mIL12RB2 | ANA584 | 10090 |
| Il13 | mIL13 | ANA585 | 10090 |
| Il13ra1 | mIL13RA1 | ANA586 | 10090 |
| Il13ra2 | mIL13RA2 | ANA587 | 10090 |
| Il15 | mIL15 | ANA588 | 10090 |
| Il15ra | mIL15RA | ANA589 | 10090 |
| Il16 | mIL16 | ANA590 | 10090 |
| Il17a | mIL17A | ANA591 | 10090 |
| Il17b | mIL17B | ANA592 | 10090 |
| Il17c | mIL17C | ANA593 | 10090 |
| Il17d | IL17D | ANA594 | 10090 |
| Il17f | mIL17F | ANA595 | 10090 |
| Il17ra | mIL17RA | ANA596 | 10090 |
| Il18 | mIL18 | ANA597 | 10090 |
| Il19 | mIL19 | ANA598 | 10090 |
| Il1a | mIL1A | ANA599 | 10090 |
| Il1b | mIL1B | ANA600 | 10090 |
| Il1f10 | mIL1F10 | ANA601 | 10090 |
| Il1f5 | mIL36RN | ANA602 | 10090 |
| Il1r1 | mIL1R1 | ANA603 | 10090 |
| Il1r2 | mIL1R2 | ANA604 | 10090 |
| Il1rn | mIL1RN | ANA605 | 10090 |
| Il2 | mIL2 | ANA606 | 10090 |
| Il20 | mIL20 | ANA607 | 10090 |
| Il20ra | mIL20RA | ANA608 | 10090 |
| Il20rb | IL20RB | ANA609 | 10090 |
| Il21 | mIL21 | ANA610 | 10090 |
| Il21r | mIL21R | ANA611 | 10090 |
| Il22 | mIl22 | ANA612 | 10090 |
| Il22ra1 | mIL22RA1 | ANA613 | 10090 |
| Il22ra2 | mIL22RA2 | ANA614 | 10090 |
| Il23a | mIL23A | ANA615 | 10090 |
| Il23r | mIL23R | ANA616 | 10090 |
| Il24 | mIL24 | ANA617 | 10090 |
| Il25 | mMYDGF | ANA618 | 10090 |
| Il27 | mIL27 | ANA619 | 10090 |
| Il2ra | mIL2RA | ANA620 | 10090 |
| Il2rb | mIL2RB | ANA621 | 10090 |
| Il2rg | mIL2RG | ANA622 | 10090 |
| Il3 | mIL3 | ANA623 | 10090 |
| Il31 | mIL31 | ANA624 | 10090 |
| Il33 | mIL33 | ANA625 | 10090 |
| Il34 | mIL34 | ANA626 | 10090 |
| Il3ra | mIL3RA | ANA627 | 10090 |
| Il4 | mIL4 | ANA628 | 10090 |
| Il4ra | mIL4R | ANA629 | 10090 |
| Il5 | mIL5 | ANA630 | 10090 |
| Il5ra | mIL5RA | ANA631 | 10090 |
| Il6 | mIL6 | ANA632 | 10090 |
| Il6ra | mIL6R | ANA633 | 10090 |
| Il6st | mIL6ST | ANA634 | 10090 |
| Il7 | mIL7 | ANA635 | 10090 |
| Il7r | mIL7R | ANA636 | 10090 |
| Il9 | mIL9 | ANA637 | 10090 |
| Il9r | mIL9R | ANA638 | 10090 |
| Itgal | mITGAL | ANA1074 | 10090 |
| JAG1 | hJAG1 | ANA1132 | 9606 |
| JAM2 | hJAM2 | ANA1126 | 9606 |
| K1-67 | hMKI67 | ANA889 | 9606 |
| KC | hCXCL1 | ANA60 | 9606 |
| KDR | hKDR | ANA1100 | 9606 |
| KEL | hKEL | ANA1073 | 9606 |
| KI67 | hMKI67 | ANA889 | 9606 |
| KIR2DL1 | hKIR2DL1 | ANA879 | 9606 |
| KIR2DL2 | hKIR2DL2 | ANA880 | 9606 |
| KIR2DL3 | hKIR2DL3 | ANA881 | 9606 |
| KIR2DL4 | hKIR2DL4 | ANA1224 | 9606 |
| KIR2DL5A | hKIR2DL5A | ANA1199 | 9606 |
| KIR2DS1 | hKIR2DS1 | ANA1157 | 9606 |
| KIR2DS2 | hKIR2DS2 | ANA1117 | 9606 |
| KIR2DS4 | hKIR2DS4 | ANA1118 | 9606 |
| KIR2DS5 | hKIR2DS5 | ANA1156 | 9606 |
| KIR3DL1 | hKIR3DL1 | ANA882 | 9606 |
| KIR3DL2 | hKIR3DL2 | ANA1116 | 9606 |
| KIR3DL3 | hKIR3DL3 | ANA1204 | 9606 |
| KIT | hKIT | ANA185 | 9606 |
| KITLG | hKITLG | ANA186 | 9606 |
| KLRB1 | hKLRB1 | ANA883 | 9606 |
| KLRC1 | hKLRC1 | ANA861 | 9606 |
| KLRC2 | hKLRC2 | ANA1080 | 9606 |
| KLRD1 | hKLRD1 | ANA884 | 9606 |
| KLRK1 | hKLRK1 | ANA886 | 9606 |
| Ki-67 | hMKI67 | ANA889 | 9606 |
| Ki67 | hMKI67 | ANA889 | 9606 |
| Kir3dl1 | mKir3dl1 | ANA1134 | 10090 |
| Kit | mKIT | ANA639 | 10090 |
| Kitl | mKITLG | ANA640 | 10090 |
| L1CAM | hL1CAM | ANA1092 | 9606 |
| LAG3 | hLAG3 | ANA1054 | 9606 |
| LAIR1 | hLAIR1 | ANA1180 | 9606 |
| LAIR2 | hLAIR2 | ANA1181 | 9606 |
| LAMP1 | hLAMP1 | ANA887 | 9606 |
| LAMP2 | hLAMP2 | ANA1024 | 9606 |
| LAMP3 | hLAMP3 | ANA1261 | 9606 |
| LBT | hLTB | ANA187 | 9606 |
| LECT1 | hCNMD | ANA188 | 9606 |
| LECT2 | hLECT2 | ANA189 | 9606 |
| LEP | LEP | ANA714 | 9606 |
| LEP-R | hLEPR | ANA899 | 9606 |
| LEPR | hLEPR | ANA899 | 9606 |
| LEPTIN | LEP | ANA714 | 9606 |
| LIF | hLIF | ANA190 | 9606 |
| LIFR | hLIFR | ANA191 | 9606 |
| LILRA1 | hLILRA1 | ANA961 | 9606 |
| LILRA2 | hLILRA2 | ANA1200 | 9606 |
| LILRA3 | hLILRA3 | ANA1202 | 9606 |
| LILRA4 | hLILRA4 | ANA1128 | 9606 |
| LILRA5 | hLILRA5 | ANA941 | 9606 |
| LILRA6 | hLILRA6 | ANA1182 | 9606 |
| LILRB1 | hLILRB1 | ANA888 | 9606 |
| LILRB2 | hLILRB2 | ANA1201 | 9606 |
| LILRB3 | hLILRB3 | ANA962 | 9606 |
| LILRB4 | hLILRB4 | ANA1205 | 9606 |
| LILRB5 | hLILRB5 | ANA963 | 9606 |
| LRP1 | hLRP1 | ANA1144 | 9606 |
| LTA | hLTA | ANA192 | 9606 |
| LTBR | hLTBR | ANA193 | 9606 |
| LY75 | hLY75 | ANA937 | 9606 |
| LY9 | hLY9 | ANA1235 | 9606 |
| Lect1 | mCNMD | ANA641 | 10090 |
| Lect2 | mLECT2 | ANA642 | 10090 |
| Leptin | LEP | ANA714 | 9606 |
| Lif | mLIF | ANA643 | 10090 |
| Lifr | mLIFR | ANA644 | 10090 |
| Lta | mLTA | ANA645 | 10090 |
| Ltb | mLTB | ANA646 | 10090 |
| Ltbr | mLTBR | ANA647 | 10090 |
| M-CSF | hCSF1 | ANA51 | 9606 |
| MCAM | hMCAM | ANA1115 | 9606 |
| MCP-1 | hCCL2 | ANA11 | 9606 |
| MCP-1(MCAF) | hCCL2 | ANA11 | 9606 |
| MCP-3 | hCCL7 | ANA28 | 9606 |
| MCP1 | hCCL2 | ANA11 | 9606 |
| MCP3 | hCCL7 | ANA28 | 9606 |
| MCP4 | hCCL13 | ANA4 | 9606 |
| MCP_1 | hCCL2 | ANA11 | 9606 |
| MCP_4 | hCCL13 | ANA4 | 9606 |
| MCSF | hCSF1 | ANA51 | 9606 |
| MDC | hCCL22 | ANA14 | 9606 |
| MELTF | hMELTF | ANA998 | 9606 |
| MET | hMET | ANA194 | 9606 |
| MIF | hMIF | ANA195 | 9606 |
| MIG | hCXCL9 | ANA73 | 9606 |
| MIP-1B | hCCL4 | ANA24 | 9606 |
| MIP-1a | hCCL3 | ANA20 | 9606 |
| MIP-1alpha | hCCL3 | ANA20 | 9606 |
| MIP-1b | hCCL4 | ANA24 | 9606 |
| MIP-1b Alexa 647-A | hCCL4 | ANA24 | 9606 |
| MIP-1beta | hCCL4 | ANA24 | 9606 |
| MIP1A | hCCL3 | ANA20 | 9606 |
| MIP1B | hCCL4 | ANA24 | 9606 |
| MIP1a | hCCL3 | ANA20 | 9606 |
| MIP1b | hCCL4 | ANA24 | 9606 |
| MIP2 | hCXCL2 | ANA68 | 9606 |
| MIPB | hCCL4 | ANA24 | 9606 |
| MIP_1a | hCCL3 | ANA20 | 9606 |
| MIP_1b | hCCL4 | ANA24 | 9606 |
| MKI67 | hMKI67 | ANA889 | 9606 |
| MPL | hMPL | ANA196 | 9606 |
| MPO | MPO | ANA707 | 9606 |
| MRC1 | hMRC1 | ANA1072 | 9606 |
| MRC2 | hMRC2 | ANA1251 | 9606 |
| MSR1 | hMSR1 | ANA1064 | 9606 |
| MST1 | hMST1 | ANA197 | 9606 |
| MST1R | hMST1R | ANA198 | 9606 |
| MUC1 | hMUC1 | ANA1041 | 9606 |
| Met | mMET | ANA648 | 10090 |
| Mif | mMIF | ANA649 | 10090 |
| Mip1b | mCCL4 | ANA489 | 10090 |
| Mpl | mMPL | ANA650 | 10090 |
| Mst1 | mMST1 | ANA651 | 10090 |
| Mst1r | mMST1R | ANA652 | 10090 |
| NCAM1 | hNCAM1 | ANA815 | 9606 |
| NCR1 | hNCR1 | ANA967 | 9606 |
| NCR2 | hNCR2 | ANA885 | 9606 |
| NCR3 | hNCR3 | ANA950 | 9606 |
| NECTIN1 | hNECTIN1 | ANA1158 | 9606 |
| NECTIN2 | hNECTIN2 | ANA1217 | 9606 |
| NECTIN3 | hNECTIN3 | ANA1243 | 9606 |
| NGF | NGF | ANA699 | 9606 |
| NGFR | hNGFR | ANA994 | 9606 |
| NKG2A | hKLRC1 | ANA861 | 9606 |
| NKP44 | hNCR2 | ANA885 | 9606 |
| NKg2D | hKLRK1 | ANA886 | 9606 |
| NKp44 | hNCR2 | ANA885 | 9606 |
| NRP1 | hNRP1 | ANA949 | 9606 |
| NT5E | hNT5E | ANA1062 | 9606 |
| Nectin1 | mNECTIN1 | ANA1237 | 10090 |
| Nectin2 | mNECTIN2 | ANA1093 | 10090 |
| Nectin3 | mNECTIN3 | ANA1238 | 10090 |
| OPG | hTNFRSF11B | ANA226 | 9606 |
| OSM | hOSM | ANA199 | 9606 |
| OSMR | hOSMR | ANA200 | 9606 |
| Osm | mOSM | ANA653 | 10090 |
| Osmr | mOSMR | ANA654 | 10090 |
| PAI-1 | SERPINE1 | ANA708 | 9606 |
| PAI1 | SERPINE1 | ANA708 | 9606 |
| PAPP-A | PAPPA | ANA700 | 9606 |
| PAPPA | PAPPA | ANA700 | 9606 |
| PD-1 | hPDCD1 | ANA818 | 9606 |
| PD1 | hPDCD1 | ANA818 | 9606 |
| PDCD1 | hPDCD1 | ANA818 | 9606 |
| PDGF | hPDGF-AB | ANA803 | 9606 |
| PDGF AB/BB | hPDGF-AB | ANA803 | 9606 |
| PDGF-bb | hPDGFB | ANA202 | 9606 |
| PDGFA | hPDGFA | ANA201 | 9606 |
| PDGFAA | hPDGFA | ANA201 | 9606 |
| PDGFB | hPDGFB | ANA202 | 9606 |
| PDGFBB | hPDGFB | ANA202 | 9606 |
| PDGFRA | hPDGFRA | ANA203 | 9606 |
| PDGFRB | hPDGFRB | ANA204 | 9606 |
| PDL2 | hPDCD1LG2 | ANA931 | 9606 |
| PECAM1 | hPECAM1 | ANA1044 | 9606 |
| PF4 | hPF4 | ANA205 | 9606 |
| PF4V1 | hPF4V1 | ANA206 | 9606 |
| PIGF | PIGF | ANA715 | 9606 |
| PIGF1 | PIGF | ANA715 | 9606 |
| PLAUR | hPLAUR | ANA1140 | 9606 |
| PLXNC1 | hPLXNC1 | ANA958 | 9606 |
| PPBP | hPPBP | ANA207 | 9606 |
| PR3 | PRTN3 | ANA703 | 9606 |
| PRF1 | hPRF1 | ANA890 | 9606 |
| PRNP | hPRNP | ANA936 | 9606 |
| PROCR | hPROCR | ANA1259 | 9606 |
| PROM1 | hPROM1 | ANA954 | 9606 |
| PRTN3 | PRTN3 | ANA703 | 9606 |
| PSG1 | hPSG1 | ANA1010 | 9606 |
| PTGDR2 | hPTGDR2 | ANA1264 | 9606 |
| PTGFRN | hPTGFRN | ANA1248 | 9606 |
| PTPRC | hPTPRC/iso:h6 | ANA816 | 9606 |
| PTPRC/iso:CD45RO | PTPRC/iso:CD45RO | ANA822 | 9606 |
| PTPRJ | hPTPRJ | ANA1151 | 9606 |
| PVR | hPVR | ANA1034 | 9606 |
| Pdgfa | mPDGFA | ANA655 | 10090 |
| Pdgfb | mPDGFB | ANA656 | 10090 |
| Pdgfra | mPDGFRA | ANA657 | 10090 |
| Pdgfrb | mPDGFRB | ANA658 | 10090 |
| Perforin | hPRF1 | ANA890 | 9606 |
| Pf4 | mPF4 | ANA659 | 10090 |
| Ppbp | PPBP | ANA660 | 10090 |
| RANKL | hTNFSF11 | ANA238 | 9606 |
| RANTES | hCCL5 | ANA27 | 9606 |
| RESISTIN | hRETN | ANA208 | 9606 |
| RETN | hRETN | ANA208 | 9606 |
| RHAG | hRHAG | ANA1137 | 9606 |
| RHCE | hRHCE | ANA1053 | 9606 |
| RHD | hRHD | ANA1138 | 9606 |
| Rantes | hCCL5 | ANA27 | 9606 |
| Resistin | hRETN | ANA208 | 9606 |
| Retn | mRETN | ANA661 | 10090 |
| SCF | hKITLG | ANA186 | 9606 |
| SDC1 | hSDC1 | ANA891 | 9606 |
| SDF1A | hCXCL12 | ANA63 | 9606 |
| SECISBP2L | hSECISBP2L | ANA906 | 9606 |
| SELE | hSELE | ANA1046 | 9606 |
| SELP | hSELP | ANA1042 | 9606 |
| SELPLG | hSELPLG | ANA903 | 9606 |
| SEMA4D | hSEMA4D | ANA1218 | 9606 |
| SEMA7A | hSEMA7A | ANA965 | 9606 |
| SERPINE1 | SERPINE1 | ANA708 | 9606 |
| SIGLEC-2 | hCD22 | ANA862 | 9606 |
| SIGLEC-3 | hCD33 | ANA864 | 9606 |
| SIGLEC1 | hSIGLEC1 | ANA1227 | 9606 |
| SIGLEC2 | hCD22 | ANA862 | 9606 |
| SIGLEC3 | hCD33 | ANA864 | 9606 |
| SIGLEC5 | hSIGLEC5 | ANA951 | 9606 |
| SIGLEC6 | hSIGLEC6 | ANA955 | 9606 |
| SIGLEC7 | hSIGLEC7 | ANA1262 | 9606 |
| SIGLEC9 | hSIGLEC9 | ANA1263 | 9606 |
| SIRPA | hSIRPA | ANA1130 | 9606 |
| SIRPB1 | hSIRPB1 | ANA935 | 9606 |
| SIRPG | hSIRPG | ANA1247 | 9606 |
| SLAMF1 | hSLAMF1 | ANA1152 | 9606 |
| SLAMF7 | hSLAMF7 | ANA1242 | 9606 |
| SLAN | hSECISBP2L | ANA906 | 9606 |
| SLC44A1 | hSLC44A1 | ANA1211 | 9606 |
| SLC4A1 | hSLC4A1 | ANA977 | 9606 |
| SLC7A5 | hSLC7A5 | ANA1136 | 9606 |
| SOL CD40L | hCD40LG | ANA43 | 9606 |
| SPN | hSPN | ANA893 | 9606 |
| SPP1 | hSPP1 | ANA209 | 9606 |
| STAT1 | hSTAT1 | ANA892 | 9606 |
| STAT3 | hSTAT3 | ANA900 | 9606 |
| STAT5 | hSTAT5A | ANA901 | 9606 |
| STAT5A | hSTAT5A | ANA901 | 9606 |
| Slan | hSECISBP2L | ANA906 | 9606 |
| Spp1 | mSPP1 | ANA662 | 10090 |
| TARC | hCCL17 | ANA8 | 9606 |
| TDGF1P2 | hTDGF1P3 | ANA210 | 9606 |
| TDGF1P3 | TDGF1P3 | ANA211 | 9606 |
| TEK | hTEK | ANA1139 | 9606 |
| TGF-a | TGFA | ANA212 | 9606 |
| TGF-b | hTGFB1 | ANA213 | 9606 |
| TGFA | TGFA | ANA212 | 9606 |
| TGFB | hTGFB1 | ANA213 | 9606 |
| TGFB1 | hTGFB1 | ANA213 | 9606 |
| TGFB2 | hTGFB2 | ANA214 | 9606 |
| TGFB3 | hTGFB3 | ANA215 | 9606 |
| TGFBR1 | hTGFBR1 | ANA216 | 9606 |
| TGFBR2 | hTGFBR2 | ANA217 | 9606 |
| TGFBR3 | hTGFBR3 | ANA218 | 9606 |
| THBD | hTHBD | ANA894 | 9606 |
| THPO | hTHPO | ANA219 | 9606 |
| TLR1 | hTLR1 | ANA1159 | 9606 |
| TLR10 | hTLR10 | ANA1225 | 9606 |
| TLR2 | hTLR2 | ANA959 | 9606 |
| TLR3 | hTLR3 | ANA952 | 9606 |
| TLR4 | hTLR4 | ANA944 | 9606 |
| TLR5 | hTLR5 | ANA872 | 9606 |
| TLR5 FITC | hTLR5 | ANA872 | 9606 |
| TLR6 | hTLR6 | ANA867 | 9606 |
| TLR6 PE | hTLR6 | ANA867 | 9606 |
| TLR7 | hTLR7 | ANA39 | 9606 |
| TLR8 | hTLR8 | ANA1245 | 9606 |
| TLR9 | hTLR9 | ANA1244 | 9606 |
| TNF | hTNF | ANA220 | 9606 |
| TNF-A | hTNF | ANA220 | 9606 |
| TNF-B | hLTA | ANA192 | 9606 |
| TNF-a | hTNF | ANA220 | 9606 |
| TNF-a PE Cy7-A | hTNF | ANA220 | 9606 |
| TNF-alpha | hTNF | ANA220 | 9606 |
| TNFA | hTNF | ANA220 | 9606 |
| TNFB | hLTA | ANA192 | 9606 |
| TNFRSF10A | hTNFRSF10A | ANA221 | 9606 |
| TNFRSF10B | hTNFRSF10B | ANA222 | 9606 |
| TNFRSF10C | hTNFRSF10C | ANA223 | 9606 |
| TNFRSF10D | hTNFRSF10D | ANA224 | 9606 |
| TNFRSF11A | hTNFRSF11A | ANA225 | 9606 |
| TNFRSF11B | hTNFRSF11B | ANA226 | 9606 |
| TNFRSF12A | hTNFRSF12A | ANA1240 | 9606 |
| TNFRSF13B | hTNFRSF13B | ANA227 | 9606 |
| TNFRSF13C | hTNFRSF13C | ANA1222 | 9606 |
| TNFRSF14 | hTNFRSF14 | ANA228 | 9606 |
| TNFRSF17 | hTNFRSF17 | ANA229 | 9606 |
| TNFRSF18 | hTNFRSF18 | ANA230 | 9606 |
| TNFRSF1A | hTNFRSF1A | ANA231 | 9606 |
| TNFRSF1B | hTNFRSF1B | ANA232 | 9606 |
| TNFRSF25 | hTNFRSF25 | ANA233 | 9606 |
| TNFRSF4 | hTNFRSF4 | ANA234 | 9606 |
| TNFRSF8 | hTNFRSF8 | ANA235 | 9606 |
| TNFRSF9 | hTNFRSF9 | ANA236 | 9606 |
| TNFSF10 | hTNFSF10 | ANA237 | 9606 |
| TNFSF11 | hTNFSF11 | ANA238 | 9606 |
| TNFSF12 | hTNFSF12 | ANA239 | 9606 |
| TNFSF13 | hTNFSF13 | ANA240 | 9606 |
| TNFSF13B | hTNFSF13B | ANA241 | 9606 |
| TNFSF14 | hTNFSF14 | ANA242 | 9606 |
| TNFSF15 | hTNFSF15 | ANA243 | 9606 |
| TNFSF18 | hTNFSF18 | ANA244 | 9606 |
| TNFSF4 | hTNFSF4 | ANA245 | 9606 |
| TNFSF8 | hTNFSF8 | ANA246 | 9606 |
| TNFSF9 | hTNFSF9 | ANA247 | 9606 |
| TNFa | hTNF | ANA220 | 9606 |
| TNFb | hLTA | ANA192 | 9606 |
| TPO | hTHPO | ANA219 | 9606 |
| TRAIL | hTNFSF10 | ANA237 | 9606 |
| TSLP | TSLP | ANA716 | 9606 |
| TSPAN7 | hTSPAN7 | ANA1113 | 9606 |
| Tgfa | Tgfa | ANA663 | 10090 |
| Tgfb1 | mTGFB1 | ANA664 | 10090 |
| Tgfb2 | mTGFB2 | ANA665 | 10090 |
| Tgfb3 | mTGFB3 | ANA666 | 10090 |
| Tgfbr1 | mTGFBR1 | ANA667 | 10090 |
| Tgfbr2 | mTGFBR2 | ANA668 | 10090 |
| Tgfbr3 | mTGFBR3 | ANA669 | 10090 |
| Thpo | mTHPO | ANA670 | 10090 |
| Tnf | mTNF | ANA671 | 10090 |
| Tnfa | mTNF | ANA671 | 10090 |
| Tnfb | mLTA | ANA645 | 10090 |
| Tnfrsf10b | mTnfrsf10b | ANA672 | 10090 |
| Tnfrsf11a | mTNFRSF11A | ANA673 | 10090 |
| Tnfrsf11b | mTNFRSF11B | ANA674 | 10090 |
| Tnfrsf13b | mTNFRSF13B | ANA675 | 10090 |
| Tnfrsf14 | mTNFRSF14 | ANA676 | 10090 |
| Tnfrsf17 | mTNFRSF17 | ANA677 | 10090 |
| Tnfrsf18 | mTnfrsf18 | ANA678 | 10090 |
| Tnfrsf1a | mTNFRSF1A | ANA679 | 10090 |
| Tnfrsf1b | mTNFRSF1B | ANA680 | 10090 |
| Tnfrsf25 | TNFRSF25 | ANA681 | 10090 |
| Tnfrsf4 | mTNFRSF4 | ANA682 | 10090 |
| Tnfrsf8 | mTNFRSF8 | ANA683 | 10090 |
| Tnfrsf9 | mTNFRSF9 | ANA684 | 10090 |
| Tnfsf10 | mTNFSF10 | ANA685 | 10090 |
| Tnfsf11 | mTNFSF11 | ANA686 | 10090 |
| Tnfsf12 | mTNFSF12 | ANA687 | 10090 |
| Tnfsf13 | mTNFSF13 | ANA688 | 10090 |
| Tnfsf13b | mTNFSF13B | ANA689 | 10090 |
| Tnfsf14 | mTNFSF14 | ANA690 | 10090 |
| Tnfsf15 | mTNFSF15 | ANA691 | 10090 |
| Tnfsf18 | mTNFSF18 | ANA692 | 10090 |
| Tnfsf4 | mTNFSF4 | ANA693 | 10090 |
| Tnfsf8 | mTNFSF8 | ANA694 | 10090 |
| Tnfsf9 | mTNFSF9 | ANA695 | 10090 |
| V-CAM-1 | VCAM1 | ANA702 | 9606 |
| VCAM1 | VCAM1 | ANA702 | 9606 |
| VEGF | VEGFA | ANA709 | 9606 |
| VEGFA | VEGFA | ANA709 | 9606 |
| VEGFD | hVEGFD | ANA710 | 9606 |
| VPREB1 | hVPREB1 | ANA1017 | 9606 |
| XCL1 | hXCL1 | ANA248 | 9606 |
| XCL2 | hXCL2 | ANA249 | 9606 |
| XCR1 | hXCR1 | ANA250 | 9606 |
| Xcl1 | mXCL1 | ANA696 | 10090 |
| Xcr1 | mXCR1 | ANA697 | 10090 |
| bcl2 | hBCL2 | ANA904 | 9606 |
| fam:hIFNA | fam:hIFNA | ANA717 | 9606 |
| gmcsf | hCSF2 | ANA53 | 9606 |
| hABCB1 | hABCB1 | ANA996 | 9606 |
| hABCG2 | hABCG2 | ANA1260 | 9606 |
| hACE | hACE | ANA1019 | 9606 |
| hACKR1 | hACKR1 | ANA1161 | 9606 |
| hACKR3 | hACKR3 | ANA1 | 9606 |
| hADAM10 | hADAM10 | ANA948 | 9606 |
| hADAM17 | hADAM17 | ANA1133 | 9606 |
| hADAM8 | hADAM8 | ANA1131 | 9606 |
| hADGRE2 | hADGRE2 | ANA1253 | 9606 |
| hADGRE5 | hADGRE5 | ANA1120 | 9606 |
| hALCAM | hALCAM | ANA1154 | 9606 |
| hALK | hALK | ANA1258 | 9606 |
| hANPEP | hANPEP | ANA1033 | 9606 |
| hANXA5 | hANXA5 | ANA909 | 9606 |
| hART1 | hART1 | ANA1123 | 9606 |
| hART4 | hART4 | ANA1220 | 9606 |
| hATP1B3 | hATP1B3 | ANA1124 | 9606 |
| hB3GAT1 | hB3GAT1 | ANA823 | 9606 |
| hBCAM | hBCAM | ANA1122 | 9606 |
| hBCL2 | hBCL2 | ANA904 | 9606 |
| hBCL6 | hBCL6 | ANA910 | 9606 |
| hBMPR1A | hBMPR1A | ANA1101 | 9606 |
| hBMPR1B | hBMPR1B | ANA945 | 9606 |
| hBSG | hBSG | ANA1098 | 9606 |
| hBST1 | hBST1 | ANA1149 | 9606 |
| hBST2 | hBST2 | ANA1150 | 9606 |
| hBTLA | hBTLA | ANA1191 | 9606 |
| hBTN3A1 | hBTN3A1 | ANA946 | 9606 |
| hC5AR1 | hC5AR1 | ANA1063 | 9606 |
| hCASP3 | hCASP3 | ANA911 | 9606 |
| hCCL1 | hCCL1 | ANA2 | 9606 |
| hCCL11 | hCCL11 | ANA3 | 9606 |
| hCCL13 | hCCL13 | ANA4 | 9606 |
| hCCL14 | hCCL14 | ANA5 | 9606 |
| hCCL15 | hCCL15 | ANA6 | 9606 |
| hCCL16 | hCCL16 | ANA7 | 9606 |
| hCCL17 | hCCL17 | ANA8 | 9606 |
| hCCL18 | hCCL18 | ANA9 | 9606 |
| hCCL19 | hCCL19 | ANA10 | 9606 |
| hCCL2 | hCCL2 | ANA11 | 9606 |
| hCCL20 | hCCL20 | ANA12 | 9606 |
| hCCL21 | hCCL21 | ANA13 | 9606 |
| hCCL22 | hCCL22 | ANA14 | 9606 |
| hCCL23 | hCCL23 | ANA15 | 9606 |
| hCCL24 | hCCL24 | ANA16 | 9606 |
| hCCL25 | hCCL25 | ANA17 | 9606 |
| hCCL26 | hCCL26 | ANA18 | 9606 |
| hCCL27 | hCCL27 | ANA19 | 9606 |
| hCCL3 | hCCL3 | ANA20 | 9606 |
| hCCL3L | hCCL3L | ANA22 | 9606 |
| hCCL4 | hCCL4 | ANA24 | 9606 |
| hCCL4L | hCCL4L | ANA26 | 9606 |
| hCCL5 | hCCL5 | ANA27 | 9606 |
| hCCL7 | hCCL7 | ANA28 | 9606 |
| hCCL8 | hCCL8 | ANA29 | 9606 |
| hCCR1 | hCCR1 | ANA30 | 9606 |
| hCCR10 | hCCR10 | ANA31 | 9606 |
| hCCR2 | hCCR2 | ANA32 | 9606 |
| hCCR3 | hCCR3 | ANA33 | 9606 |
| hCCR4 | hCCR4 | ANA34 | 9606 |
| hCCR5 | hCCR5 | ANA35 | 9606 |
| hCCR6 | hCCR6 | ANA36 | 9606 |
| hCCR7 | hCCR7 | ANA37 | 9606 |
| hCCR8 | hCCR8 | ANA38 | 9606 |
| hCCR9 | hCCR9 | ANA824 | 9606 |
| hCD101 | hCD101 | ANA1219 | 9606 |
| hCD109 | hCD109 | ANA1188 | 9606 |
| hCD14 | hCD14 | ANA804 | 9606 |
| hCD151 | hCD151 | ANA1119 | 9606 |
| hCD160 | hCD160 | ANA973 | 9606 |
| hCD163 | hCD163 | ANA1192 | 9606 |
| hCD164 | hCD164 | ANA1141 | 9606 |
| hCD177 | hCD177 | ANA1203 | 9606 |
| hCD180 | hCD180 | ANA1223 | 9606 |
| hCD19 | hCD19 | ANA805 | 9606 |
| hCD1A | hCD1A | ANA988 | 9606 |
| hCD1B | hCD1B | ANA1084 | 9606 |
| hCD1C | hCD1C | ANA895 | 9606 |
| hCD1D | hCD1D | ANA1039 | 9606 |
| hCD1E | hCD1E | ANA1038 | 9606 |
| hCD2 | hCD2 | ANA860 | 9606 |
| hCD200 | hCD200 | ANA1111 | 9606 |
| hCD207 | hCD207 | ANA1255 | 9606 |
| hCD209 | hCD209 | ANA869 | 9606 |
| hCD22 | hCD22 | ANA862 | 9606 |
| hCD226 | hCD226 | ANA1160 | 9606 |
| hCD24 | hCD24 | ANA807 | 9606 |
| hCD244 | hCD244 | ANA1226 | 9606 |
| hCD247 | hCD247 | ANA1060 | 9606 |
| hCD248 | hCD248 | ANA1236 | 9606 |
| hCD27 | hCD27 | ANA40 | 9606 |
| hCD274 | hCD274 | ANA1246 | 9606 |
| hCD276 | hCD276 | ANA1169 | 9606 |
| hCD28 | hCD28 | ANA863 | 9606 |
| hCD300A | hCD300A | ANA1252 | 9606 |
| hCD300C | hCD300C | ANA1146 | 9606 |
| hCD300E | hCD300E | ANA1167 | 9606 |
| hCD302 | hCD302 | ANA1196 | 9606 |
| hCD320 | hCD320 | ANA1241 | 9606 |
| hCD33 | hCD33 | ANA864 | 9606 |
| hCD34 | hCD34 | ANA1083 | 9606 |
| hCD36 | hCD36 | ANA1047 | 9606 |
| hCD37 | hCD37 | ANA1008 | 9606 |
| hCD38 | hCD38 | ANA808 | 9606 |
| hCD3D | hCD3D | ANA979 | 9606 |
| hCD3E | hCD3E | ANA809 | 9606 |
| hCD3G | hCD3G | ANA1003 | 9606 |
| hCD4 | hCD4 | ANA41 | 9606 |
| hCD40 | hCD40 | ANA42 | 9606 |
| hCD40LG | hCD40LG | ANA43 | 9606 |
| hCD44 | hCD44 | ANA914 | 9606 |
| hCD46 | hCD46 | ANA1036 | 9606 |
| hCD47 | hCD47 | ANA1147 | 9606 |
| hCD48 | hCD48 | ANA1001 | 9606 |
| hCD5 | hCD5 | ANA915 | 9606 |
| hCD52 | hCD52 | ANA1087 | 9606 |
| hCD53 | hCD53 | ANA1057 | 9606 |
| hCD55 | hCD55 | ANA995 | 9606 |
| hCD58 | hCD58 | ANA1056 | 9606 |
| hCD59 | hCD59 | ANA1030 | 9606 |
| hCD6 | hCD6 | ANA1085 | 9606 |
| hCD63 | hCD63 | ANA902 | 9606 |
| hCD68 | hCD68 | ANA1096 | 9606 |
| hCD69 | hCD69 | ANA865 | 9606 |
| hCD7 | hCD7 | ANA1002 | 9606 |
| hCD70 | hCD70 | ANA44 | 9606 |
| hCD72 | hCD72 | ANA1066 | 9606 |
| hCD74 | hCD74 | ANA978 | 9606 |
| hCD79A | hCD79A | ANA1015 | 9606 |
| hCD79B | hCD79B | ANA1109 | 9606 |
| hCD80 | hCD80 | ANA866 | 9606 |
| hCD81 | hCD81 | ANA1129 | 9606 |
| hCD82 | hCD82 | ANA1082 | 9606 |
| hCD83 | hCD83 | ANA916 | 9606 |
| hCD84 | hCD84 | ANA1254 | 9606 |
| hCD86 | hCD86 | ANA868 | 9606 |
| hCD8A | hCD8A | ANA810 | 9606 |
| hCD8B | hCD8B | ANA1007 | 9606 |
| hCD9 | hCD9 | ANA1068 | 9606 |
| hCD93 | hCD93 | ANA918 | 9606 |
| hCD96 | hCD96 | ANA1106 | 9606 |
| hCD99 | hCD99 | ANA1031 | 9606 |
| hCDCP1 | hCDCP1 | ANA1234 | 9606 |
| hCDH1 | hCDH1 | ANA1020 | 9606 |
| hCDH2 | hCDH2 | ANA1055 | 9606 |
| hCDH5 | hCDH5 | ANA1095 | 9606 |
| hCEACAM1 | hCEACAM1 | ANA1027 | 9606 |
| hCEACAM3 | hCEACAM3 | ANA1104 | 9606 |
| hCEACAM5 | hCEACAM5 | ANA990 | 9606 |
| hCEACAM6 | hCEACAM6 | ANA1105 | 9606 |
| hCEACAM8 | hCEACAM8 | ANA1091 | 9606 |
| hCENPB | hCENPB | ANA821 | 9606 |
| hCKLF | hCKLF | ANA45 | 9606 |
| hCLCF1 | hCLCF1 | ANA46 | 9606 |
| hCLEC10A | hCLEC10A | ANA1195 | 9606 |
| hCLEC4C | hCLEC4C | ANA870 | 9606 |
| hCLEC4M | hCLEC4M | ANA1233 | 9606 |
| hCMTM1 | hCMTM1 | ANA47 | 9606 |
| hCMTM6 | hCMTM6 | ANA48 | 9606 |
| hCMTM7 | hCMTM7 | ANA49 | 9606 |
| hCNMD | hCNMD | ANA188 | 9606 |
| hCNTFR | hCNTFR | ANA50 | 9606 |
| hCR1 | hCR1 | ANA1051 | 9606 |
| hCR2 | hCR2 | ANA919 | 9606 |
| hCSF1 | hCSF1 | ANA51 | 9606 |
| hCSF1R | hCSF1R | ANA52 | 9606 |
| hCSF2 | hCSF2 | ANA53 | 9606 |
| hCSF2RA | hCSF2RA | ANA54 | 9606 |
| hCSF2RB | hCSF2RB | ANA55 | 9606 |
| hCSF3 | hCSF3 | ANA56 | 9606 |
| hCSF3R | hCSF3R | ANA57 | 9606 |
| hCTLA4 | hCTLA4 | ANA871 | 9606 |
| hCX3CL1 | hCX3CL1 | ANA58 | 9606 |
| hCX3CR1 | hCX3CR1 | ANA59 | 9606 |
| hCXCL1 | hCXCL1 | ANA60 | 9606 |
| hCXCL10 | hCXCL10 | ANA61 | 9606 |
| hCXCL11 | hCXCL11 | ANA62 | 9606 |
| hCXCL12 | hCXCL12 | ANA63 | 9606 |
| hCXCL13 | hCXCL13 | ANA64 | 9606 |
| hCXCL14 | hCXCL14 | ANA65 | 9606 |
| hCXCL16 | hCXCL16 | ANA66 | 9606 |
| hCXCL17 | hCXCL17 | ANA67 | 9606 |
| hCXCL2 | hCXCL2 | ANA68 | 9606 |
| hCXCL3 | hCXCL3 | ANA69 | 9606 |
| hCXCL5 | hCXCL5 | ANA70 | 9606 |
| hCXCL6 | hCXCL6 | ANA71 | 9606 |
| hCXCL8 | hCXCL8 | ANA72 | 9606 |
| hCXCL9 | hCXCL9 | ANA73 | 9606 |
| hCXCR1 | hCXCR1 | ANA74 | 9606 |
| hCXCR2 | hCXCR2 | ANA75 | 9606 |
| hCXCR3 | hCXCR3 | ANA76 | 9606 |
| hCXCR4 | hCXCR4 | ANA77 | 9606 |
| hCXCR5 | hCXCR5 | ANA78 | 9606 |
| hCXCR6 | hCXCR6 | ANA79 | 9606 |
| hDDR1 | hDDR1 | ANA1145 | 9606 |
| hDPP4 | hDPP4 | ANA1081 | 9606 |
| hEBI3 | hEBI3 | ANA80 | 9606 |
| hEGF | hEGF | ANA81 | 9606 |
| hEGFR | hEGFR | ANA82 | 9606 |
| hENG | hENG | ANA1050 | 9606 |
| hENPEP | hENPEP | ANA1142 | 9606 |
| hENPP3 | hENPP3 | ANA947 | 9606 |
| hENTPD1 | hENTPD1 | ANA921 | 9606 |
| hEPCAM | hEPCAM | ANA1045 | 9606 |
| hEPO | hEPO | ANA83 | 9606 |
| hEPOR | hEPOR | ANA84 | 9606 |
| hERBB2 | hERBB2 | ANA982 | 9606 |
| hF11R | hF11R | ANA1265 | 9606 |
| hF3 | hF3 | ANA1028 | 9606 |
| hFAS | hFAS | ANA85 | 9606 |
| hFASLG | hFASLG | ANA86 | 9606 |
| hFCAR | hFCAR | ANA1075 | 9606 |
| hFCER2 | hFCER2 | ANA922 | 9606 |
| hFCGR1A | hFCGR1A | ANA873 | 9606 |
| hFCGR2A | hFCGR2A | ANA1018 | 9606 |
| hFCGR2B | hFCGR2B | ANA1088 | 9606 |
| hFCGR2C | hFCGR2C | ANA1089 | 9606 |
| hFCGR3A | hFCGR3A | ANA811 | 9606 |
| hFCGR3B | hFCGR3B | ANA960 | 9606 |
| hFGF1 | hFGF1 | ANA87 | 9606 |
| hFGF2 | hFGF2 | ANA88 | 9606 |
| hFGFR1 | hFGFR1 | ANA1009 | 9606 |
| hFGFR2 | hFGFR2 | ANA1065 | 9606 |
| hFGFR3 | hFGFR3 | ANA1070 | 9606 |
| hFGFR4 | hFGFR4 | ANA1069 | 9606 |
| hFLT3 | hFLT3 | ANA89 | 9606 |
| hFLT3LG | hFLT3LG | ANA90 | 9606 |
| hFOXP3 | hFOXP3 | ANA874 | 9606 |
| hFUT3 | hFUT3 | ANA1061 | 9606 |
| hFUT4 | hFUT4 | ANA875 | 9606 |
| hFZD10 | hFZD10 | ANA1257 | 9606 |
| hFZD4 | hFZD4 | ANA1256 | 9606 |
| hFZD9 | hFZD9 | ANA943 | 9606 |
| hGDF15 | hGDF15 | ANA91 | 9606 |
| hGGT1 | hGGT1 | ANA1058 | 9606 |
| hGP1BA | hGP1BA | ANA992 | 9606 |
| hGP1BB | hGP1BB | ANA1022 | 9606 |
| hGP5 | hGP5 | ANA1103 | 9606 |
| hGP9 | hGP9 | ANA1032 | 9606 |
| hGPR15 | hGPR15 | ANA896 | 9606 |
| hGYPA | hGYPA | ANA976 | 9606 |
| hGYPB | hGYPB | ANA987 | 9606 |
| hGYPC | hGYPC | ANA983 | 9606 |
| hGZMB | hGZMB | ANA897 | 9606 |
| hHGF | hHGF | ANA92 | 9606 |
| hHLA-A | hHLA-A | ANA938 | 9606 |
| hHLA-A*2 | hHLA-A*2 | ANA975 | 9606 |
| hHLA-C | hHLA-C | ANA939 | 9606 |
| hHLA-DRA | hHLA-DRA | ANA812 | 9606 |
| hHLA-E | hHLA-E | ANA1029 | 9606 |
| hHLA-G | hHLA-G | ANA1049 | 9606 |
| hHMMR | hHMMR | ANA966 | 9606 |
| hICAM2 | hICAM2 | ANA1025 | 9606 |
| hICAM3 | hICAM3 | ANA1094 | 9606 |
| hICAM4 | hICAM4 | ANA1155 | 9606 |
| hICOS | hICOS | ANA898 | 9606 |
| hICOSLG | hICOSLG | ANA964 | 9606 |
| hIFITM1 | hIFITM1 | ANA1021 | 9606 |
| hIFNA10 | hIFNA10 | ANA94 | 9606 |
| hIFNA14 | hIFNA14 | ANA96 | 9606 |
| hIFNA16 | hIFNA16 | ANA97 | 9606 |
| hIFNA17 | hIFNA17 | ANA98 | 9606 |
| hIFNA2 | hIFNA2 | ANA99 | 9606 |
| hIFNA21 | hIFNA21 | ANA100 | 9606 |
| hIFNA4 | hIFNA4 | ANA101 | 9606 |
| hIFNA5 | hIFNA5 | ANA102 | 9606 |
| hIFNA6 | hIFNA6 | ANA103 | 9606 |
| hIFNA7 | hIFNA7 | ANA104 | 9606 |
| hIFNA8 | hIFNA8 | ANA105 | 9606 |
| hIFNAR1 | hIFNAR1 | ANA106 | 9606 |
| hIFNAR2 | hIFNAR2 | ANA107 | 9606 |
| hIFNB1 | hIFNB1 | ANA108 | 9606 |
| hIFNE | hIFNE | ANA109 | 9606 |
| hIFNG | hIFNG | ANA110 | 9606 |
| hIFNGR1 | hIFNGR1 | ANA111 | 9606 |
| hIFNGR2 | hIFNGR2 | ANA112 | 9606 |
| hIFNK | hIFNK | ANA113 | 9606 |
| hIFNL1 | hIFNL1 | ANA114 | 9606 |
| hIFNL2 | hIFNL2 | ANA115 | 9606 |
| hIFNL3 | hIFNL3 | ANA116 | 9606 |
| hIFNLR1 | hIFNLR1 | ANA117 | 9606 |
| hIGF1R | hIGF1R | ANA993 | 9606 |
| hIGF2R | hIGF2R | ANA1013 | 9606 |
| hIGHA1 | hIGHA1 | ANA820 | 9606 |
| hIGHA2 | hIGHA2 | ANA819 | 9606 |
| hIGHD | hIGHD | ANA813 | 9606 |
| hIGHM | hIGHM | ANA817 | 9606 |
| hIGLL1 | hIGLL1 | ANA1040 | 9606 |
| hIGSF8 | hIGSF8 | ANA1221 | 9606 |
| hIL10 | hIL10 | ANA118 | 9606 |
| hIL10RA | hIL10RA | ANA119 | 9606 |
| hIL10RB | hIL10RB | ANA120 | 9606 |
| hIL11 | hIL11 | ANA121 | 9606 |
| hIL11RA | hIL11RA | ANA122 | 9606 |
| hIL12 | hIL12 | ANA800 | 9606 |
| hIL12A | hIL12A | ANA123 | 9606 |
| hIL12B | hIL12B | ANA124 | 9606 |
| hIL12RB1 | hIL12RB1 | ANA125 | 9606 |
| hIL12RB2 | hIL12RB2 | ANA126 | 9606 |
| hIL13 | hIL13 | ANA127 | 9606 |
| hIL13RA1 | hIL13RA1 | ANA128 | 9606 |
| hIL13RA2 | hIL13RA2 | ANA129 | 9606 |
| hIL15 | hIL15 | ANA130 | 9606 |
| hIL15RA | hIL15RA | ANA131 | 9606 |
| hIL16 | hIL16 | ANA132 | 9606 |
| hIL17A | hIL17A | ANA133 | 9606 |
| hIL17B | hIL17B | ANA134 | 9606 |
| hIL17C | hIL17C | ANA135 | 9606 |
| hIL17D | hIL17D | ANA136 | 9606 |
| hIL17F | hIL17F | ANA137 | 9606 |
| hIL17F-17A | hIL17F-17A | ANA801 | 9606 |
| hIL17RA | hIL17RA | ANA138 | 9606 |
| hIL18 | hIL18 | ANA139 | 9606 |
| hIL18R1 | hIL18R1 | ANA140 | 9606 |
| hIL18RAP | hIL18RAP | ANA972 | 9606 |
| hIL19 | hIL19 | ANA141 | 9606 |
| hIL1A | hIL1A | ANA142 | 9606 |
| hIL1B | hIL1B | ANA143 | 9606 |
| hIL1F10 | hIL1F10 | ANA144 | 9606 |
| hIL1R1 | hIL1R1 | ANA145 | 9606 |
| hIL1R2 | hIL1R2 | ANA146 | 9606 |
| hIL1RN | hIL1RN | ANA147 | 9606 |
| hIL2 | hIL2 | ANA148 | 9606 |
| hIL20 | hIL20 | ANA149 | 9606 |
| hIL20RA | hIL20RA | ANA150 | 9606 |
| hIL20RB | hIL20RB | ANA151 | 9606 |
| hIL21 | hIL21 | ANA152 | 9606 |
| hIL21R | hIL21R | ANA153 | 9606 |
| hIL22 | hIL22 | ANA154 | 9606 |
| hIL22RA1 | hIL22RA1 | ANA155 | 9606 |
| hIL22RA2 | hIL22RA2 | ANA156 | 9606 |
| hIL23 | hIL23 | ANA802 | 9606 |
| hIL23A | hIL23A | ANA157 | 9606 |
| hIL23R | hIL23R | ANA158 | 9606 |
| hIL24 | hIL24 | ANA159 | 9606 |
| hIL25 | hIL25 | ANA160 | 9606 |
| hIL26 | hIL26 | ANA161 | 9606 |
| hIL27 | hIL27 | ANA162 | 9606 |
| hIL2RA | hIL2RA | ANA163 | 9606 |
| hIL2RB | hIL2RB | ANA164 | 9606 |
| hIL2RG | hIL2RG | ANA165 | 9606 |
| hIL3 | hIL3 | ANA166 | 9606 |
| hIL31 | hIL31 | ANA167 | 9606 |
| hIL32 | hIL32 | ANA168 | 9606 |
| hIL33 | hIL33 | ANA169 | 9606 |
| hIL34 | hIL34 | ANA170 | 9606 |
| hIL36G | hIL36G | ANA171 | 9606 |
| hIL36RN | hIL36RN | ANA172 | 9606 |
| hIL3RA | hIL3RA | ANA173 | 9606 |
| hIL4 | hIL4 | ANA174 | 9606 |
| hIL4R | hIL4R | ANA175 | 9606 |
| hIL5 | hIL5 | ANA176 | 9606 |
| hIL5RA | hIL5RA | ANA177 | 9606 |
| hIL6 | hIL6 | ANA178 | 9606 |
| hIL6R | hIL6R | ANA179 | 9606 |
| hIL6ST | hIL6ST | ANA180 | 9606 |
| hIL7 | hIL7 | ANA181 | 9606 |
| hIL7R | hIL7R | ANA182 | 9606 |
| hIL9 | hIL9 | ANA183 | 9606 |
| hIL9R | hIL9R | ANA184 | 9606 |
| hINSR | hINSR | ANA989 | 9606 |
| hITGA1 | hITGA1 | ANA927 | 9606 |
| hITGA2 | hITGA2 | ANA1048 | 9606 |
| hITGA2B | hITGA2B | ANA997 | 9606 |
| hITGA3 | hITGA3 | ANA1079 | 9606 |
| hITGA4 | hITGA4 | ANA1026 | 9606 |
| hITGA5 | hITGA5 | ANA999 | 9606 |
| hITGA6 | hITGA6 | ANA876 | 9606 |
| hITGAD | hITGAD | ANA1153 | 9606 |
| hITGAE | hITGAE | ANA877 | 9606 |
| hITGAL | hITGAL | ANA1059 | 9606 |
| hITGAM | hITGAM | ANA878 | 9606 |
| hITGAV | hITGAV | ANA991 | 9606 |
| hITGAX | hITGAX | ANA814 | 9606 |
| hITGB1 | hITGB1 | ANA986 | 9606 |
| hITGB2 | hITGB2 | ANA985 | 9606 |
| hITGB3 | hITGB3 | ANA984 | 9606 |
| hITGB4 | hITGB4 | ANA1043 | 9606 |
| hJAG1 | hJAG1 | ANA1132 | 9606 |
| hJAM2 | hJAM2 | ANA1126 | 9606 |
| hKDR | hKDR | ANA1100 | 9606 |
| hKEL | hKEL | ANA1073 | 9606 |
| hKIR2DL1 | hKIR2DL1 | ANA879 | 9606 |
| hKIR2DL2 | hKIR2DL2 | ANA880 | 9606 |
| hKIR2DL3 | hKIR2DL3 | ANA881 | 9606 |
| hKIR2DL4 | hKIR2DL4 | ANA1224 | 9606 |
| hKIR2DL5A | hKIR2DL5A | ANA1199 | 9606 |
| hKIR2DS1 | hKIR2DS1 | ANA1157 | 9606 |
| hKIR2DS2 | hKIR2DS2 | ANA1117 | 9606 |
| hKIR2DS4 | hKIR2DS4 | ANA1118 | 9606 |
| hKIR2DS5 | hKIR2DS5 | ANA1156 | 9606 |
| hKIR3DL1 | hKIR3DL1 | ANA882 | 9606 |
| hKIR3DL2 | hKIR3DL2 | ANA1116 | 9606 |
| hKIR3DL3 | hKIR3DL3 | ANA1204 | 9606 |
| hKIT | hKIT | ANA185 | 9606 |
| hKITLG | hKITLG | ANA186 | 9606 |
| hKLRB1 | hKLRB1 | ANA883 | 9606 |
| hKLRC1 | hKLRC1 | ANA861 | 9606 |
| hKLRC2 | hKLRC2 | ANA1080 | 9606 |
| hKLRD1 | hKLRD1 | ANA884 | 9606 |
| hKLRK1 | hKLRK1 | ANA886 | 9606 |
| hL1CAM | hL1CAM | ANA1092 | 9606 |
| hLAG3 | hLAG3 | ANA1054 | 9606 |
| hLAIR1 | hLAIR1 | ANA1180 | 9606 |
| hLAIR2 | hLAIR2 | ANA1181 | 9606 |
| hLAMP1 | hLAMP1 | ANA887 | 9606 |
| hLAMP2 | hLAMP2 | ANA1024 | 9606 |
| hLAMP3 | hLAMP3 | ANA1261 | 9606 |
| hLECT2 | hLECT2 | ANA189 | 9606 |
| hLEPR | hLEPR | ANA899 | 9606 |
| hLIF | hLIF | ANA190 | 9606 |
| hLIFR | hLIFR | ANA191 | 9606 |
| hLILRA1 | hLILRA1 | ANA961 | 9606 |
| hLILRA2 | hLILRA2 | ANA1200 | 9606 |
| hLILRA3 | hLILRA3 | ANA1202 | 9606 |
| hLILRA4 | hLILRA4 | ANA1128 | 9606 |
| hLILRA5 | hLILRA5 | ANA941 | 9606 |
| hLILRA6 | hLILRA6 | ANA1182 | 9606 |
| hLILRB1 | hLILRB1 | ANA888 | 9606 |
| hLILRB2 | hLILRB2 | ANA1201 | 9606 |
| hLILRB3 | hLILRB3 | ANA962 | 9606 |
| hLILRB4 | hLILRB4 | ANA1205 | 9606 |
| hLILRB5 | hLILRB5 | ANA963 | 9606 |
| hLRP1 | hLRP1 | ANA1144 | 9606 |
| hLTA | hLTA | ANA192 | 9606 |
| hLTB | hLTB | ANA187 | 9606 |
| hLTBR | hLTBR | ANA193 | 9606 |
| hLY75 | hLY75 | ANA937 | 9606 |
| hLY9 | hLY9 | ANA1235 | 9606 |
| hMCAM | hMCAM | ANA1115 | 9606 |
| hMELTF | hMELTF | ANA998 | 9606 |
| hMET | hMET | ANA194 | 9606 |
| hMIF | hMIF | ANA195 | 9606 |
| hMKI67 | hMKI67 | ANA889 | 9606 |
| hMME | hMME | ANA930 | 9606 |
| hMPL | hMPL | ANA196 | 9606 |
| hMRC1 | hMRC1 | ANA1072 | 9606 |
| hMRC2 | hMRC2 | ANA1251 | 9606 |
| hMS4A1 | hMS4A1 | ANA806 | 9606 |
| hMSR1 | hMSR1 | ANA1064 | 9606 |
| hMST1 | hMST1 | ANA197 | 9606 |
| hMST1R | hMST1R | ANA198 | 9606 |
| hMUC1 | hMUC1 | ANA1041 | 9606 |
| hNCAM1 | hNCAM1 | ANA815 | 9606 |
| hNCR1 | hNCR1 | ANA967 | 9606 |
| hNCR2 | hNCR2 | ANA885 | 9606 |
| hNCR3 | hNCR3 | ANA950 | 9606 |
| hNECTIN1 | hNECTIN1 | ANA1158 | 9606 |
| hNECTIN2 | hNECTIN2 | ANA1217 | 9606 |
| hNECTIN3 | hNECTIN3 | ANA1243 | 9606 |
| hNGFR | hNGFR | ANA994 | 9606 |
| hNRP1 | hNRP1 | ANA949 | 9606 |
| hNT5E | hNT5E | ANA1062 | 9606 |
| hOSM | hOSM | ANA199 | 9606 |
| hOSMR | hOSMR | ANA200 | 9606 |
| hPDCD1 | hPDCD1 | ANA818 | 9606 |
| hPDCD1LG2 | hPDCD1LG2 | ANA931 | 9606 |
| hPDGF-AB | hPDGF-AB | ANA803 | 9606 |
| hPDGFA | hPDGFA | ANA201 | 9606 |
| hPDGFB | hPDGFB | ANA202 | 9606 |
| hPDGFRA | hPDGFRA | ANA203 | 9606 |
| hPDGFRB | hPDGFRB | ANA204 | 9606 |
| hPECAM1 | hPECAM1 | ANA1044 | 9606 |
| hPF4 | hPF4 | ANA205 | 9606 |
| hPF4V1 | hPF4V1 | ANA206 | 9606 |
| hPLAUR | hPLAUR | ANA1140 | 9606 |
| hPLXNC1 | hPLXNC1 | ANA958 | 9606 |
| hPPBP | hPPBP | ANA207 | 9606 |
| hPRF1 | hPRF1 | ANA890 | 9606 |
| hPRNP | hPRNP | ANA936 | 9606 |
| hPROCR | hPROCR | ANA1259 | 9606 |
| hPROM1 | hPROM1 | ANA954 | 9606 |
| hPSG1 | hPSG1 | ANA1010 | 9606 |
| hPTGDR2 | hPTGDR2 | ANA1264 | 9606 |
| hPTGFRN | hPTGFRN | ANA1248 | 9606 |
| hPTPRC/iso:h6 | hPTPRC/iso:h6 | ANA816 | 9606 |
| hPTPRJ | hPTPRJ | ANA1151 | 9606 |
| hPVR | hPVR | ANA1034 | 9606 |
| hRETN | hRETN | ANA208 | 9606 |
| hRHAG | hRHAG | ANA1137 | 9606 |
| hRHCE | hRHCE | ANA1053 | 9606 |
| hRHD | hRHD | ANA1138 | 9606 |
| hSDC1 | hSDC1 | ANA891 | 9606 |
| hSECISBP2L | hSECISBP2L | ANA906 | 9606 |
| hSELE | hSELE | ANA1046 | 9606 |
| hSELL | hSELL | ANA712 | 9606 |
| hSELP | hSELP | ANA1042 | 9606 |
| hSELPLG | hSELPLG | ANA903 | 9606 |
| hSEMA4D | hSEMA4D | ANA1218 | 9606 |
| hSEMA7A | hSEMA7A | ANA965 | 9606 |
| hSIGLEC1 | hSIGLEC1 | ANA1227 | 9606 |
| hSIGLEC5 | hSIGLEC5 | ANA951 | 9606 |
| hSIGLEC6 | hSIGLEC6 | ANA955 | 9606 |
| hSIGLEC7 | hSIGLEC7 | ANA1262 | 9606 |
| hSIGLEC9 | hSIGLEC9 | ANA1263 | 9606 |
| hSIRPA | hSIRPA | ANA1130 | 9606 |
| hSIRPB1 | hSIRPB1 | ANA935 | 9606 |
| hSIRPG | hSIRPG | ANA1247 | 9606 |
| hSLAMF1 | hSLAMF1 | ANA1152 | 9606 |
| hSLAMF7 | hSLAMF7 | ANA1242 | 9606 |
| hSLC44A1 | hSLC44A1 | ANA1211 | 9606 |
| hSLC4A1 | hSLC4A1 | ANA977 | 9606 |
| hSLC7A5 | hSLC7A5 | ANA1136 | 9606 |
| hSPN | hSPN | ANA893 | 9606 |
| hSPP1 | hSPP1 | ANA209 | 9606 |
| hSTAT1 | hSTAT1 | ANA892 | 9606 |
| hSTAT1/iso:1/Phos:1 | hSTAT1/iso:1/Phos:1 | ANA907 | 9606 |
| hSTAT3 | hSTAT3 | ANA900 | 9606 |
| hSTAT3/Phos:1 | hSTAT3/Phos:1 | ANA908 | 9606 |
| hSTAT5A | hSTAT5A | ANA901 | 9606 |
| hTDGF1P3 | hTDGF1P3 | ANA210 | 9606 |
| hTEK | hTEK | ANA1139 | 9606 |
| hTFRC | hTFRC | ANA932 | 9606 |
| hTGFB1 | hTGFB1 | ANA213 | 9606 |
| hTGFB2 | hTGFB2 | ANA214 | 9606 |
| hTGFB3 | hTGFB3 | ANA215 | 9606 |
| hTGFBR1 | hTGFBR1 | ANA216 | 9606 |
| hTGFBR2 | hTGFBR2 | ANA217 | 9606 |
| hTGFBR3 | hTGFBR3 | ANA218 | 9606 |
| hTHBD | hTHBD | ANA894 | 9606 |
| hTHPO | hTHPO | ANA219 | 9606 |
| hTHY1 | hTHY1 | ANA934 | 9606 |
| hTLR1 | hTLR1 | ANA1159 | 9606 |
| hTLR10 | hTLR10 | ANA1225 | 9606 |
| hTLR2 | hTLR2 | ANA959 | 9606 |
| hTLR3 | hTLR3 | ANA952 | 9606 |
| hTLR4 | hTLR4 | ANA944 | 9606 |
| hTLR5 | hTLR5 | ANA872 | 9606 |
| hTLR6 | hTLR6 | ANA867 | 9606 |
| hTLR7 | hTLR7 | ANA39 | 9606 |
| hTLR8 | hTLR8 | ANA1245 | 9606 |
| hTLR9 | hTLR9 | ANA1244 | 9606 |
| hTNF | hTNF | ANA220 | 9606 |
| hTNFRSF10A | hTNFRSF10A | ANA221 | 9606 |
| hTNFRSF10B | hTNFRSF10B | ANA222 | 9606 |
| hTNFRSF10C | hTNFRSF10C | ANA223 | 9606 |
| hTNFRSF10D | hTNFRSF10D | ANA224 | 9606 |
| hTNFRSF11A | hTNFRSF11A | ANA225 | 9606 |
| hTNFRSF11B | hTNFRSF11B | ANA226 | 9606 |
| hTNFRSF12A | hTNFRSF12A | ANA1240 | 9606 |
| hTNFRSF13B | hTNFRSF13B | ANA227 | 9606 |
| hTNFRSF13C | hTNFRSF13C | ANA1222 | 9606 |
| hTNFRSF14 | hTNFRSF14 | ANA228 | 9606 |
| hTNFRSF17 | hTNFRSF17 | ANA229 | 9606 |
| hTNFRSF18 | hTNFRSF18 | ANA230 | 9606 |
| hTNFRSF1A | hTNFRSF1A | ANA231 | 9606 |
| hTNFRSF1B | hTNFRSF1B | ANA232 | 9606 |
| hTNFRSF25 | hTNFRSF25 | ANA233 | 9606 |
| hTNFRSF4 | hTNFRSF4 | ANA234 | 9606 |
| hTNFRSF8 | hTNFRSF8 | ANA235 | 9606 |
| hTNFRSF9 | hTNFRSF9 | ANA236 | 9606 |
| hTNFSF10 | hTNFSF10 | ANA237 | 9606 |
| hTNFSF11 | hTNFSF11 | ANA238 | 9606 |
| hTNFSF12 | hTNFSF12 | ANA239 | 9606 |
| hTNFSF13 | hTNFSF13 | ANA240 | 9606 |
| hTNFSF13B | hTNFSF13B | ANA241 | 9606 |
| hTNFSF14 | hTNFSF14 | ANA242 | 9606 |
| hTNFSF15 | hTNFSF15 | ANA243 | 9606 |
| hTNFSF18 | hTNFSF18 | ANA244 | 9606 |
| hTNFSF4 | hTNFSF4 | ANA245 | 9606 |
| hTNFSF8 | hTNFSF8 | ANA246 | 9606 |
| hTNFSF9 | hTNFSF9 | ANA247 | 9606 |
| hTSPAN7 | hTSPAN7 | ANA1113 | 9606 |
| hVEGFD | hVEGFD | ANA710 | 9606 |
| hVPREB1 | hVPREB1 | ANA1017 | 9606 |
| hXCL1 | hXCL1 | ANA248 | 9606 |
| hXCL2 | hXCL2 | ANA249 | 9606 |
| hXCR1 | hXCR1 | ANA250 | 9606 |
| human IFN-gamma | hIFNG | ANA110 | 9606 |
| ifna | fam:hIFNA | ANA717 | 9606 |
| ifna2 | hIFNA2 | ANA99 | 9606 |
| ifnb | hIFNB1 | ANA108 | 9606 |
| ifng | hIFNG | ANA110 | 9606 |
| il10 | hIL10 | ANA118 | 9606 |
| il12p40 | hIL12B | ANA124 | 9606 |
| il12p70 | hIL12 | ANA800 | 9606 |
| il13 | hIL13 | ANA127 | 9606 |
| il18 | hIL18 | ANA139 | 9606 |
| il18r1 | mIL18R1 | ANA698 | 10090 |
| il1b | hIL1B | ANA143 | 9606 |
| il2 | hIL2 | ANA148 | 9606 |
| il4 | hIL4 | ANA174 | 9606 |
| il6 | hIL6 | ANA178 | 9606 |
| il8 | hCXCL8 | ANA72 | 9606 |
| ip10 | hCXCL10 | ANA61 | 9606 |
| ki67 | hMKI67 | ANA889 | 9606 |
| mACKR3 | mACKR3 | ANA475 | 10090 |
| mBCL2 | mBCL2 | ANA1005 | 10090 |
| mBCL6 | mBCL6 | ANA1110 | 10090 |
| mCCL1 | mCCL1 | ANA476 | 10090 |
| mCCL11 | mCCL11 | ANA477 | 10090 |
| mCCL2 | mCCL2 | ANA480 | 10090 |
| mCCL20 | mCCL20 | ANA481 | 10090 |
| mCCL22 | mCCL22 | ANA483 | 10090 |
| mCCL24 | mCCL24 | ANA484 | 10090 |
| mCCL27 | mCCL27 | ANA487 | 10090 |
| mCCL3 | mCCL3 | ANA488 | 10090 |
| mCCL4 | mCCL4 | ANA489 | 10090 |
| mCCL5 | mCCL5 | ANA490 | 10090 |
| mCCL7 | mCCL7 | ANA491 | 10090 |
| mCCR1 | mCCR1 | ANA493 | 10090 |
| mCCR10 | mCCR10 | ANA494 | 10090 |
| mCCR2 | mCCR2 | ANA495 | 10090 |
| mCCR3 | mCCR3 | ANA496 | 10090 |
| mCCR4 | mCCR4 | ANA497 | 10090 |
| mCCR5 | mCCR5 | ANA498 | 10090 |
| mCCR6 | mCCR6 | ANA499 | 10090 |
| mCCR7 | mCCR7 | ANA500 | 10090 |
| mCCR8 | mCCR8 | ANA501 | 10090 |
| mCCR9 | mCCR9 | ANA502 | 10090 |
| mCD101 | mCD101 | ANA942 | 10090 |
| mCD109 | mCD109 | ANA1207 | 10090 |
| mCD14 | mCD14 | ANA1006 | 10090 |
| mCD151 | mCD151 | ANA953 | 10090 |
| mCD160 | mCD160 | ANA970 | 10090 |
| mCD163 | mCD163 | ANA1164 | 10090 |
| mCD164 | mCD164 | ANA1250 | 10090 |
| mCD164L2 | mCD164L2 | ANA1229 | 10090 |
| mCD180 | mCD180 | ANA1176 | 10090 |
| mCD19 | mCD19 | ANA1078 | 10090 |
| mCD1D | mCD1D | ANA1011 | 10090 |
| mCD2 | mCD2 | ANA1000 | 10090 |
| mCD200 | mCD200 | ANA956 | 10090 |
| mCD200R1L | mCD200R1L | ANA1187 | 10090 |
| mCD207 | mCD207 | ANA1208 | 10090 |
| mCD22 | mCD22 | ANA1097 | 10090 |
| mCD226 | mCD226 | ANA1198 | 10090 |
| mCD24 | mCD24 | ANA1077 | 10090 |
| mCD244 | mCD244 | ANA1143 | 10090 |
| mCD247 | mCD247 | ANA1076 | 10090 |
| mCD248 | mCD248 | ANA1212 | 10090 |
| mCD27 | mCD27 | ANA503 | 10090 |
| mCD274 | mCD274 | ANA1231 | 10090 |
| mCD276 | mCD276 | ANA1210 | 10090 |
| mCD28 | mCD28 | ANA1086 | 10090 |
| mCD2AP | mCD2AP | ANA1239 | 10090 |
| mCD2BP2 | mCD2BP2 | ANA1228 | 10090 |
| mCD300A | mCD300A | ANA1183 | 10090 |
| mCD300C | mCD300C | ANA940 | 10090 |
| mCD300E | mCD300E | ANA1197 | 10090 |
| mCD300LB | mCD300LB | ANA1166 | 10090 |
| mCD300LF | mCD300LF | ANA1185 | 10090 |
| mCD302 | mCD302 | ANA1230 | 10090 |
| mCD320 | mCD320 | ANA1266 | 10090 |
| mCD33 | mCD33 | ANA1177 | 10090 |
| mCD34 | mCD34 | ANA1178 | 10090 |
| mCD36 | mCD36 | ANA1148 | 10090 |
| mCD37 | mCD37 | ANA1172 | 10090 |
| mCD38 | mCD38 | ANA1125 | 10090 |
| mCD3D | mCD3D | ANA980 | 10090 |
| mCD3E | mCD3E | ANA1071 | 10090 |
| mCD3EAP | mCD3EAP | ANA1189 | 10090 |
| mCD3G | mCD3G | ANA1016 | 10090 |
| mCD4 | mCD4 | ANA504 | 10090 |
| mCD40 | mCD40 | ANA505 | 10090 |
| mCD40LG | mCD40LG | ANA506 | 10090 |
| mCD44 | mCD44 | ANA1035 | 10090 |
| mCD46 | mCD46 | ANA968 | 10090 |
| mCD47 | mCD47 | ANA1175 | 10090 |
| mCD48 | mCD48 | ANA1052 | 10090 |
| mCD5 | mCD5 | ANA1023 | 10090 |
| mCD52 | mCD52 | ANA1179 | 10090 |
| mCD53 | mCD53 | ANA1171 | 10090 |
| mCD5L | mCD5L | ANA1249 | 10090 |
| mCD6 | mCD6 | ANA1170 | 10090 |
| mCD63 | mCD63 | ANA1112 | 10090 |
| mCD68 | mCD68 | ANA1090 | 10090 |
| mCD69 | mCD69 | ANA1102 | 10090 |
| mCD7 | mCD7 | ANA1121 | 10090 |
| mCD70 | mCD70 | ANA507 | 10090 |
| mCD72 | mCD72 | ANA1067 | 10090 |
| mCD74 | mCD74 | ANA981 | 10090 |
| mCD79A | mCD79A | ANA1014 | 10090 |
| mCD79B | mCD79B | ANA1037 | 10090 |
| mCD80 | mCD80 | ANA1135 | 10090 |
| mCD81 | mCD81 | ANA1099 | 10090 |
| mCD82 | mCD82 | ANA1107 | 10090 |
| mCD83 | mCD83 | ANA969 | 10090 |
| mCD84 | mCD84 | ANA1162 | 10090 |
| mCD86 | mCD86 | ANA1114 | 10090 |
| mCD8A | mCD8A | ANA974 | 10090 |
| mCD8B | mCD8B | ANA1004 | 10090 |
| mCD9 | mCD9 | ANA1108 | 10090 |
| mCD93 | mCD93 | ANA971 | 10090 |
| mCD96 | mCD96 | ANA1165 | 10090 |
| mCD99L2 | mCD99L2 | ANA1193 | 10090 |
| mCKLF | mCKLF | ANA508 | 10090 |
| mCLCF1 | mCLCF1 | ANA509 | 10090 |
| mCMTM6 | mCMTM6 | ANA511 | 10090 |
| mCMTM7 | mCMTM7 | ANA512 | 10090 |
| mCNMD | mCNMD | ANA641 | 10090 |
| mCNTFR | mCNTFR | ANA513 | 10090 |
| mCSF1 | mCSF1 | ANA514 | 10090 |
| mCSF1R | mCSF1R | ANA515 | 10090 |
| mCSF2 | mCSF2 | ANA516 | 10090 |
| mCSF2RA | mCSF2RA | ANA517 | 10090 |
| mCSF3 | mCSF3 | ANA519 | 10090 |
| mCSF3R | mCSF3R | ANA520 | 10090 |
| mCX3CL1 | mCX3CL1 | ANA521 | 10090 |
| mCX3CR1 | mCX3CR1 | ANA522 | 10090 |
| mCXCL1 | mCXCL1 | ANA523 | 10090 |
| mCXCL10 | mCXCL10 | ANA524 | 10090 |
| mCXCL12 | mCXCL12 | ANA526 | 10090 |
| mCXCL13 | mCXCL13 | ANA527 | 10090 |
| mCXCL14 | mCXCL14 | ANA528 | 10090 |
| mCXCL16 | mCXCL16 | ANA529 | 10090 |
| mCXCL17 | mCXCL17 | ANA530 | 10090 |
| mCXCL5 | mCXCL5 | ANA533 | 10090 |
| mCXCL9 | mCXCL9 | ANA534 | 10090 |
| mCXCR2 | mCXCR2 | ANA536 | 10090 |
| mCXCR3 | mCXCR3 | ANA537 | 10090 |
| mCXCR4 | mCXCR4 | ANA538 | 10090 |
| mCXCR5 | mCXCR5 | ANA539 | 10090 |
| mCXCR6 | mCXCR6 | ANA540 | 10090 |
| mCcl19 | mCcl19 | ANA479 | 10090 |
| mCcl21a | mCcl21a | ANA482 | 10090 |
| mCcl25 | mCcl25 | ANA485 | 10090 |
| mCcl8 | mCcl8 | ANA492 | 10090 |
| mCd177 | mCd177 | ANA1206 | 10090 |
| mCd1d2 | mCd1d2 | ANA1012 | 10090 |
| mCd200r1 | mCd200r1 | ANA1232 | 10090 |
| mCd200r3 | mCd200r3 | ANA1168 | 10090 |
| mCd200r4 | mCd200r4 | ANA1186 | 10090 |
| mCd209a | mCd209a | ANA1216 | 10090 |
| mCd209b | mCd209b | ANA1194 | 10090 |
| mCd209c | mCd209c | ANA1215 | 10090 |
| mCd209d | mCd209d | ANA1214 | 10090 |
| mCd209e | mCd209e | ANA1213 | 10090 |
| mCd300lg | mCd300lg | ANA1163 | 10090 |
| mCd55 | mCd55 | ANA1173 | 10090 |
| mCd55b | mCd55b | ANA1174 | 10090 |
| mCd59a | mCd59a | ANA957 | 10090 |
| mCd59b | mCd59b | ANA1127 | 10090 |
| mClm | mClm | ANA1190 | 10090 |
| mClm3 | mClm3 | ANA1184 | 10090 |
| mClm5 | mClm5 | ANA1209 | 10090 |
| mCsf2rb | mCsf2rb | ANA518 | 10090 |
| mCxcl11 | mCxcl11 | ANA525 | 10090 |
| mCxcl2 | mCxcl2 | ANA531 | 10090 |
| mCxcl3 | mCxcl3 | ANA532 | 10090 |
| mCxcr1 | mCxcr1 | ANA535 | 10090 |
| mEBI3 | mEBI3 | ANA541 | 10090 |
| mEGF | mEGF | ANA542 | 10090 |
| mEGFR | mEGFR | ANA543 | 10090 |
| mEPO | mEPO | ANA544 | 10090 |
| mEPOR | mEPOR | ANA545 | 10090 |
| mFAS | mFAS | ANA546 | 10090 |
| mFASLG | mFASLG | ANA547 | 10090 |
| mFGF1 | mFGF1 | ANA548 | 10090 |
| mFGF2 | mFGF2 | ANA549 | 10090 |
| mFLT3 | mFLT3 | ANA550 | 10090 |
| mFLT3LG | mFLT3LG | ANA551 | 10090 |
| mGDF15 | mGDF15 | ANA552 | 10090 |
| mHGF | mHGF | ANA553 | 10090 |
| mIFNAR1 | mIFNAR1 | ANA565 | 10090 |
| mIFNAR2 | mIFNAR2 | ANA566 | 10090 |
| mIFNB1 | mIFNB1 | ANA567 | 10090 |
| mIFNE | mIFNE | ANA568 | 10090 |
| mIFNG | mIFNG | ANA569 | 10090 |
| mIFNGR1 | mIFNGR1 | ANA570 | 10090 |
| mIFNK | mIFNK | ANA572 | 10090 |
| mIFNLR1 | mIFNLR1 | ANA575 | 10090 |
| mIL10 | mIL10 | ANA576 | 10090 |
| mIL10RA | mIL10RA | ANA577 | 10090 |
| mIL10RB | mIL10RB | ANA578 | 10090 |
| mIL11 | mIL11 | ANA579 | 10090 |
| mIL12A | mIL12A | ANA581 | 10090 |
| mIL12B | mIL12B | ANA582 | 10090 |
| mIL12RB1 | mIL12RB1 | ANA583 | 10090 |
| mIL12RB2 | mIL12RB2 | ANA584 | 10090 |
| mIL13 | mIL13 | ANA585 | 10090 |
| mIL13RA1 | mIL13RA1 | ANA586 | 10090 |
| mIL13RA2 | mIL13RA2 | ANA587 | 10090 |
| mIL15 | mIL15 | ANA588 | 10090 |
| mIL15RA | mIL15RA | ANA589 | 10090 |
| mIL16 | mIL16 | ANA590 | 10090 |
| mIL17A | mIL17A | ANA591 | 10090 |
| mIL17B | mIL17B | ANA592 | 10090 |
| mIL17C | mIL17C | ANA593 | 10090 |
| mIL17F | mIL17F | ANA595 | 10090 |
| mIL17RA | mIL17RA | ANA596 | 10090 |
| mIL18 | mIL18 | ANA597 | 10090 |
| mIL18R1 | mIL18R1 | ANA698 | 10090 |
| mIL19 | mIL19 | ANA598 | 10090 |
| mIL1A | mIL1A | ANA599 | 10090 |
| mIL1B | mIL1B | ANA600 | 10090 |
| mIL1F10 | mIL1F10 | ANA601 | 10090 |
| mIL1R1 | mIL1R1 | ANA603 | 10090 |
| mIL1R2 | mIL1R2 | ANA604 | 10090 |
| mIL1RN | mIL1RN | ANA605 | 10090 |
| mIL2 | mIL2 | ANA606 | 10090 |
| mIL20 | mIL20 | ANA607 | 10090 |
| mIL20RA | mIL20RA | ANA608 | 10090 |
| mIL21 | mIL21 | ANA610 | 10090 |
| mIL21R | mIL21R | ANA611 | 10090 |
| mIL22RA1 | mIL22RA1 | ANA613 | 10090 |
| mIL22RA2 | mIL22RA2 | ANA614 | 10090 |
| mIL23A | mIL23A | ANA615 | 10090 |
| mIL23R | mIL23R | ANA616 | 10090 |
| mIL24 | mIL24 | ANA617 | 10090 |
| mIL27 | mIL27 | ANA619 | 10090 |
| mIL2RA | mIL2RA | ANA620 | 10090 |
| mIL2RB | mIL2RB | ANA621 | 10090 |
| mIL2RG | mIL2RG | ANA622 | 10090 |
| mIL3 | mIL3 | ANA623 | 10090 |
| mIL31 | mIL31 | ANA624 | 10090 |
| mIL33 | mIL33 | ANA625 | 10090 |
| mIL34 | mIL34 | ANA626 | 10090 |
| mIL36RN | mIL36RN | ANA602 | 10090 |
| mIL3RA | mIL3RA | ANA627 | 10090 |
| mIL4 | mIL4 | ANA628 | 10090 |
| mIL4R | mIL4R | ANA629 | 10090 |
| mIL5 | mIL5 | ANA630 | 10090 |
| mIL5RA | mIL5RA | ANA631 | 10090 |
| mIL6 | mIL6 | ANA632 | 10090 |
| mIL6R | mIL6R | ANA633 | 10090 |
| mIL6ST | mIL6ST | ANA634 | 10090 |
| mIL7 | mIL7 | ANA635 | 10090 |
| mIL7R | mIL7R | ANA636 | 10090 |
| mIL9 | mIL9 | ANA637 | 10090 |
| mIL9R | mIL9R | ANA638 | 10090 |
| mITGAL | mITGAL | ANA1074 | 10090 |
| mIfna1 | mIfna1 | ANA554 | 10090 |
| mIfna13 | mIfna13 | ANA556 | 10090 |
| mIfna2 | mIfna2 | ANA559 | 10090 |
| mIfna4 | mIfna4 | ANA560 | 10090 |
| mIfna5 | mIfna5 | ANA561 | 10090 |
| mIfna6 | mIfna6 | ANA562 | 10090 |
| mIfna7 | mIfna7 | ANA563 | 10090 |
| mIfnl2 | mIfnl2 | ANA573 | 10090 |
| mIfnl3 | mIfnl3 | ANA574 | 10090 |
| mIl11ra1 | mIl11ra1 | ANA580 | 10090 |
| mIl22 | mIl22 | ANA612 | 10090 |
| mKIT | mKIT | ANA639 | 10090 |
| mKITLG | mKITLG | ANA640 | 10090 |
| mKir3dl1 | mKir3dl1 | ANA1134 | 10090 |
| mLECT2 | mLECT2 | ANA642 | 10090 |
| mLIF | mLIF | ANA643 | 10090 |
| mLIFR | mLIFR | ANA644 | 10090 |
| mLTA | mLTA | ANA645 | 10090 |
| mLTB | mLTB | ANA646 | 10090 |
| mLTBR | mLTBR | ANA647 | 10090 |
| mMET | mMET | ANA648 | 10090 |
| mMIF | mMIF | ANA649 | 10090 |
| mMPL | mMPL | ANA650 | 10090 |
| mMST1 | mMST1 | ANA651 | 10090 |
| mMST1R | mMST1R | ANA652 | 10090 |
| mMYDGF | mMYDGF | ANA618 | 10090 |
| mNECTIN1 | mNECTIN1 | ANA1237 | 10090 |
| mNECTIN2 | mNECTIN2 | ANA1093 | 10090 |
| mNECTIN3 | mNECTIN3 | ANA1238 | 10090 |
| mOSM | mOSM | ANA653 | 10090 |
| mOSMR | mOSMR | ANA654 | 10090 |
| mPDGFA | mPDGFA | ANA655 | 10090 |
| mPDGFB | mPDGFB | ANA656 | 10090 |
| mPDGFRA | mPDGFRA | ANA657 | 10090 |
| mPDGFRB | mPDGFRB | ANA658 | 10090 |
| mPF4 | mPF4 | ANA659 | 10090 |
| mRETN | mRETN | ANA661 | 10090 |
| mSPP1 | mSPP1 | ANA662 | 10090 |
| mTGFB1 | mTGFB1 | ANA664 | 10090 |
| mTGFB2 | mTGFB2 | ANA665 | 10090 |
| mTGFB3 | mTGFB3 | ANA666 | 10090 |
| mTGFBR1 | mTGFBR1 | ANA667 | 10090 |
| mTGFBR2 | mTGFBR2 | ANA668 | 10090 |
| mTGFBR3 | mTGFBR3 | ANA669 | 10090 |
| mTHPO | mTHPO | ANA670 | 10090 |
| mTNF | mTNF | ANA671 | 10090 |
| mTNFRSF11A | mTNFRSF11A | ANA673 | 10090 |
| mTNFRSF11B | mTNFRSF11B | ANA674 | 10090 |
| mTNFRSF13B | mTNFRSF13B | ANA675 | 10090 |
| mTNFRSF14 | mTNFRSF14 | ANA676 | 10090 |
| mTNFRSF17 | mTNFRSF17 | ANA677 | 10090 |
| mTNFRSF1A | mTNFRSF1A | ANA679 | 10090 |
| mTNFRSF1B | mTNFRSF1B | ANA680 | 10090 |
| mTNFRSF4 | mTNFRSF4 | ANA682 | 10090 |
| mTNFRSF8 | mTNFRSF8 | ANA683 | 10090 |
| mTNFRSF9 | mTNFRSF9 | ANA684 | 10090 |
| mTNFSF10 | mTNFSF10 | ANA685 | 10090 |
| mTNFSF11 | mTNFSF11 | ANA686 | 10090 |
| mTNFSF12 | mTNFSF12 | ANA687 | 10090 |
| mTNFSF13 | mTNFSF13 | ANA688 | 10090 |
| mTNFSF13B | mTNFSF13B | ANA689 | 10090 |
| mTNFSF14 | mTNFSF14 | ANA690 | 10090 |
| mTNFSF15 | mTNFSF15 | ANA691 | 10090 |
| mTNFSF18 | mTNFSF18 | ANA692 | 10090 |
| mTNFSF4 | mTNFSF4 | ANA693 | 10090 |
| mTNFSF8 | mTNFSF8 | ANA694 | 10090 |
| mTNFSF9 | mTNFSF9 | ANA695 | 10090 |
| mTnfrsf10b | mTnfrsf10b | ANA672 | 10090 |
| mTnfrsf18 | mTnfrsf18 | ANA678 | 10090 |
| mXCL1 | mXCL1 | ANA696 | 10090 |
| mXCR1 | mXCR1 | ANA697 | 10090 |
| mip1a | hCCL4 | ANA24 | 9606 |
| mip1b | hCCL4 | ANA24 | 9606 |
| nCD19 | hCD19 | ANA805 | 9606 |
| pSTAT-1 | hSTAT1/iso:1/Phos:1 | ANA907 | 9606 |
| pSTAT-3 | hSTAT3/Phos:1 | ANA908 | 9606 |
| pSTAT-5 | hSTAT5A | ANA901 | 9606 |
| pSTAT1 | hSTAT1/iso:1/Phos:1 | ANA907 | 9606 |
| pSTAT3 | hSTAT3/Phos:1 | ANA908 | 9606 |
| pSTAT5 | hSTAT5A | ANA901 | 9606 |
| s IL2-RA | hIL2RA | ANA163 | 9606 |
| sCD40L | hCD40LG | ANA43 | 9606 |
| sFAS ligand | hFASLG | ANA86 | 9606 |
| sVEGF | VEGFA | ANA709 | 9606 |
| tnfa | hTNF | ANA220 | 9606 |

# Appendix B Non-Analyte Markers

The following table defines all the reported non-analyte markers that have have
corresponding preferred non-analyte markers and analyte accession values.  This
table is derived from lk_cell_population_marker (name), and
lk_cell_pop_pref_mapping (marker_reported) tables. Non-analyte markers apply to
all species equally.

| Analyte Reported | Analyte Preferred | Analyte Accession | Taxonomy ID |
| -----------------|-------------------|-------------------|-------------------|
| 2-WBC | leukocyte |  |  |
| 2-grans | granulocyte |  |  |
| 2-mono | monocyte |  |  |
| Annexin negative | viable |  |  |
| Annexin- | viable |  |  |
| CFSE- | proliferated |  |  |
| Dead | dead |  |  |
| Intact cells | intact |  |  |
| Intact singlets | singlet |  |  |
| Intact_cells | intact |  |  |
| Intact_cells_population | intact |  |  |
| Intact_singlets | singlet |  |  |
| Leukocyte | leukocyte |  |  |
| Live cells | viable |  |  |
| Live/Dead | viable |  |  |
| Live/dead | viable |  |  |
| LiveDead | viable |  |  |
| Live_cells | viable |  |  |
| Live_dead | viable |  |  |
| Lv | viable |  |  |
| Lymo | lymphocyte |  |  |
| Lymp | lymphocyte |  |  |
| Lymph | lymphocyte |  |  |
| Lymphocytes | lymphocyte |  |  |
| Lymphs | lymphocyte |  |  |
| MNC | monocyte |  |  |
| Mono | monocyte |  |  |
| Monocytes | monocyte |  |  |
| SSC | SSC |  |  |
| Singlet | singlet |  |  |
| Singlets | singlet |  |  |
| TracerViolet- | proliferated |  |  |
| Viable | viable |  |  |
| Viable Gate | viable |  |  |
| Viable_Gate | viable |  |  |
| Viable_gate | viable |  |  |
| WBC | leukocyte |  |  |
| dead | dead |  |  |
| doublet_excluded | singlet |  |  |
| gran | granulocyte |  |  |
| granulocyte | granulocyte |  |  |
| granulocytes | granulocyte |  |  |
| intact | intact |  |  |
| intact singlets | singlet |  |  |
| intact_singlet | singlet |  |  |
| intact_singlets | singlet |  |  |
| leukocyte | leukocyte |  |  |
| live | viable |  |  |
| live/Dead | viable |  |  |
| live/dead | viable |  |  |
| live/dead stain-? | viable |  |  |
| ly | lymphocyte |  |  |
| lymo | lymphocyte |  |  |
| lymono | lymphocyte |  |  |
| lymp | lymphocyte |  |  |
| lymph | lymphocyte |  |  |
| lymphocyte | lymphocyte |  |  |
| lymphocytes | lymphocyte |  |  |
| mo | monocyte |  |  |
| mo2 | monocyte |  |  |
| mo3 | monocyte |  |  |
| mono | monocyte |  |  |
| monocyte | monocyte |  |  |
| monocytes | monocyte |  |  |
| monos | monocyte |  |  |
| proliferated | proliferated |  |  |
| sWBC | leukocyte |  |  |
| sing | singlet |  |  |
| sing-F | singlet |  |  |
| singlet | singlet |  |  |
| singlets | singlet |  |  |
| small_lymphocyte | lymphocyte |  |  |
| viable | viable |  |  |
| viable singlets | singlet |  |  |
| viable_singlets | singlet |  |  |

# Appendix C Species Mapping

The following table defines how other species are mapped to human (9606) or
mouse (10090) group for determining preferred analytes.

| Name | Common Name | Taxonomy Id | Group Taxonomy ID |
| -----------------|-------------------|-------------------|-------------------|
| Mus musculus | Mouse | 10090 | 10090 |
| Mus musculus castaneus | Southeastern Asian house mouse | 10091 | 10090 |
| Mus spretus | Western wild mouse | 10096 | 10090 |
| Aotus nancymaae | Ma's night monkey | 37293 | 9606 |
| Macaca fascicularis | Macaca fascicularis | 9541 | 9606 |
| Macaca mulatta | Rhesus macaque | 9544 | 9606 |
| Pan troglodytes | Chimpanzee | 9598 | 9606 |
| Homo sapiens | Human | 9606 | 9606 |
