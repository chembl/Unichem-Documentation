# Mappings

### **Auxiliary Data Mappings**

Most sources within UniChem create URLs for compound specific pages by simply appending a src\_compound\_id to a ‘base URL’.

For example, appending the ChEMBL src\_compound\_id **'CHEMBL59'** onto 'https://www.ebi.ac.uk**/chembldb/compound/inspect/'** will give **https://www.ebi.ac.uk/chembldb/compound/inspect/CHEMBL59'**, the compound-specific page in ChEMBL for this compound.

However, some instances of UniChem may contain sources that create URLs for compound-specific pages by using strings or identifiers \(called 'auxiliary data' here\) that are different to the src\_compound\_ids for the source. This is not very common, but is dealt with in UniChem by use of an additional mapping step for these sources, which can be achieved on this page.

Currently there is only 1 source in UniChem with auxiliary data.

### Whole Source Mappings

 UniChem can be used to create full mappings between different sources.

 Previously, these mappings could be retrieved from this page, but now these are located on the UniChem FTP site...

 [ftp://ftp.ebi.ac.uk/pub/databases/chembl/UniChem/data/wholeSourceMapping/](ftp://ftp.ebi.ac.uk/pub/databases/chembl/UniChem/data/wholeSourceMapping/)

