# Rules for Loading

 During the loading process some records are omitted for various reasons. These reasons are listed below.

 A record is not loaded if any of the following apply:

| Rule | Description |
| :--- | :--- |
| 1 | There is a mis-match between the InChI and the InChIkey. \(\*\) |
| 2 | The source does not provide a Standard InChI. \(\*\*\) |
| 3 | UniChem cannot generate an InChIkey from the Standard InChI provided by the source. |
| 4 | The source does not provide an ID for the structure. |
| 5 | The Standard InChI supplied is greater than 2000 characters long. |
| 6 | The auxilliary data is absent, or greater than 4000 characters long \(\*\*\*\) |

 \* = In other words, where the InChIKey calculated by UniChem from the InChI provided by the source does not exactly match the InChIKey provided by the source. Note, however, if the InChIKey is completely absent \(ie: not provided by the source\), then UniChem will calculate an InChIKey, and the record loaded with this calculated key \(although UniChem will note this absence in a 'comment'\).  
  
 \*\* = However, if the source only provides Molfiles rather than Standard InChIs, then UniChem will generate Standard InChIs instead. Currently, this has only been done for a limited number of sources \[see the [sources](https://www.ebi.ac.uk/unichem/ucquery/listSources) page to see which ones\]\).  
  
 \*\*\* = Clearly, this only applies to the limited number of sources that require auxilliary information. Go [here](https://www.ebi.ac.uk/unichem/info/faq#faq13) to find out what auxilliary information is.

