# What is meant by a 'src\_id' and a 'src\_compound\_id' in UniChem ?

##  src\_id

 src\_ids are integers that are unique identifiers for sources in UniChem. A list of valid src\_id's can be found either on the [sources](https://www.ebi.ac.uk/unichem/ucquery/listSources) page or by using the [web services](https://www.ebi.ac.uk/unichem/info/webservices).

##  src\_compound\_id

 src\_compound\_ids are the individual compound identifiers provided by each of the sources. For example 'CHEMBL12' is a src\_compound\_id from the 'chembl' source \(src\_id = 1\). Since src\_compound\_ids may be ambiguous across different sources, querying UniChem with a src\_compound\_id also requires the specification of a corresponding src\_id. src\_compound\_ids are dealt with in a case sensitive manner, as explained [here](https://www.ebi.ac.uk/unichem/info/inputFormats).

##  'Current' vrs 'Obsolete' src\_compound\_id's.

 All src\_compound\_ids for a source may be classified as either 'Current' or 'Obsolete'...  
  
  **'Current src\_compound\_id'** = a src\_compound\_id which is currently assigned to one or more structures.  
  **'Obsolete src\_compound\_id'** = a src\_compound\_id that is NOT currently assigned any structures.  
  
 Clearly, for an 'Obsolete src\_compound\_id' to exist within UniChem it must have been assigned to a structure in at least one previous data releases from the source, but in the most recent release from the source it is absent. Note that these definitions are distinct from the [definitions of 'Current and Obsolete Assignments'](https://www.ebi.ac.uk/unichem/info/assignmentExplain).  
  
 Thus, for example, a given src\_compound\_id may have an 'Obsolete Assignment' to structure X, but the src\_compound\_id itself may be 'Current', because it is 'Currently Assigned' to structure Y. Another src\_compound\_id may also have an 'Obsolete Assignment' to structure X, and the src\_compound\_id itself may also be 'Obsolete', simply because it is not assigned to any structure in the most recent release \(ie: it has no current assignment\).

 Using the 'Include non-mapped src\_compound\_ids' option on the [Whole source mapping page](https://www.ebi.ac.uk/unichem/wholesourcemap). will return both Current and Obsolete src\_compound\_ids, as explained [here](https://www.ebi.ac.uk/unichem/info/includeExplain).

