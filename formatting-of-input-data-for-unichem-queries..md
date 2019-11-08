# Formatting of input data for UniChem queries.

 Below are some simple tips for reviewing your query strings for the correct formatting

####  **src\_compound\_id**

 src\_compound\_ids are treated in a case sensitive manner. For example, querying with 'chembl123' instead of 'CHEMBL123' will return nothing, as the lower-case form is currently not a valid ChEMBL id.

 This distinction is made in UniChem to account for the possibility that a source may change the case in an src\_compound\_id from one release to another: UniChem must distinguish between these to indicate the current and obsolete versions to the user.

####  **src\_id**

 src\_ids are integers.

####  **InChIs and InChIKeys**

Standard InChIs in UniChem are calculated with version 1 of the IUPAC International Chemical Identifier \(InChI\) generation software. Full detailed information of the format of valid Standard InChIs and InChIKeys using this software may be found [here](http://old.iupac.org/inchi/release102final.html) . Below are some simple first pass checks you can do before consulting the more detailed documentation cited in the above link.

####  **Standard InChIs**

Standard InChIs in UniChem should always begin with "**InChI=1S/".**

Thus, for example, the following ****string is a valid Standard InChi in UniChem.: ****

* **InChI=1S/C2H6O/c1-2-3/h3H,2H2,1H3**

####  **Standard InChIKeys**

 Standard InChIKeys should always follow the following 27-character format...

*  **XXXXXXXXXXXXXX-XXXXXXXXSA-X**
  *  X is any uppercase letter
  * The two hyphens separate three blocks of 14, 10 and 1 uppercase letters respectively. 
  * 'SA' in positions 9 and 10 of the second block signifies that this is a key for a Standard \('S'\) Inchi, generated using version 1 \('A'\) of the InChI software

Thus, for example, the following string is a valid Standard InChiKey in UniChem:

* LFQSCWFLJHTTHZ-UHFFFAOYSA-N

####  **Web Interface Queries**

* Enter plain text only into the query field. 
* New-lines and/or white space may be used to separate entries. 
* Remove all other non-printing special characters.
* Note that querying with src\_compound\_ids requires additional information:
  * The src\_id for the source of the src\_compound\_id's.
  * An indication of whether query src\_compound\_ids with 'obsolete' assignments should be included in the query \(go [here](https://www.ebi.ac.uk/unichem/info/obsoleteIncExplain) for a more detailed explanation of this option\).
  * It is recommended that normally users will probably NOT wish to have this option ticked.
* Note, also, that for large queries the output may difficult to interpret, and slow to load in your browser. For larger queries, therefore, users are strongly advised to use the [web services](https://www.ebi.ac.uk/unichem/info/webservices) instead.   

