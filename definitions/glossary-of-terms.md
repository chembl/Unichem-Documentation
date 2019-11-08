# Glossary of Terms

**Term:**  Source Data Release  
 **Description:**  \(SDR\) A data set obtained from a source, constituting all the current assignments in the source. Sometimes simply referred to as a 'Data Release'. Not to be confused with a UDR.  
  
**Term:**  src\_release\_number  
 **Description:**  A release number, as defined by the source, for a particular SDR. Each source is defined as having either a 'date' or a 'number' for identifying different SDRs.  
  
**Term:**  src\_release\_date  
 **Description:**  A release date, as obtained from the source, for a particular SDR. Each source is defined as having either a 'date' or a 'number' for identifying different SDRs.  
  
**Term:**  Release\_U  
 **Description:**  \(RU\) UniChem-generated integers \(One for each source\) incremented by 1 for each Data Load from that source. For example, if, for a given source, the CRU is 4 then a total of 4 SDRs have been loaded for this source.  
  
**Term:**  Current Release\_U  
**Description:**  \(CRU\) The current Release\_U for a particular source  
  
**Term:**  Data Load  
**Description:**  The process of adding a single 'Source Data Release' into UniChem.  
  
**Term:**  UniChem Load Index  
**Description:**  \(UC\_LOAD\_INDEX, or ULI\) A UniChem-generated integer incremented by 1 for each successful Data Load from any source. The current ULI therefore indicates the total number of separate Data Loads from all sources.  
  
**Term:**  UniChem Data Release  
**Description:**  \(UDR\) Data is loaded into UniChem in a 'production' instance of the database. After several data loads, a copy is made of this database and is made available to users. Each new UDR may therefore contain several additional ULI's compared to the last UDR  
  
**Term:**  UniChem Data Release Index  
**Description:**  \(UDRI\) An integer indicating the number of the UDR. Also called a 'UC\_RELEASE\_NUMBER', or 'UC Rel No.'  
  
**Term:**  Query Data Type  
**Description:**  \(QDT\) The permitted Data Types for querying UniChem. Four such Types exist: src\_id, src\_compound\_id, InChI and InChI Key. As defined [elsewhere](http://howe.ebi.ac.uk:3000/info/srcidExplain)  


