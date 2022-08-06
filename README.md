# SQLRPGLE_Tools
These HTML pages contain JavaScript and are intended to make life for the RPGLE programmer easier.

## XML_to_XMLTABLE.html
SQL provides a powerful function XMLTABLE to read XML documents as if they were ordinary table rows (or database records).
However, the coding is a cumbersome and errorprone activity, at least in my not so humble opinion.
So the JavaScript on this page tries to find the repeating element and generates a SQL statement that can be almost immediately used in ACS to read the XML file.

Copy a XML document into the left textarea, leave the field and find the generated SQL in the right textarea.

### known weaknesses
- [ ] generated column names are not necessarily unique. E.g. /Creditor/Id/BIC and /Debitor/Id/BIC both lead to the same column name Id_BIC.
- [ ] repeating elements at the end of the tree. E.g. 
```
<PstlAdr><AdrLine>Nowhere Street</AdrLine><AdrLine>4711 In Vain</AdrLine></PstlAdr> 
```
generates just one line:
```
 AdrLine   VARCHAR(80)  PATH('PstlAdr/AdrLine')
```
It should be 
```
 AdrLine1  VARCHAR(80)  PATH('PstlAdr/AdrLine[1]')
 AdrLine2  VARCHAR(80)  PATH('PstlAdr/AdrLine[2]')
```
 