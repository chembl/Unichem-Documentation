# Analysis

#### Introduction.

A number of pages in UniChem are dedicated to various analyses of UniChem data. The analyses include the calculation of the numbers of structures assigned to the separate sources, how many of these overlap, and how many are unique. These analyses, and others, may be straightforwardly generated using the data provided in the UniChem data downloads.

#### A Note of Caution.

 When loading data from a particular source, UniChem makes no attempt to filter out structures with a provenance other than the source being loaded. The reasons for this have been explored previously in citation 1, [here](https://www.ebi.ac.uk/unichem/info/citation). Now, because many of the sources in UniChem have exchanged their own structures with other sources in UniChem, the 'overlaps' and 'uniques' calculated here cannot reflect the true values which would be observed if no such cross-integration had taken place.

 Thus, for example, ChEMBL data has been integrated into PubChem. This results in a very large apparent overlap of structures between the two sources, and obscures the degree of uniqueness of many ChEMBL structures.

 The analyses shown here should therefore only be treated as an analysis of the data as it has been integrated into UniChem, and should not be considered a bone fide cross-source comparison of the sources themselves, or a means of evaluating the relative value or quality of a source. It is important to understand this proviso before viewing the numbers on these pages.

#### Types of Analyses.

 Analyses are displayed in a number of separate pages, as described below...

 A ['Release'](https://www.ebi.ac.uk/unichem/ucquery/stats) page shows the current release number, and a high level view of the current content, including the total number of InChIKeys and Assignments.

 A ['Uniques'](https://www.ebi.ac.uk/unichem/analysis/unique) page shows a breakdown of the numbers of structures from each individual source, and the numbers that are unique.

 Three separate pages also exist for describing 'Overlaps' between the sources. These are called [FULIK](https://www.ebi.ac.uk/unichem/analysis/heatoverFullInchi), [FIKHB](https://www.ebi.ac.uk/unichem/analysis/heatoverConnectivity), and [SCFIB](https://www.ebi.ac.uk/unichem/analysis/heatoverConnectSing). These three separate pages are required for the reasons described below.

#### Definitions of 'Structural Identity'.

 The calculated numbers in these analyses vary depending upon the definition of structural identity used. Three different criteria of structural identity used in UniChem, and for brevity they are called FULIK, FIKHB and SCFIB. These are defined as follows...  
  
 FULIK = The Full InChIKey. Two molecules are considered identical if there is a complete match of the full InChiKey.  
 FIKHB = First InChIKey Hash Block. Two molecules are considered identical if there is a complete match of the First InChIKey Hash block \(commonly called 'the connectivity layer' of the InChIKey\).  
 SCFIB = Separated Single Components of FIKHB. This definition is the same as FIKHB, except that prior to carrying out matching all structures within UniChem which are mixtures \(or salts\) are parsed into their separate single components, and then the FIKHBs calculated for these separated molecules.  
  
 Many of the analyses have been carried out for all three of these structural definitions \(and a separate page for each is given for the 'Overlaps' analyses\), However, the data shown on the 'Top Level Stats' page is calculated using FULIK only.  
  


