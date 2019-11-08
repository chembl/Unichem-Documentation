# What is an Assignment?

 An 'Assignment' refers to the mapping of a src\_compound\_id to a particular structure in UniChem. Thus the src\_compound\_d 'CHEMBL2' is assigned to the InChI 'InChI=1S/C16H13ClN2O/c1-19-14-8-7-12\(17\)9-13\(14\)16\(18-10-15\(19\)20\)11-5-3-2-4-6-11/h2-9H,10H2,1H3' in UniChem.

 In the database, all assignments are classified as either 'current' \('1'\) or 'obsolete' \('0'\). A 'current' assignment means that this assignment exists in the most recently loaded data release from the source. An 'obsolete' assignment means that the most recent data release does not have this assignment, but an earlier release from the same source did make this assignment.

 When querying UniChem via the [Home / Search page](https://www.ebi.ac.uk/unichem/) the classifications of assignments are shown in the field 'Assigned in Latest Release'. If an assignment is current \('Yes', or '1' in the database\) then the adjacent field in the results table \('Last release when current'\) will display nothing. However, if the assignment is obsolete then this adjacent field will indicate the last data release when this assignment was current. This field may contain a date or a release version number, depending on the system used by the original source.

 Note that the terms 'Current/Obsolete Assignments' are distinct from 'Current/Obsolete src\_compound\_ids' \(as defined [here](what-is-meant-by-a-src_id-and-a-src_compound_id-in-unichem.md). \).

