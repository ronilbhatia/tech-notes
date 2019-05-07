# Nonrelational Databases

Nonrelational databases store information in **collections** and **documents** rather than tables and rows, as in relational databases. In some cases, information may be **embedded** in a document, where the associated information itself is stored in the document, whereas in others it may be **referenced** within the document, where the associated information is stored in a separate document, and a reference to that associated document's id is stored within the document. 

Information is likely to be embedded within a document if:
  * The information "belongs to" the document
  * The sub-document is small in size
  * The data from the entities are likely to be queried together
  * There is a one-to-one relationship relationship with the associated model

Typically embedded data models provide better *read* performance.

Information is likely to be referenced within a document if:
  * There is a many-to-many relationship with the associated model
  * The sub-document is likely to continue to increase in size or is large in size
  * Unbounded one-to-many relationships

Typically referenced data models provide better *write* performance.