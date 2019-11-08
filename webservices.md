# Webservices

Using the UniChem web service API users can retrieve data from the UniChem database in a programmatic fashion. This page documents the currently supported functionality and defines the expected inputs and outputs of each method, together with examples for each one \(which may be tested most simply by pasting into a browser, or using an open source tool such as [RESTClient from WizTools](http://www.wiztools.org/) \). 

Please note that although that wherever possible small data sets are used in the examples, occassionally the only examples possible are with larger sets, which may take some time to retrieve \(such as the auxiliary mapping method\). In order to help you get started, we have provided some example cURL requests \(below\). Note that for small, ad hoc queries, users should consider simply using the [Home / Search](https://www.ebi.ac.uk/unichem/) page.

 For whole source mapping, users are strongly advised to simply download the pre-generated mappings as gzip files from the [downloads site](https://www.ebi.ac.uk/unichem/info/downloads) instead, rather than use the web services mapping method described below.

## Constructing Queries.

All RESTful queries are constructed using the following 'stem' or 'base' url:  
**https://www.ebi.ac.uk/unichem/rest/**   

Specific query urls are all constructed by adding a method name to this base url, followed by input data, as shown in the API methods section below.

 Input data may consist of three types:

*   src\_compound\_id
* src\_id
* InChIKey

**src\_ids** are integers that represent the various sources in UniChem. A list of valid src\_ids can be found either on the [sources](https://www.ebi.ac.uk/unichem/ucquery/listSources) page or by using the 'Get all src\_ids' method below.'

For some methods, a '**to\_src\_id**' may be required. This is simply a normal src\_id but serves to specify the source to which the output is specifically mapped to.

**src\_compound\_ids** are the individual compound identifiers provided by each of the sources. Since src\_compound\_ids may be ambiguous across different sources, most API methods requiring a src\_compound\_id as an input also require the specification of a corresponding src\_id. However, for a few methods, an '**orphan src\_compound\_id**' is expected. An 'orphan src\_compound\_id' is simply a normal src\_compound\_id for which the src\_id is not specified. For example, '1234' and 'CHEMBL121' are both termed an 'orphan src\_compound\_id's if their corresponding src\_ids are not specified. Methods accepting such 'orphan src\_compound\_ids' serve to identify possible src\_ids for the orphan src\_compound\_id \(eg: '4, 22, 31' and '1', respectively, using the previous example\). Other methods using 'orphan src\_compound\_id's serve first to identify possible src\_ids for the orphan src\_compound\_id, and then to generate all possible mappings to other src\_compound\_id/src\_ids for each of the possible src\_ids for the orphan src\_compound\_id \(eg: method 'Get mappings for orphan src\_compound\_id'\).

Note also that src-compound\_ids are treated in a case-sensitive manner throughout UniChem \(see [here](https://www.ebi.ac.uk/unichem/info/inputFormats) for formatting information on search terms\).  


## Content Negotiation.

 The default data serialization method is JSON. However, alternative content types are available \(eg: XML\). These may be selected by the user by specifying the content type HTTP Accept header \(eg: 'text/xml' for XML\). JSONP may be returned without specifying an Accept header, but by simply appending **'?callback=xyz'** to the request\_url \(where 'xyz' is defined by the user\). In this case, the returned object will then have the form of **xyz\(serializedJSON\)**. See examples at the foot of this page.

## Error Codes.

| HTTP Response Code | Summary | Description |
| :--- | :--- | :--- |
| 200 | OK | The request to the web service completed successfully. This includes valid requests that happen to return empty data sets. |
| 400 | Bad Request | The parameters passed to the API endpoint were deemed invalid. This response will be returned for... 1. Invalid API method names, or 2. Valid method names with invalid numbers of parameters, or 3. InChIKeys which do not match the pattern of a Standard InChIKey version 1 |
| 404 | Not Found | The resource corresponding to the supplied parameters does not exist. This response will be returned if the inputted data type \(src\_compound\_id, src\_id, or InChIKey matching the pattern of a Standard InChIKey version 1\) does not exist in UniChem. |
| 500 | Service Unavailable | An internal problem prevented us from fulfilling your request.    |

## Methods

### Get src\_compound\_ids from src\_compound\_id

**Description:**  

* Obtain a list of all src\_compound\_ids from all sources which are CURRENTLY assigned to the same structure as a currently assigned query src\_compound\_id. 
* The output will include query src\_compound\_id if it is a valid src\_compound\_id with a current assignment. 
* Note also, that by adding an additional \(optional\) argument \(a valid src\_id\), then results will be restricted to only the source specified with this optional argument.

**Extension of base url:**  src\_compound\_id  
**Number of required input parameters:**  2 or 3  
**Input:**  /src\_compound\_id/src\_id\(/to\_src\_id\)  
**Output:**  list of two element arrays, containing 'src\_compound\_id' and 'src\_id', or \(if optional 'to\_src\_id' is specified\) list of 'src\_compound\_id's.  
**Example:**  [https://www.ebi.ac.uk/unichem/rest/src\_compound\_id/CHEMBL12/1](https://www.ebi.ac.uk/unichem/rest/src_compound_id/CHEMBL12/1)  
**Example:**  [https://www.ebi.ac.uk/unichem/rest/src\_compound\_id/CHEMBL12/1/2](https://www.ebi.ac.uk/unichem/rest/src_compound_id/CHEMBL12/1/2)

### Get src\_compound\_ids all from src\_compound\_id

**Description:**  

* Obtain a list of all src\_compound\_ids from all sources \(including BOTH current AND obsolete assignments\) to the same structure as a currently assigned query src\_compound\_id. 
* The output will include query src\_compound\_id if it is a valid src\_compound\_id with a current assignment. 
* Note also, that by adding an additional \(optional\) argument \(a valid src\_id\), then results will be restricted to only the source specified with this optional argument.

**Extension of base url:**  src\_compound\_id\_all  
**Number of required input parameters:**  2 or 3  
**Input:**  /src\_compound\_id/src\_id\(/to\_src\_id\)  
**Output:**  list of three element arrays, containing 'src\_compound\_id', 'src\_id' and 'Assignment', or \(if optional 'to\_src\_id' is specified\) list of two element arrays, containing 'src\_compound\_id' and 'Assignment'.  
**Example:**  [https://www.ebi.ac.uk/unichem/rest/src\_compound\_id\_all/CHEMBL12/1](https://www.ebi.ac.uk/unichem/rest/src_compound_id_all/CHEMBL12/1)  
**Example:**  [https://www.ebi.ac.uk/unichem/rest/src\_compound\_id\_all/CHEMBL12/1/2](https://www.ebi.ac.uk/unichem/rest/src_compound_id_all/CHEMBL12/1/2)

### Get mapping

**Description:**  Obtain a full mapping between two sources. Uses only currently assigned src\_compound\_ids from both sources.  
 **Extension of base url:**  mapping  
 **Number of required input parameters:**  2  
 **Input:**  src\_id/to\_src\_id  
 **Output:**  list of two element arrays, containing 'src\_compound\_id' and 'src\_compound\_id'.  
 **Example:**  [https://www.ebi.ac.uk/unichem/rest/mapping/4/1](https://www.ebi.ac.uk/unichem/rest/mapping/4/1)

### Get src\_compound\_ids from InChIKey

**Description:**  Obtain a list of all src\_compound\_ids \(from all sources\) which are CURRENTLY assigned to a query InChIKey  
 **Extension of base url:**  inchikey  
 **Number of required input parameters:**  1  
 **Input:**  /InChIKey  
 **Output:**  list of two element arrays, containing 'src\_compound\_id' and 'src\_id'.  
 **Example:**  [https://www.ebi.ac.uk/unichem/rest/inchikey/AAOVKJBEBIDNHE-UHFFFAOYSA-N](https://www.ebi.ac.uk/unichem/rest/inchikey/AAOVKJBEBIDNHE-UHFFFAOYSA-N)

### Get src\_compound\_ids all from InChIKey

**Description:**  Obtain a list of all src\_compound\_ids \(from all sources\) which have current AND obsolete assignments to a query InChIKey  
 **Extension of base url:**  inchikey\_all  
 **Number of required input parameters:**  1  
 **Input:**  /InChIKey  
 **Output:**  list of two element arrays, containing 'src\_compound\_id', 'src\_id' and 'Assignment'.  
 **Example:**  [https://www.ebi.ac.uk/unichem/rest/inchikey\_all/AAOVKJBEBIDNHE-UHFFFAOYSA-N](https://www.ebi.ac.uk/unichem/rest/inchikey_all/AAOVKJBEBIDNHE-UHFFFAOYSA-N) 

### Get all src\_ids

 **Description:**  Obtain all src\_ids currently in UniChem  
 **Extension of base url:**  src\_ids  
 **Number of required input parameters:**  0  
 **Input:**   - none -  
 **Output:**  list of 'src\_id's.  
 **Example:**  [https://www.ebi.ac.uk/unichem/rest/src\_ids/](https://www.ebi.ac.uk/unichem/rest/src_ids/)

### Get source infomation

 **Description:**  Obtain all information on a source by querying with a source id \(src\_id\).  
 **Extension of base url:**  sources  
 **Number of required input parameters:**  1  
 **Input:**  /src\_id  
 **Output:**  list containing:

* src\_id \(the src\_id for this source\).
* src\_url \(the main home page of the source\).
* name \(the unique name for the source in UniChem, always lower case\).
* name\_long \(the full name of the source, as defined by the source\).
* name\_label \(A name for the source suitable for use as a 'label' for the source within a web-page. Correct case setting for source, and always less than 30 characters\).
* description \(a description of the content of the source\).
* base\_id\_url\_available \(an flag indicating whether this source provides a valid base\_id\_url for creating cpd-specific links \[1=yes, 0=no\]\).
* base\_id\_url \(the base url for constructing hyperlinks to this source \[append an identifier from this source to the end of this url to create a valid url to a specific page for this cpd\], unless aux\_for\_url=1\).
* aux\_for\_url \(A flag to indicate whether the aux\_src field should be used to create hyperlinks instead of the src\_compound\_id \[1=yes, 0=no\].

**Example:**  [https://www.ebi.ac.uk/unichem/rest/sources/1](https://www.ebi.ac.uk/unichem/rest/sources/1)

###  Get structure

 **Description:**  Obtain structure\(s\) CURRENTLY assigned to a query src\_compound\_id.  
 **Extension of base url:**  structure  
 **Number of required input parameters:**  2  
 **Input:**  /src\_compound\_id/src\_id  
 **Output:**  list of two element arrays, containing 'Standard InChI', and 'Standard InChIKey'  
 **Example:**  [https://www.ebi.ac.uk/unichem/rest/structure/CHEMBL12/1](https://www.ebi.ac.uk/unichem/rest/structure/CHEMBL12/1)

### Get structure all

 **Description:**  Obtain structure\(s\) with current AND obsolete assignments to a query src\_compound\_id.  
 **Extension of base url:**  structure\_all  
 **Number of required input parameters:**  2  
 **Input:**  /src\_compound\_id/src\_id  
 **Output:**  list of three element arrays, containing 'Standard InChI', 'Standard InChIKey', and 'Assignment'  
 **Example:**  [https://www.ebi.ac.uk/unichem/rest/structure\_all/CHEMBL12/1](https://www.ebi.ac.uk/unichem/rest/structure_all/CHEMBL12/1)

### Get URL for src\_compound\_ids from src\_compound\_id

**Description:**  

* Obtain a list of URLs for all src\_compound\_ids, from a specified source \(the 'to\_src\_id'\), which are CURRENTLY assigned to the same structure as a currently assigned query src\_compound\_id.
* Method only applicable for sources which support direct URLs to src\_compound\_id pages. 
* Method also applicable for 'to\_src\_id's where the hyperlink is constructed from auxiliary data \[and not from the src\_compound\_id\] as per example 2 below.

**Extension of base url:**  src\_compound\_id\_url  
**Number of required input parameters:**  3  
**Input:**  /src\_compound\_id/src\_id/to\_src\_id  
**Output:**  list of URLs.  
**Example:**  [https://www.ebi.ac.uk/unichem/rest/src\_compound\_id\_url/CHEMBL12/1/2](https://www.ebi.ac.uk/unichem/rest/src_compound_id_url/CHEMBL12/1/2)  
**Example:**  [https://www.ebi.ac.uk/unichem/rest/src\_compound\_id\_url/CHEMBL490/1/15](https://www.ebi.ac.uk/unichem/rest/src_compound_id_url/CHEMBL490/1/15)

### Get src\_compound\_ids all from obsolete src\_compound\_id

**Description:**  

* Obtain a list of all src\_compound\_ids from all sources with BOTH current AND obsolete to the same structure with an obsolete assignment to the query src\_compound\_id. 
* The output will include query src\_compound\_id if it is a valid src\_compound\_id with an obsolete assignment. 
* Note also, that by adding an additional \(optional\) argument \(a valid src\_id\), then results will be restricted to only the source specified with this optional argument. 

**Extension of base url:**  src\_compound\_id\_all\_obsolete  
 **Number of required input parameters:**  2 or 3  
 **Input:**  /src\_compound\_id/src\_id\(/to\_src\_id\)  
 **Output:**  list of four element arrays, containing 'src\_compound\_id', 'src\_id', 'Assignment' and 'InChIKey', or \(if optional 'to\_src\_id' is specified\) list of three element arrays, containing 'src\_compound\_id', 'Assignment' and 'UCI'.  
 **Example:**  [https://www.ebi.ac.uk/unichem/rest/src\_compound\_id\_all\_obsolete/DB07699/2](https://www.ebi.ac.uk/unichem/rest/src_compound_id_all_obsolete/DB07699/2)  
 **Example:**  [https://www.ebi.ac.uk/unichem/rest/src\_compound\_id\_all\_obsolete/DB07699/2/1](https://www.ebi.ac.uk/unichem/rest/src_compound_id_all_obsolete/DB07699/2/1)  


### Get verbose src\_compound\_ids from InChIKey

**Description:**  

* Obtain all src\_compound\_ids \(from all sources\) which are CURRENTLY assigned to a query InChIKey. 
* However, these are returned as part of the following data structure: 
  * A list of sources containing these src\_compound\_ids, including source description, base\_id\_url, etc. 
  * One element in this list is a list of the src\_compound\_ids currently assigned to the query InChIKey.

**Extension of base url:**  verbose\_inchikey  
**Number of required input parameters:**  1  
**Input:**  /InChIKey  
**Output:**  list containing:

* src\_id \(the src\_id for this source\).
* src\_url \(the main home page of the source\).
* name \(the unique name for the source in UniChem, always lower case\).
* name\_long \(the full name of the source, as defined by the source\).
* name\_label \(A name for the source suitable for use as a 'label' for the source within a web page. Correct case setting for source, and always less than 30 characters.
* description \(a description of the content of the source\).
* base\_id\_url\_available \(an flag indicating whether this source provides a valid base\_id\_url for creating cpd-specific links \[1=yes, 0=no\]\).
* base\_id\_url \(the base url for constructing hyperlinks to this source \[append an identifier from this source to the end of this url to create a valid url to a specific page for this cpd\], unless aux\_for\_url=1\).
* aux\_for\_url \(A flag to indicate whether the aux\_src field should be used to create hyperlinks instead of the src\_compound\_id \[1=yes, 0=no\] .
* src\_compound\_id \(a list of src\_compound\_ids from this source which are currently assigned to the query InChIKey.
* aux\_src \(a list of src-compound\_id keys mapping to corresponding auxiliary data \(url\_id:value\), for creating links if aux\_for\_url=1. Only shown if aux\_for\_url=1\).

**Example:**  [https://www.ebi.ac.uk/unichem/rest/verbose\_inchikey/GZUITABIAKMVPG-UHFFFAOYSA-N](https://www.ebi.ac.uk/unichem/rest/verbose_inchikey/GZUITABIAKMVPG-UHFFFAOYSA-N)

### Get auxiliary mappings

**Description:**  

* For a single source, obtain a mapping between all current src\_compound\_ids to their corresponding auxiliary data.
* See FAQ for an explanation of 'auxiliary data'. Please note that the only examples available \(below\) for this method may be very large data sets, and may therefore take a very long time to retrieve. 
* A much faster method of retrieving this same data set is to download the pre-cached, gzipped mapping file for the source of interest from the Auxiliary Data Mapping page.

**Extension of base url:**  mappingaux  
**Number of required input parameters:**  1  
**Input:**  /src\_id  
**Output:**  list of two element arrays, containing 'src\_compound\_id' and 'auxiliary data'.  
**Example:**  [https://www.ebi.ac.uk/unichem/rest/mappingaux/20](https://www.ebi.ac.uk/unichem/rest/mappingaux/20)

### Get Connectivity data from InChIKey

**Description:**  

* One of two 'Connectivity-Based' Searching methods. Because of the complexity of these methods, details are shown elsewhere. 
* Follow link in 'Details' below. 
* This method replaces the now deprecated 'Get verbose src\_compound\_ids from InChIKey' method above. **Extension of base url:**  key\_search **Number of required input parameters:**  1 and optional criteria A-H **Input:**  /InChIKey/A/B/C/D/E/F/G/H **Detail:**  [https://www.ebi.ac.uk/unichem/info/widesearchInfo](https://www.ebi.ac.uk/unichem/info/widesearchInfo)

### Get Connectivity data from src\_compound\_id

**Description:**  One of two 'Connectivity-Based' Searching methods. Because of the complexity of these methods, details are shown elsewhere. Follow link in 'Details' below.  
**Extension of base url:**  cpd\_search  
**Number of required input parameters:**  2 and optional criteria A-H  
**Input:**  /src\_compound\_id/src\_id/A/B/C/D/E/F/G/H  
**Detail:**  [https://www.ebi.ac.uk/unichem/info/widesearchInfo](https://www.ebi.ac.uk/unichem/info/widesearchInfo)

### Get InChI from InChIKey

**Description:**  Obtain InChI for InChIKey  
**Extension of base url:**  inchi  
**Number of required input parameters:**  1  
**Input:**  /InChIKey  
**Output:**    
**Example:**  [https://www.ebi.ac.uk/unichem/rest/inchi/AAOVKJBEBIDNHE-UHFFFAOYSA-N](https://www.ebi.ac.uk/unichem/rest/inchi/AAOVKJBEBIDNHE-UHFFFAOYSA-N)

### Get Current Release Information

**Description:**  Obtain Information about the Current Release  
**Extension of base url:**  release  
**Number of required input parameters:**  0  
**Input:**   - none -  
**Output:**  list containing:

* release \(the current release number \[aka UDRI \(UniChem Data Release ID\)\].
* date \(the date of the current release\).
* source\_count \(The number of sources in the current release\).
* structure\_count \(The number of structures in the current release\).
* xref\_count \(The number of XREF records \[aka assignments\] in the current release\).
* xref\_count\_current \(The number of Current XREF records \[aka current assignments\] in the current release\).
* xref\_count\_obsolete \(The number of Obsolete XREF records \[aka obsolete assignments\] in the current release\).  **Example:**  [https://www.ebi.ac.uk/unichem/rest/release/](https://www.ebi.ac.uk/unichem/rest/release/)

### Get src\_ids for orphan src\_compound\_id

**Description:**  Obtain a non-redundant list of all src\_ids which have current assignments for an 'orphan src\_compound\_id' \(see definition in 'Constructing Queries', above\).  
**Extension of base url:**  orphanIdSource  
**Number of required input parameters:**  1  
**Input:**  /src\_compound\_id  
**Output:**  list of possible 'src\_id's for the query orphan src\_compound\_id  
**Example:**  [https://www.ebi.ac.uk/unichem/rest/orphanIdSource/1234](https://www.ebi.ac.uk/unichem/rest/orphanIdSource/1234)  
**Example:**  [https://www.ebi.ac.uk/unichem/rest/orphanIdSource/AIN](https://www.ebi.ac.uk/unichem/rest/orphanIdSource/AIN)  


### Get mappings for orphan src\_compound\_id

**Description:**  

* Obtain mappings between the query 'orphan src\_compound\_id' \(see definition in 'Constructing Queries', above\) and all other src\_compound\_ids from all other sources. 
* A separate set of mappings is supplied for each possible src\_id identified for the orphan src\_compound\_id. 
* Only current mappings are shown \(ie: mappings between src\_compound\_ids with current assignments\). 
* Optionally, returned data may be filtered to give only mappings TO a particular src\_id of interest by adding a 'to\_src\_id' as an additional argument. Thus appending the additional arguement '1' to a query will return only mappings TO ChEMBL \(see 3rd example below\). 
* UCI \(UniChem Identifiers\) are also included for each mapping in case a query orphan src\_compound\_id were to be mapped to multiple structures in a single source \(unlikely\). In this case the UCI can be used to distinguish the mappings for the different structures. **Extension of base url:**  orphanIdMap **Number of required input parameters:**  1 **Input:**  /src\_compound\_id/\(to\_src\_id\) **Output:**  list of possible 'src\_id's for the query orphan src\_compound\_id, each one a key to a mapping between this 'orphan src\_compound\_id / src\_id' combination and other src\_compound\_ids and src\_ids. **Example:**  [https://www.ebi.ac.uk/unichem/rest/orphanIdMap/1234](https://www.ebi.ac.uk/unichem/rest/orphanIdMap/1234) **Example:**  [https://www.ebi.ac.uk/unichem/rest/orphanIdMap/AIN](https://www.ebi.ac.uk/unichem/rest/orphanIdMap/AIN) **Example:**  [https://www.ebi.ac.uk/unichem/rest/orphanIdMap/1234/1](https://www.ebi.ac.uk/unichem/rest/orphanIdMap/1234/1)

## Example cURL requests

The example cURL requests illustrate how the web services may be queried programmatically. In each case, the cURL request is shown, then the retrieved data.  
  
**Example 1: Retrieve Source information**

Retrieve information relating to the source 'ChEMBL' \(src\_id = 1\). Note that JSON is returned \(the default serialization method\). 

```text
curl https://www.ebi.ac.uk/unichem/rest/sources/1
[{"name":"chembl","description":"A database of bioactive drug-like small molecules and associated bioactivities abstracted from the scientific literature","name_long"  :"ChEMBL","base_id_url":"https://www.ebi.ac.uk/chembldb/compound/inspect/","src_id":"1","aux_for_url":"0","base_id_url_available":"1","name_label":"ChEMBL","src_url":"https://www.ebi.ac.uk/chembl/"}]

```

**Example 2: Retrieve Structure Information**

Retrieve the structure currently assigned to CHEMBL12 \(from src\_id = 1\). Note that JSON is returned \(the default serialization method\).

```text
curl https://www.ebi.ac.uk/unichem/rest/structure/CHEMBL12/1
[{"standardinchikey":"AAOVKJBEBIDNHE-UHFFFAOYSA-N","standardinchi":"InChI=1S/C16H13ClN2O/c1-19-14-8-7-12(17)9-13(14)16(18-10-15(19)20)11-5-3-2-4-6-11/h2-9H,10H2,1H3"}]
```

**Example 3: Retrieve JSONP**

Retrieve the structure currently assigned to CHEMBL12 \(from src\_id = 1\), as per example 2, but append a callback to return JSONP.

```text
curl https://www.ebi.ac.uk/unichem/rest/structure/CHEMBL12/1?callback=xyz
xyz([{"standardinchikey":"AAOVKJBEBIDNHE-UHFFFAOYSA-N","standardinchi":"InChI=1S/C16H13ClN2O/c1-19-14-8-7-12(17)9-13(14)16(18-10-15(19)20)11-5-3-2-4-6-11/h2-9H,10H2,1H3"}]);
```

**Example 4: Retrieve XML**

Retrieve the structure currently assigned to CHEMBL12 \(from src\_id = 1\), as per example 2, but set the 'Accept Header' to return XML.

```text
curl -H "Accept: text/xml" -H "Content-Type: text/xml" https://www.ebi.ac.uk/unichem/rest/structure/CHEMBL12/1
<opt\>
  <data standardinchi="InChI=1S/C16H13ClN2O/c1-19-14-8-7-12(17)9-13(14)16(18-10-15(19)20)11-5-3-2-4-6-11/h2-9H,10H2,1H3" standardinchikey="AAOVKJBEBIDNHE-UHFFFAOYSA-N" />
<opt\>
```

