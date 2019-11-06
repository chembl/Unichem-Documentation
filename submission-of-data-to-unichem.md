# Submission of data to UniChem

UniChem seeks to integrate chemistry aware data sources \([more background](https://www.ebi.ac.uk/unichem/info/general)\).

 If you are in charge of a data source which you believe could be included into UniChem, then please [contact us](https://www.ebi.ac.uk/unichem/info/gettingintouch).

 The most important criteria for including a source is that the source itself should host a site that permits users to view compound-specific pages. In other words, each src\_comound\_id from the source should have its own web page where information relating to the compound can be viewed publicly. Also, the source should contain some useful information relating to the compound. Ideally, the source should be the primary provider, and not simply act as a aggregator of data from other sources. Lastly, the source must define the structures of the compounds, and make available regularly updated versions of the mappings between the src\_compound\_ids and the structures. The most convenient structural representation for UniChem is the Standard InChI, but other representations can be considered.

 There are many mechanisms by which a source's data can become integrated into UniChem. A simple example might be where a source provides a regularly updated file of src\_compound\_ids, Standard InChIs and Standard InChIKeys \(ideally as a 3 column tsv\) on an ftp site - UniChem will then automatically poll for new updates to this file, and then automatically upload these new data sets. However, other mechanisms are possible, which may better suit different resources.

