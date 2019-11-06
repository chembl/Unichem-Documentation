# Connectivity Search Documentation

 Background, rationale and discussion of Connectivity Searching is published here: [http://www.jcheminf.com/content/6/1/43](http://www.jcheminf.com/content/6/1/43)

 Here, full documentation on Connectivity Search is shown. Some of this information is not included in the above publication either because the detail may change over time, or the level of technical detail was not relevant for the Journal.  


####  Contents

  
   1 [Introduction](https://www.ebi.ac.uk/unichem/info/widesearchInfo#Introduction)  
   2 [Query Construction](https://www.ebi.ac.uk/unichem/info/widesearchInfo#QueryConstruction)  
   3 [Search Terms](https://www.ebi.ac.uk/unichem/info/widesearchInfo#SearchTerms)  
             3.1 [General](https://www.ebi.ac.uk/unichem/info/widesearchInfo#GeneralST)  
             3.2 ['key\_search' Search Terms](https://www.ebi.ac.uk/unichem/info/widesearchInfo#key_searchSearchTerms)  
             3.3 ['cpd\_search' Search Terms](https://www.ebi.ac.uk/unichem/info/widesearchInfo#cpd_searchSearchTerms)  
   4 [Search Criteria A-H](https://www.ebi.ac.uk/unichem/info/widesearchInfo#SearchCriteriaA-H)  
             4.1 [General](https://www.ebi.ac.uk/unichem/info/widesearchInfo#GeneralSC)  
             4.2 [A. Sources](https://www.ebi.ac.uk/unichem/info/widesearchInfo#critA)  
             4.3 [B. Pattern](https://www.ebi.ac.uk/unichem/info/widesearchInfo#critB)  
             4.4 [C. Component Mapping](https://www.ebi.ac.uk/unichem/info/widesearchInfo#critC)  
             4.5 [D. Frequency Block](https://www.ebi.ac.uk/unichem/info/widesearchInfo#critD)  
             4.6 [E. InChI Length Block](https://www.ebi.ac.uk/unichem/info/widesearchInfo#critE)  
             4.7 [F. UniChem Labels](https://www.ebi.ac.uk/unichem/info/widesearchInfo#critF)  
             4.8 [G. Assignment Status](https://www.ebi.ac.uk/unichem/info/widesearchInfo#critG)  
             4.9 [H. Data Structure](https://www.ebi.ac.uk/unichem/info/widesearchInfo#critH)  
   5 [Multiple Component InChIs.](https://www.ebi.ac.uk/unichem/info/widesearchInfo#MultipleComponentInChIs)  
   6 [Avoiding excessively large Result sets.](https://www.ebi.ac.uk/unichem/info/widesearchInfo#AvoidLargeResultSets)  
   7 [Multiply assigned src\_compound\_ids](https://www.ebi.ac.uk/unichem/info/widesearchInfo#MultiplyAssignedIds)  
   8 [Querying with InChIKeys that do not exist in UniChem](https://www.ebi.ac.uk/unichem/info/widesearchInfo#InChIKeysNoExist)  
   9 [Working within the constraints of Standard InChI](https://www.ebi.ac.uk/unichem/info/widesearchInfo#WorkingwithintheconstraintsofStandardInChI)  
  
  
  


#### Section 1  Introduction

[\(Back up to Contents\)](https://www.ebi.ac.uk/unichem/info/widesearchInfo#Contents)

 Under normal use, UniChem allows users to create links between structures and identifiers in different sources on the basis of complete identity between InChIKeys. However, the 'layered' structure of the InChI lends itself to also allow matching at different levels of structure specification. For a full description see the [IUPAC website.](http://www.iupac.org/home/publications/e-resources/inchi.html) UniChem can exploit this property of InChIs to discern relationships between molecules. Thus, stereochemical and isotopic variants of the same basic molecule can be identified, in both single and multiple component InChIs \(ie: mixtures and salts\).

 Finding related molecules in this way is achieved in UniChem using 'Connectivity Searching'. Connectivity Searching can be carried out using either the web-services or the ['Connectivity Search' web interface.](https://www.ebi.ac.uk/unichem/widesearch/widesearch). Two basic methods can be used for Connectivity Search: 'key\_search' or 'cpd\_search'. In the output from these methods \(identical for both\) UniChem compares and highlights differences between the InChI layers in the InChI represented by the Search term, and the InChIs retrieved from the database. The description is mainly focussed on the web services, as the web interface is more self explanatory. However, most of the details described here apply equally well to the use of the web-interface page, which is, in fact, simply a GUI front-end to the above two web-service methods. Thus, the Search terms, and Criteria \(A, B, etc\), are exactly the same in format and meaning between web-services and web-interface. In this regard, the web-interface can be very useful for learning how to use the web services. Indeed, the web-interface results page shows the 'equivalent web-services query' that could have been used to retrieve exactly the same data using the web-services. For more general information on web-services \(eg: content negotiation, error codes, etc\) visit the [Web Services page.](https://www.ebi.ac.uk/unichem/info/webservices). For more general information and background to Connectivity Search, visit the full publication cited at the top of this page.  
  
  


#### Section 2  Query Construction

[\(Back up to Contents\)](https://www.ebi.ac.uk/unichem/info/widesearchInfo#Contents)

 Connectivity Searching in UniChem uses two different methods: 'key\_search' and 'cpd\_search'. The two methods are similar in may ways. For example the Search Criteria \( [Search Criteria A-H](https://www.ebi.ac.uk/unichem/info/widesearchInfo#SearchCriteriaA-H) \) that are accepted by each are identical. In fact, the methods only differ in the kind of search term that each accepts: 'key\_search' accepts a Standard InChIKey \(or truncated form thereof\), and 'cpd\_search' accepts a src\_compound\_id/src\_id combination \(see [Search Terms](https://www.ebi.ac.uk/unichem/info/widesearchInfo#SearchTerms) below for more details on search terms\). In practice, the 'cpd\_search' method only differs from 'key\_search' in that prior to running the query, a smaller query first retrieves the currently assigned Std InChIKey for the 'src-compound\_id/src\_id', and then uses this to run a 'key\_search'.

 For web-service queries, method construction begins by appending the method name to the 'base' or 'stem' url, [as described for all other UniChem web servies](https://www.ebi.ac.uk/unichem/info/webservices), thus...

   https://www.ebi.ac.uk/unichem/rest/key\_search  
   https://www.ebi.ac.uk/unichem/rest/cpd\_search  


 Next, the Search term is appended. The Search Term is the only required argument for these methods. The exact format of the Search term required for each of the two methods is detailed in the next section. All additional arguments \(called search 'criteria'\) to the URL are optional. This basic query pattern may be refined and sophisticated by appending these additional optional search 'criteria' to the query URL, each of which 'qualify' or 'extend' the basic query in a particular kind of way \(see [Search Criteria A-H](https://www.ebi.ac.uk/unichem/info/widesearchInfo#SearchCriteriaA-H) below\). Currently, a total of 8 such optional qualifying criteria \(A-H\) can be defined, although criteria H is specific to web-services, and cannot be used on the web-interface. These criteria are appended, in strict alphabetical order, as additional path components of the URL, and are each defined with an integer. Thus the general case for a key\_search query is as follows...

   http/ ... rest/key\_search/StandardInChIKey/A/B/C/D/E/F/G/H

 And a specific example \(where all criteria are set to '0' except for C=4 and H=1\) would be...

   [https://www.ebi.ac.uk/unichem/rest/key\_search/QJVHTELASVOWBE-YBABNSIOSA-N/0/0/4/0/0/0/0/1](https://www.ebi.ac.uk/unichem/rest/key_search/QJVHTELASVOWBE-YBABNSIOSA-N/0/0/4/0/0/0/0/1)

 The structure of a 'cpd\_search' follows a very similar pattern, except that the Search Term must be a combination of a src\_compound\_id AND a src\_id \( [What are these ?](https://www.ebi.ac.uk/unichem/info/srcidExplain)\), since the src\_compound\_id on its own is not sufficient to unambiguously identify a compound identifier in UniChem. Thus, in the example below, the Search term has been specified as 'CHEMBL121/1', and Criterion A as '0', B as '0', C as '4', etc. . .

   [https://www.ebi.ac.uk/unichem/rest/cpd\_search/CHEMBL121/1/0/0/4/0/0/0/0/1](https://www.ebi.ac.uk/unichem/rest/cpd_search/CHEMBL121/1/0/0/4/0/0/0/0/1)

 ... note that the criteria for this query are set to exactly the same values as in the previous example.

 The default for each criteria is '0', Criteria must be set to '0' if subsequent criteria are defined as values other than the default. Thus, the two examples below are equivalent and permissable. In this example criteria A has been set to 1, C to 3, and all others left as the defaults \('0'\). Note that 'B' must be set to '0' \(in order for C to be unambiguously defined as '3' in this case\), but all other trailing '0's may be omitted.

   [https://www.ebi.ac.uk/unichem/rest/key\_search/QJVHTELASVOWBE-YBABNSIOSA-N/1/0/3/0/0/0/0/0](https://www.ebi.ac.uk/unichem/rest/key_search/QJVHTELASVOWBE-YBABNSIOSA-N/1/0/3/0/0/0/0/0)  
   [https://www.ebi.ac.uk/unichem/rest/key\_search/QJVHTELASVOWBE-YBABNSIOSA-N/1/0/3](https://www.ebi.ac.uk/unichem/rest/key_search/QJVHTELASVOWBE-YBABNSIOSA-N/1/0/3)  


 Thus if the user simply wishes to use all the default settings for the optional criteria, then none need to be specified in the URL. Thus the following two queries are identical \(and all criteria are set to '0'\)...

   [https://www.ebi.ac.uk/unichem/rest/cpd\_search/CHEMBL121/1/0/0/0/0/0/0/0/0](https://www.ebi.ac.uk/unichem/rest/cpd_search/CHEMBL121/1/0/0/0/0/0/0/0/0)  
   [https://www.ebi.ac.uk/unichem/rest/cpd\_search/CHEMBL121/1](https://www.ebi.ac.uk/unichem/rest/cpd_search/CHEMBL121/1)  


 In summary, if a user wishes to specify a later criteria \(for example F, G or H\) but use the defaults for earlier criteria \(eg: A, B, etc\), then the earlier criteria must be specified with a '0', so that their positions marked within the URL and the correct position in the URL is therefore defined for F, G and H.  
  
  


#### Section 3  Search Terms

[\(Back up to Contents\)](https://www.ebi.ac.uk/unichem/info/widesearchInfo#Contents)

  
**3.1  General**  


 The two Connectivity Search methods require different Search terms.  
**3.2  'key\_search' Search Terms**  


 The Search term for a 'key\_search' method may either be...

1. The full 27 character Standard InChiKey, or
2. The First InChIKey Hash Block \(FIKHB\), ie The first 14 character InChIKey block, sometimes called the InChIKey connectivity block or layer.

 Thus, the following two examples are both permissable...

   [https://www.ebi.ac.uk/unichem/rest/key\_search/QJVHTELASVOWBE-YBABNSIOSA-N/1/0/3](https://www.ebi.ac.uk/unichem/rest/key_search/QJVHTELASVOWBE-YBABNSIOSA-N/1/0/3)  
   [https://www.ebi.ac.uk/unichem/rest/key\_search/QJVHTELASVOWBE/1/0/3](https://www.ebi.ac.uk/unichem/rest/key_search/QJVHTELASVOWBE/1/0/3)  


 However, their meaning is quite different. The difference is NOT, as one might first suspect, that the first will search for matches to the entire Query InChI and the second for matches to any InChI with a common 'First InChIKey Hash Block' \('FIKHB'\). This 'scope' or 'pattern' of searching is defined instead by Criterion C \(see below\), and NOT by the query InChIKey itself. Rather, the difference between the two queries lies in the comparisons that are made between the 'Query InChI' and the InChIs retrieved from the search when it is completed. In the first case, the retrieved InChIs are compared to the InChI corresponding to the full InChIKey shown. In the second case, the retrieved InChIs are compared to the InChI corresponding to the query FIKHB with '-UHFFFAOYSA-N' appended \(ie: The second InChIKey hash block corresponding to no defined stereochemistry and no proton flag\).

 Thus the following two queries are identical...

   [https://www.ebi.ac.uk/unichem/rest/key\_search/QJVHTELASVOWBE/1/0/3](https://www.ebi.ac.uk/unichem/rest/key_search/QJVHTELASVOWBE/1/0/3)  
   [https://www.ebi.ac.uk/unichem/rest/key\_search/QJVHTELASVOWBE-UHFFFAOYSA-N/1/0/3](https://www.ebi.ac.uk/unichem/rest/key_search/QJVHTELASVOWBE-UHFFFAOYSA-N/1/0/3)  


 For a full understanding of the rationale behind this the reader is referred to [Avoiding excessively large Result sets.](https://www.ebi.ac.uk/unichem/info/widesearchInfo#AvoidLargeResultSets) below. Essentially though, this process is required since a full 'Query InChI' is always required for the InChI comparisons to be made in the connectivity searching output. Note that since there is always a 1:1 relationship between an InChIKey and an InChI, the query term for this method will only ever return a single Query InChI, if it exists in UniChem. Interestingly though, occassionally UniChem can proceed with a successful key\_search query even if the Search term does not exist in UniChem. The section explains this further.  
**3.3  'cpd\_search' Search Terms**  


 The Search term for a 'cpd\_search' must consist of two parts: The src\_compound\_id, and the src\_id for the source from where the src\_compound\_id originates. The src\_id is always an integer. If the Search Term is not currently assigned to a Standard InChIKey in UniChem then no data is returned \(and an error code 404 is given\). If more than one Std InChIKey is currently assigned to the specified Search Term then a separate query is run for each InChIKey and the data combined into one large data set, but with an 'Assignment Grouping Number' attached to each of the separate data sets. When this occurrs in the web-interface the user is warned. This is discussed in more detail in the section below.  
  
  


#### Section 4  Search Criteria A-H

[\(Back up to Contents\)](https://www.ebi.ac.uk/unichem/info/widesearchInfo#Contents)

  
**4.1  General**  


 The purpose of the optional search criteria \(A - H\) is to allow the user to qualify and refine the search. They are descibed in detail in the publication cited above.  
**4.2  A. Sources**  


 This criterion defines the src\_id to be searched against. All sources are searched if the default is used. If set to anything other than ‘0’, then only the src\_id corresponding to this value will be searched. Selecting a single source may provide a small performance advantage, especially if the source is small. Note that criterion A does not refer to the src\_id used as one of the two elements required for a valid cpd\_search search term, and which simply serves to unambiguously identify the source of the Query src\_compound\_id. Thus, it should be clear from this that is quite permissible to exclusively search one single source only, but using a src\_compound\_id from another source.  
**4.3  B. Pattern**  


 This criterion defines the pattern that is used to search UniChem.

* 0 = Match on FIKHB \(First InChIKey Hash Block, or 'Connectivity' block.\)
* 1 = Match on FIKHB and the second InChIKey hash block combined \(ie: The Full InChIKey minus the proton flag\).

 The default for this criterion is to retrieve all data which match on FIKHB. However, if this criterion is set to ‘1’, then only data which match on both the first and second InChIKey hash blocks combined is retrieved \(the proton flag is ignored\). Searching with a full InChIKey \(ie: including the proton flag\) is not provided. This is because for certain settings of criterion C the ‘p-layer’ of the InChI cannot be compared between Query and retrieved InChIs. The reasons for this are discussed in the section ‘Multiple Component InChIs’.  
**4.4  C. Component Mapping**  


 This criterion allows the user to set the component mapping relationship.

 Setting this criterion to '0' \(the default\) will result in UniChem searching for examples of where the Query InChI matches an existing InChI within UniChem. Other values for C will find different component relationships, as shown in the table below. If, however, the user simply wishes to retrieve all relations, then setting C to '4' will run all the queries '0' to '3'.  


| C | Component Mapping Relationship | Description |
| :--- | :--- | :--- |
| 0 | ...matches... | The Query InChI matches the InChI assigned to the src\_compound\_id |
| 1 | ...matches a component of... | The Query InChI matches a component of the InChI assigned to this src\_compound\_id. |
| 2 | ...has a component which matches... | A component of the Query InChI matches the InChI assigned to the src\_compound\_id |
| 3 | ...has a component which matches a component of... | A component of the Query InChI matches a component of the InChI assigned to src\_compound\_id |

 A number of potential complications can arise when using C set to something other than ‘0’. Thus, when querying with multiple component InChIs, some apparent redundancy may be appear in the result set. This is discussed in detail in the section ‘Multiple Component InChIs’. Also, using settings 1, 3 or 4 may occasionally result in the potential production of very large amounts of data, if the component being searched for is very common \(eg: ‘HCl’\). Search criteria D and E are designed to help to manage such large queries but this topic is also discussed in greater detail later in the section ‘Avoiding excessively large Result sets’.  
**4.5  D. Frequency Block**  


 This criterion is designed to prevent UniChem and the user from being overwhelmed by requests for excessively large, and usually unwanted, data sets. A full discussion of this is given later in the section ‘Avoiding excessively large Result sets’. But briefly, Criterion D will block sub-queries C1 and C3 for a given a single-component InChI on the basis of the frequency of occurrence of this single-component InChI in multiple component InChIs in UniChem. The default has been initially set at '200' and this may be defined by setting D to either '200' or '0, but may be specified by the user as any value between 1 and 500. Obviously, higher values for 'D' \(eg: &gt;200\) will, if they have an effect, produce larger results sets than the default, and smaller values \(&lt;200\) will tend to produce smaller data sets than the default. The upper limit of 500 cannot be overridden. The default \(200\) and the upper limit \(500\) were originally set at values which were considered to be optimal for the current size of UniChem. However, these values \(but not their meaning or function\) may be changed in future to further optimize performance.  
**4.6  E. InChI Length Block**  


 This criterion like criterion D, is designed to prevent queries that would otherwise return excessively large data sets. Thus criterion E will block sub-queries C1 and C3 for a given a single-component InChI on the basis of the length of the Standard InChI up to the end of the connection layer of the InChI. The default is to not use this block at all, and is specified with a '0'. If set to, say, 45, however, then all InChIs less than 45 characters long will be excluded from C1 and C3 subqueries. But, note that all InChIs returned from other sub-queries will be included, regardless of size, as the block only affects C1 and C3 sub-queries. This value may be set from anywhere between 1 and 2000. Obviously, a higher value \(eg:2000\) will produce a smaller result set than a smaller value. A value below 8 will have no effect at all, as all Standard InChIs are at least 8 characters long, as all begin with 'InChI=1S'. Note that this block cannot override the mandatory block imposed by criterion D. The general issue of limiting sub-queries is dealt with in more detail below.  
**4.7  F. UniChem Labels**  


 UniChem annotates a number of FIKHB's with 'labels' summarizing the meaning of these connectivity hash blocks. Thus the label for the FIKHB of the InChI describing 'HCl' is 'HCl'. The labels are designed to flag frequently occurring components of InChIs in the retrieved data set. This can help to highlight potential salts, etc. The default \('0'\) is to use these labels. If the user does not wish to annotate the retrieved data with labels then '1' should be specified for this criterion. An up to date full list of all labels currently in use can be found on a [Connectivity Labels](https://www.ebi.ac.uk/unichem/widesearch/connectivityLabels) page. This list currently contains only a limited number of the most frequently occurring FIKHBs, but it is anticipated this will be extended in the future to include less frequently occurring salt counter ions. Unfortunately, this list cannot currently be customized for individual queries.  
**4.8  G. Assignment Status**  


 By default, only currently assigned records are retrieved \(i.e. records where the src\_compound\_id is currently assigned to the Standard InChI, as declared in the most recent data load from the source\). However, setting criterion G to '1' will result in both current and obsolete assignments being retrieved.  
**4.9  H. Data Structure**  


 This criterion is used to set the structure of the data object returned. Since in the web interface this structure is defined in the results table, and cannot be changed by the user, this criterion is only available when using the web services. Note that the data structure is NOT the same as the serialization method, which can be specified, as for any web-service call, as described on the [web services page](https://www.ebi.ac.uk/unichem/info/webservices).

 The default \(H='0'\) returns a complex data structure. This structure was chosen for its concise style, and its 'source-centric' format as likely the most useful format for users wishing to use connectivity searching on the fly, in a single query, to generate hyperlinks within the compound pages of their resource. Perhaps the best way to understand the format is to simply study an example of the output, but briefly...

 An associative array consisting of 'Assignment Grouping Number' keys represent different Query InChI subqueries. 'Assignment Grouping Number' are integers \(from 1 upwards\). For most queries, there will only be one such key, with a value of '1', however, for some queries, multiple keys may exist See below for why this sometimes occurs. Each of these keys will have the data structure from a separate sub-query as the 'values' of the associative array. Each of these values consist of an ordered array of source data information: One element per separate source in UniChem \(although sources not returning data for this particular query are omitted\). Each of the elements in this ordered array consists of a associative array of key-value pairs, where each key represents some information about the source. These keys are listed in the table below.  


| key | Description |
| :--- | :--- |
| src\_id | An integer use to unambiguously identify this source in UniChem |
| src\_URL | The home page of the source |
| src\_details | Some information on how the data was obtained from the source and processed prior to loading into UniChem |
| aux\_for\_url | A flag to indicate how URLs for compound specific pages should be created: either by appending the src\_compound\_id \('0'\), or the aux\_src \('1'\) to the base\_id\_url. |
| base\_id\_url\_available | A flag to indicate whether this source supports compound-specific pages which can be hyperlinked to \(1 = yes, 0 = no\) |
| base\_id\_url | The base URL to which src\_compound\_id must be appended in order to create a valid URL to the source compound-specific page. |
| description | A description of the source |
| name | A short unique label for the source \(always lower case\) |
| name\_label | A short string suitable for a label for this source |
| name\_long | The long name for the source |
| src\_matches | Data describing what src\_compound\_id assignments from this source have matched the Query InChI. |

 The values associated with the above keys are all text strings except for the 'src\_matches' key, for which the value is an ordered array. Each element of this array is an associative array describing the 'match' of an src\_compound\_id assignment to the Query InChI. Note that src\_compound\_ids with multiple assignments where more than one of the assignments has been matched, will result in the presence of more than one element for this src\_compound\_id; each separate element dealing with the separate assignments for this src\_compound\_id.  


| key | Description |
| :--- | :--- |
| src\_compound\_id | The src\_compound\_id |
| aux\_src | The string that should be appended to the base\_id\_url to create a hyperlink to the compound specific page in this source, if the aux\_for\_url flag is set to '1' for this source. |
| B | The value of Criterion B in the query |
| CpdId\_InChIKey | The InChIKey assigned to this src\_compound\_id in UniChem |
| Full\_CpdId\_InChI | The InChI assigned to this src\_compound\_id in UniChem |
| assignment | The setting of this assignemnt \(1=current, 0=obsolete |
| match\_compare | Data describing the ways in which this src\_compound\_id assignment have matched the query. |

 The values associated with the above keys are all text strings except for the 'match\_compare' key, for which the value is an ordered array. Each element of this array is an associative array describing the \(possibly many\) 'matches' of this src\_compound\_id assignment to the Query InChI.  


| key | Description |
| :--- | :--- |
| C | The value of the criterion C in the query. May be 0-3. Indicates the relationship between the Query InChI and the CpdId InChI |
| Matching\_Query\_InChI | Either the Query InChI itself, or the component InChI within the Query InChI which matches the CpdId\_InChI. |
| Matching\_CpdId\_InChI | Either the CpdId InChI itself \(ie the InChI assigned to the src\_compound\_id\), or the component InChI within the CpdId InChI which matches the Query\_InChI. |
| b | A comparison of the 'b' layer between the Matching Query InChI and the Matching CpdId InChI \(0=same, 1=different\) |
| i | A comparison of the 'i' layer between the Matching Query InChI and the Matching CpdId InChI \(0=same, 1=different\) |
| m | A comparison of the 'm' layer between the Matching Query InChI and the Matching CpdId InChI \(0=same, 1=different\) |
| p | A comparison of the 'p' layer between the Matching Query InChI and the Matching CpdId InChI \(0=same, 1=different\) |
| s | A comparison of the 's' layer between the Matching Query InChI and the Matching CpdId InChI \(0=same, 1=different\) |
| t | A comparison of the 't' layer between the Matching Query InChI and the Matching CpdId InChI \(0=same, 1=different\) |

 Changing 'H' from the default to '1' will create the same data in a different structure. With H=1, all source specfic data is absent \(apart from the src\_id\), and the remaining data is 'flattened' into an array of arrays, resembling the data structure in the output generated from the web-interface. The first array is an array of the 'headers' for all subsequent data. This arrangement of the data is more suited to direct import into a flat file. Because most of the source-specific data is absent, a second query for these data would be necessary in order to create hyperlink URLs to compound specific pages of a source.

 Currently, H0 and H1 are the only two data formats supported.  
  
  


#### Section 5  Multiple Component InChIs.

[\(Back up to Contents\)](https://www.ebi.ac.uk/unichem/info/widesearchInfo#Contents)

 Querying with multiple component InChIs \(ie: mixtures or salts\) can produce a number of complications such as apparent redundancy. These complications are dealt with by UniChem in a particular way, which is described here with examples. In the examples that follow, criterion G is set to ‘1’, so that both current and obsolete assignments are retrieved. This is because some of the examples require reference to now obsolete assignments. Also criterion A may set to ‘1’ throughout. This is not strictly necessary to illustrate the behavior under discussion, but serves to produce a clearer output \(uncluttered with data from other sources\), since all examples refer to data from only one source \(ChEMBL\).

 CHEMBL2097107 is the ChEMBL src\_compound\_id currently assigned to a composite InChI; the mixture 'Amoxycillin and Clavulanic acid'. Querying with CHEMBL2097107, and with C initially set to '0' will retrieve CHEMBL8156 \(an obsolete an src\_compound\_id for the same mixture, but where there are some differences in stereochemistry\), but will not retrieve CHEMBL1082 \(the src\_compound\_id for Amoxicillin\).

 Repeating this query but with C set to '1' will retrieve nothing, as a multi-component can never be a single component of a multiple-component InChI. However, changing C to '2' will retrieve CHEMBL1082 but not CHEMBL8156. Changing C to '3' will retrieve CHEMBL8156 again, and a src\_compound\_id not retrieved by the previous two setting: CHEMBL2105950 \(Amoxicillin Na\). Setting C to '4' will retrieve all three: CHEMBL2105950, CHEMBL8156 and CHEMBL1082. This is perhaps as one might expect in view of the component mapping relationships defined in table 2.

 However, closer inspection of the result set will reveal that some apparent redundancy is present in the results set. Thus, when C is set to '3', then both CHEMBL8156 and CHEMBL2097107 are retrieved twice. This is because the multiple components within the query separately match to multiple components of the retrieved InChI. Each is given a separate record so that the user may understand how each of the separate components differ. This situation becomes more complicated when searching with the 'C' criterion set to '4'. In this case, CHEMBL2097107 will match on both the 'C0' and the 'C3' subqueries. This might be expected to lead to yet more apparent redundancy in the output. In fact, however, UniChem will only show the results of the 'C3' subquery if the 'C0' subquery is not an exact match. In other words, if, for the 'C0' subquery, no differences between the InChI layers are detected, then the results of the 'C3' query are not shown. Thus, the result of querying with CHEMBL2097107 with C set to '4' \(and G = '1'\) will be three records for CHEMBL8156, and one for CHEMBL2097107. The reason for this is that since no differences exist between the Full Query InChI and the Full retrieved InChI, then none would be expected between the separate component InChIs, and so the user would gain no additional information. Likewise, if differences do exist between the full composite InChIs then the user may wish to determine which of the components differ \(which can be deduced from an analysis of the C3 subquery results\). Thus when querying with a multi-component InChI, with C set to '4', the Query src\_compound\_id itself will only ever appear once in the result set. However, it should be noted that the above rules are applied to any src\_compound\_id in the result set that is assigned to an identical compound InChI to the Query InChI, and not just the Query src\_compound\_id.

 One further complication arises from the process of splitting multi-component InChIs. The 'p' layer in a multi-component InChI is a single value descriptor applied to the entire multi-component InChI and cannot be ascribed to the separate InChIs during splitting. For this reason, the 'p' value is ignored when creating the separate InChIs from a multi-component InChI. Thus, comparisons of the p layers are only valid where none of the compared InChIs have been split. For this reason, in the results set, 'p' comparisons are shown as 'null' for all component mapping relationships other than C=0.  
  
  


#### Section 6  Avoiding excessively large Result sets.

[\(Back up to Contents\)](https://www.ebi.ac.uk/unichem/info/widesearchInfo#Contents)

 A potential problem of using C1 and C3 search criterion is that under certain circumstances the number of records retrieved can potentially be vast, and almost certainly not intended or required by the user. For example, consider the case of a sodium salt of X, a molecule of interest. If criterion C3 is used, then all the different mixtures and salt forms of X would be retrieved, which for many compounds of interest might typically amount to several dozen different InChIs. These are the data which are most likely to be of greatest interest to the user. However, in addition, this same query will also retrieve all sodium salts of any molecule in UniChem. This could amount to many tens of thousands of different InChIs, if not more. To prevent this, UniChem employs a number of mechanisms which stop such C1 and C3 sub-queries from running at all \(but still allowing the 'molecule of interest' C1/C3 sub-query to be run\). These mechanisms are described below. None are ideal solutions to this problem, but do serve to provide a useful result set quickly, whilst protecting UniChem and the user from being overwhelmed.

 The first mechanism \(based around criterion D\) simply blocks queries on single-InChI components which UniChem knows occur with very great frequency in multiple-component InChIs in UniChem. The default setting for this 'frequency block' in UniChem is currently 200, although the user may alter this to any specified number, but only up to 500 \(currently\). Note that this threshold number refers to the number of distinct Standard InChIs in UniChem that contain the single component. Since the records retrieved by the 'key\_search' method is based on src\_compound\_id, and since many src\_compound\_ids \(often from different sources\) are assigned to the same InChI, then the '500' cutoff does not mean that no more than 500 records can ever be retrieved by C1 or C3. Rather, it simply means that if the query is going to retrieve a data set from either the C1 or C3 part of the query which would contain more than 500 distinct InChIs, then none at all will be retrieved from that sub-query for that particular single-InChI component. Note, therefore, that this represents not so much a 'cutoff' as a 'block' on anything above the threshold \(ie: In the example above, none of the many tens of thousands of sodium salts would be retrieved\). Note also that this high frequency block only refers to the data retrieved separately for each component in a C1 or C3 sub-query \(ie: 'X', the \`molecule of interest\` in the example above, will still yield a result set, even if its fellow component is blocked\).

 In addition to this 'frequency block', the user also has the option to include an additional block, based on length of the InChI. This additional block cannot be used instead of the frequency block \(the '500' limit cannot be overridden\), but may be useful to employ for less common single-InChI-components that might be identified as potentially of less interest simply on the basis of the length of the Std InChI.

 None of the two mechanisms above provide a perfect solution to the problem of retrieving large amounts of unwanted data. Even the most careful setting of the criteria D and E is unlikely to result in the user never missing some data of interest. This is an unfortunate consequence of the need to protect UniChem from excessively large queries, and to prevent users from being overwhelmed with irrelevant data. However, despite this shortcoming, these mechanisms do allow a simple, low maintenance, automated solution, whilst at the same time allowing fast retrieval times.  
  
  


#### Section 7  Multiply assigned src\_compound\_ids

[\(Back up to Contents\)](https://www.ebi.ac.uk/unichem/info/widesearchInfo#Contents)

 In some cases a src\_compound\_id can be currently assigned to multiple InChIs. This is perfectly permissible in UniChem. Querying with these sort of src\_compound\_ids will result in UniChem initially retrieving multiple 'Query InChIs'. In this situation, UniChem then takes each 'Query InChI' in turn, and runs a separate query on each. The output from all these separate queries is combined into a single data structure, but each separate query is tagged with an 'Assignment Grouping Number'. In the web-services output, the Assignment Grouping Number is present as the top level key of the data structure \(see Search Criterion H above\). When using the web interface if an Assignment Grouping Number other than '1' is present, then the user receives clear warnings about this at the head of the results table page, and the users attention is drawn to the Assignment Grouping Numbers shown in a column marked '\#' on the far right hand side of the results table.

 Multiply assigned src\_compound\_ids in the results set from a Connectivity Query present less of a problem. Suppose that a particular src\_compound\_id is assigned to multiple InChIs. If one of these InChIs matches in some way to the Query InChI, then only this matching InChI assignment is retrieved and shown in the results table, as might be expected. However, if more than one of the multiple InChIs assigned to this src\_compound\_id match the Query InChI then all of these matches are retrieved, and shown separately. An example of this can be seen if one Queries with CHEMBL2097107, using all the default settings \(ie: 0 for everything\), except for criterion 'C' set to '2'. By filtering the results data set for the src\_compound\_id:'EP0220925A1' \(use the filter text bar at the top right of the data table\) it can be seen that 2 records exist for EP0220925A1, and that the InChI assigned to the src\_compound\_id for each of these is different.  
  
  


#### Section 8  Querying with InChIKeys that do not exist in UniChem

[\(Back up to Contents\)](https://www.ebi.ac.uk/unichem/info/widesearchInfo#Contents)

 If a user queries with an InChIKey which does not exist within UniChem, then clearly, UniChem cannot obtain the corresponding 'Query InChI' \(except in one particular situation, described further below\), and so returns no assignment data. However, in addition to this information, in the web interface UniChem is also able to inform the user as to whether data exists for the connectivity layer of this failed InChIKey query, and if there is, it invites the user to re-query with the FIKHB alone.

 Querying with the FIKHB alone will retrieve data successfully if there are any InChIKeys in UniChem with this connectivity layer, or any components of InChIs in UniChem which share this connectivity layer \(ie: the InChI sharing the connectivity layer need not necessarily be an InChI assigned in UniChem, it may only exist as a component of a multi-component InChI which is assigned\). Critically though, because a 'Query InChI' is required for any successful connectivity search, the first InChIKey hash block \(FIKHB\) that was used for the query must somehow be converted to an InChI.

 For this purpose, the block '-UHFFFAOYSA-N' is effectively appended to the query InChIKey, to create a hypothetical full InChIKey \(but with no non-connectivity data present, since this string represents the remainder of the InChIKey which is always created for InChIs with no stereochemistry or isotope information, and no proton flag\). The corresponding hypothetical InChI is then obtained by removing the non-connectivity layers from an InChI which shares the connectivity layers with the query. These operations are necessary to provide the user with a 'Query InChI' with which to make comparisons. It should always be remembered that querying with the connectivity layer of the InChIKey alone in this way will always trigger this process, and so all comparisons shown in the results table are with respect to the non-stereo form with a proton flag of '-N', regardless of the plausibility of this molecule in reality.

 There is one situation where querying with a full InChIKey which does not exist in UniChem may retrieve data without requiring re-querying with a connection block alone, as described above. This arises when the query InChIKey contains a second hash block of 'UHFFFAOYSA'. In this situation, a similar search for the corresponding InChI is triggered as explained above. If an InChI can be found in this way, then the query may continue, but only after UniChem has automatically appended the proton flag to the InChI, as specified in the query InChIKey. Clearly, in this situation then, the comparisons made in the 'p' layer on the results page will be with respect to whatever was specified in the query InChIKey. This contrasts with the default '-N' that is always used if the FIKHB alone is used as the query term, as explained in the previous paragraph. It is also worth mentioning at this point that the choice of querying with either a Full InChIKey or a FIKHB will not affect the 'pattern' that is used to find matches. This pattern is defined only by criterion 'B', and never by the query term. Thus, for example, querying with...

 PQLXHQMOHUQAKB

 ...with all criteria set to '0' will retrieve matches to InChIs with InChIKeys such as...

 PQLXHQMOHUQAKB-PGVNZGOUSA-N  
 and  
 PQLXHQMOHUQAKB-UHFFFAOYSA-N  
 and  
 PQLXHQMOHUQAKB-UHFFFAOYSA-O  


 ...but with 'B' set to '1', this same query will retrieve ONLY InChIs with InChIKeys...

 PQLXHQMOHUQAKB-UHFFFAOYSA-N  
 and  
 PQLXHQMOHUQAKB-UHFFFAOYSA-O  


...and any other InChIs in UniChem with keys differing only in the proton layer.  
  
  


#### Section 9  Working within the constraints of Standard InChI

 UniChem utilizes the Standard InChI and does not accept non-Standard InChIs. Higher levels of structural representation that can only be captured in non-Standard InChIs, and not in Standard InChIs, are therefore clearly lost. In addition to this, there are other limitations of the Standard InChI which affect Connectivity Searching, and which are discussed here. Connectivity Searching in UniChem relies entirely upon the ability of InChI software to normalize the connectivity of molecules that may have been drawn in different protonation or charge states. In the vast majority of cases of compounds of biological interest, InChI handles these normalizations extremely well. There are some examples, however, where InChI is not yet able to handle such normalization correctly. Clearly, UniChem is not able to correct for these occurrences, as it relies solely on the InChI software to create connection keys. Users should therefore be aware of these shortcomings, as in some cases this can explain the absence of connectivity matches that may have been expected.

 For example, for a sodium salt of a carboxylic acid such as aminobenzoic acid the InChI software understands that the carboxylic acid has been deprotonated and the InChI is...

 InChI=1S/C7H7NO2.Na/c8-6-3-1-5\(2-4-6\)7\(9\)10;/h1-4H,8H2,\(H,9,10\);/q;+1/p-1

 In this case the connectivity layer of the aminobenzoate component will match that of aminobenzoic acid where the InChI is...

 InChI=1S/C7H7NO2/c8-6-3-1-5\(2-4-6\)7\(9\)10/h1-4H,8H2,\(H,9,10\)

 ...and so aminobenzoic acid will be identified as a component of sodium aminobenzoate, and likewise sodium aminobenzoic acid will be identified as matching a component of aminobenzoic acid.

 This works well for most common salts such as carboxylates, phenolates, hydrochlorides and ammonium salts. More details can be found on which salts are represented in their connected or disconnected form on page 20 of the InChI Technical Manual version 1.04. However, there are some relatively common acid anions that are not recognized as acid anions and so the relationship between the parent and salt is lost. Sulphonamides and tetrazoles are the most common examples of this but there are others. For example, the InChI for methyl tetrazole is...

 InChI=1S/C2H4N4/c1-2-3-5-6-4-2/h1H3,\(H,3,4,5,6\)

 ...whereas the InChI for its sodium salt is...

 InChI=1S/C2H3N4.Na/c1-2-3-5-6-4-2;/h1H3;/q-1;+1

 i.e. the InChI software doesn’t know to protonate the tetrazole and so the InChIs for the tetrazole components of these two compounds are different. Other shortcomings that result from limitations in InChI are that certain enantiomers cannot be identified by comparing Standard InChIs.  
  


