# What does the option 'Include non-mapped src\_compound\_ids' mean with respect to whole source mapping

The default option for whole source mapping is to 'Exclude' non-mapped 'From' src\_compound\_ids. Thus the default output simply gives a mapping of all currently assigned src\_compound\_ids in the 'From' source that happen to share a structure with a src\_compound\_id \(that is also currently assigned to this structure\) in the 'To' source. This output is normally all that is required for routine mapping purposes, such as the creation of upto date hyperlinks between the two sources.

However, some users \(typically, data managers of resources containing smaller sets of src\_compound\_ids\) have specifically asked to have the option of being able to modify the output to include \(in addition to all the data that is provided by the 'Exclude' option\) all 'non-mapped' src\_compound\_ids from the 'From' source in the output, including both current and obsolete src\_compound\_ids \(see \* below\). This form of output assists efforts to curate and manually maintain links from \(usually smaller\) sources to other sources by allowing the user to more conveniently see what src\_compound\_ids are currently not mapped \(when perhaps they should be\) and which may therefore require further curation within their own resource. In this way, UniChem is being used as an aid to curation. Selecting the 'Include' option allows these users to do this.

Since the output for the 'Include' option contains a number of different kinds of data, it is useful to clarify how these will appear in the output:

* **Mapped src\_compound\_ids** will appear as per the 'Exclude' option \(ie: with the corresponding 'To' src\_compound\_id in the second column\).
* **Non-mapped 'Current src-compound\_ids'** will appear with a 'null' in the second column.
* **Non-mapped 'Obsolete src-compound\_ids'** will appear with a 'Obsolete src\_compound\_id' in the second column.

 Note that although the list of 'From' src-compound\_ids in the output is complete \(ie: all src\_compound\_ids are present\), it is not necessarily non-redundant, as mapped src\_compound\_ids may have multiple mappings to the 'To' source.

 Unfortunately, the use of the 'Include' option may result in very significantly larger mapping files than the equivalent sets using the 'Exclude' option. For some very large sources this would produce extremely large outputs, which would be unlikely to be of value to any users. For this reason, the use of this option is limited to 'From' sources below a certain size. The current limit is set to '30000'. Queries using the 'Include' option with 'From' sources containing more that this number of currently assigned src\_compound\_ids are prohibitted.

####  **Notes.**

 \* Note that the terms 'Current/Obsolete src\_compound\_id' \(defined [here](https://www.ebi.ac.uk/unichem/info/srcidExplain). \) are distinct from 'Current/Obsolete Assignments' \(defined [here](https://www.ebi.ac.uk/unichem/info/assignmentExplain) \).

