# FAQs

## **Unichem Contents**

**What sort of sources are used in UniChem ?**

* Any chemically aware database that contains compounds which have been assigned ids \(named as src\_compound\_ids in UniChem\) and structures. A source may store structures in a variety of ways. 
* If standard InChIs are provided by the source, then these are used by UniChem. 
* However, if a source does not provide standard InChIs, UniChem will produce these during loading of the data. 
* There need not be a 1:1 relationship between src\_compound\_id's and InChIs in a source. Many sources define chemical uniqueness by other means than the standard InChI. UniChem will handle 1:many and many:1 relationships between src\_compound\_ids and standard InChIs.

 **What sources are currently used in UniChem ?**  
 These are listed on the 'Sources' page...  
 Go [here](https://www.ebi.ac.uk/unichem/ucquery/listSources)  
  
 **How many structures are there in UniChem ?**  
 These are shown on the 'Stats' page...  
 Go [here](https://www.ebi.ac.uk/unichem/ucquery/stats)  
  
 **Some src\_compound\_ids are missing from a source in UniChem. Why is this ?**  
 This is explained on the 'Rules for Loading' page...  
 Go [here](https://www.ebi.ac.uk/unichem/info/rulesforloading)

**The source I am trying to create hyperlinks to does not use the src\_compound\_id to create the URL for compound-specific pages. How does UniChem deal with this ?**  
 In these circumstances, UniChem makes use of 'auxiliary data' to create links, as described immediately below.  
  
**What is 'auxiliary data' for a src\_compound\_id and when would I need to use it ?**

* Most sources within UniChem create URLs for compound specific pages by simply appending a src\_compound\_id to a ‘base URL’ \(eg: appending 'CHEMBL59' to 'https://www.ebi.ac.uk/chembldb/compound/inspect/' gives: https://www.ebi.ac.uk/chembldb/compound/inspect/CHEMBL59\). 
* However, in some instances of UniChem a small number of sources exist which create URLs for compound-specific pages by using strings or identifiers \('auxiliary data'\) that are different to the src\_compound\_ids for the source. This is not very common, but is dealt with in UniChem by use of an additional mapping step for these sources, where the src\_compound\_ids are mapped to the 'auxiliary data'. 
* Sources where this step is necesary are marked up with a '1' in the 'AUX\_FOR\_URL' field of the UC\_SOURCES table. 
* This can be seen in the drill-down page for each individual source, and is also shown in the output of two web-service methods: 'Get Source Information' and 'Get verbose src\_compound\_ids from InChIKey'. Note that for these sources, Auxiliary data is only held for src\_compound\_ids that have current assignments: auxiliary data for assignments that become obsolete are deleted, and the field holding these data set to null.

**Some src\_compound\_ids from some sources do not appear to have standard InChIs. Why is this ?**

* Some sources in UniChem do not provide standard InChIs, only standard InChIKeys. These sources are marked with a '1' in the 'keys\_only' field on the sources drilldown page. 
* UniChem deals with the data from these sources in a slightly different way to normal. 
* Firstly, InChIKeys which are unique to this source are included in the UC\_STRUCTURE table, and given a UCI, just like any other new InChIKey. However, the Standard InChI field remains null. 
* If, subsequently, another source provides a standard InChI for this Key, then the standard InChI field is populated.

**What does the 'private' flag mean on the sources drilldown pages ?**

* Sources in UniChem may be flagged as 'private' or 'public'. 
* Private sources and their corresponding data are not visible on the instance of UniChem available on the internet, but are visible within the firewall of the local network where UniChem is loaded. 
* The setting for this flag may be seen in the drill-down page for each source, in the 'private' field \(1=private, 0=public\)

**It looks like some data is replicated in multiple sources in UniChem, for example… ‘pubchem’, ‘pubchem\_tpharma’ and 'pubchem\_dotf’ all come from PubChem. Why is this ?**

* Some users wish to create hyperlinks to an entire data source, others to only sub-sets of data within a data sources. For this reason, some sources are maintained in UniChem as a separate source for the entire source, and others for sub-sets of the source.
* Some sources in UniChem, such as PubChem, have integrated structures from a wide variety of depositing primary sources. In the case of PubChem, the structures as originally deposited are assigned a different set of identifiers \(SIDs\) to the ‘integrated’ equivalent of the molecule \(which is assigned a ‘CID’\). SIDs therefore represents the original depositor-defined version of the structure, and the CID represents ‘PubChem’s’ normalized, integrated form of the molecule. 
* Sometimes these structures are different to one another, as the normalization process may change the structure. 
* In the case of PubChem, UniChem has included some sub-sets on the basis of the original depositor, and has therefore adopted the following policy: 
  * For the entire Pubchem data source CIDs are used. 
  * For depositor-defined sub-sets of PubChem, SIDs are used instead. 
* Please go [here](http://www.jcheminf.com/content/5/1/3) for a full discussion of provenance in relation to UniChem. 

## **Querying UniChem**

**How do I create mappings between similar compounds rather than just between identical compounds ?**  
 This is explained on the Documentation page for Connectivity Searching...  
 Go [here](https://www.ebi.ac.uk/unichem/info/widesearchInfo)

**Some queries from the home page return src\_compound\_ids which are not hyperlinked to the original source, why?**

* Some sources in UniChem do not have compound-specific pages which can be linked back to. In these cases, the main query interface simply gives the src\_compound\_id, with no hyperlink. 
* When using the web-services, and creating hyperlinks programmatically, it is useful to know that for web-service queries that return information on the source \(such as the two examples below\) the 'base\_id\_url\_available' field indicates whether such compound\_specific pages occur in the source or not \(1=yes, 0=no\). In this way, the sources for which hyperlinks should not be constructed may be easily filtered out.
* Example [https://www.ebi.ac.uk/unichem/info/webservices\#GetSourceInfo](https://www.ebi.ac.uk/unichem/info/webservices#GetSourceInfo)
* Example [https://www.ebi.ac.uk/unichem/info/webservices\#GetVerboseSrcCpdIdsFromInchiKey](https://www.ebi.ac.uk/unichem/info/webservices#GetVerboseSrcCpdIdsFromInchiKey)

  
  
  
  
  
  


