Working in creation of SAP ABAP Notes 
Working in Odata file.
In future will upload all the concepts in SAP ABAP
OData - Open Data Protocol
Protocol - A set of rules defined to access specific data.
SAP also uses OData Service to transfer data to external systems through REST APIs.
CDS - Core Data Service(Set of domain soecific language and services)
=>Sap hana supports sql to define mainupulate and consume the data from the database - On top we have odata, bobf, business intelligent edm, etc use to create the higher level data models on its own.
=> We are having different technologies to maintain data models , so to overcome and maintain in common technologies we are going with CDS.
=>Set of domain specific languages and services, called CDS, for defining and consuming semantically rich data models.
=>Domain specific languages/ data definition language/data query language/data control language and services - DDL, DQL, DCL.
a)Data Definition language is the enhancement of sql - Define semantically rich database tables and the views- Called CDS entity - We can call the entity in another CDS as well or in our select query as well.
b)Data Control language - Whatever the entity defined using data definition language, we can give the authorization to that particular cds entity using the data query language or data control language
=>Semantically rich data models - Annotations, Expression, Association.
a)Not only table having the relationship, If we are using CDS in FIORI application - What will be the description of the fields will be displayed on the FIORI application. What is the F4 help related to the particular field, How we can filter further the particular field - All the information will be embedded in the cds.Simply, we can use the annotation to add the infromation.
b)Not only annotation to add information on particular field, but also we can do expression if we want any calculation and we can join the table using association(on-demand).
=>There are 2 flavors of CDS - 1)ABAP CDS 2)HANA CDS.
1)ABAP CDS
->ABAP application server
->It's Open SQL(It suuport in all os - linux,oracle)
->Developed by ABAPer
->It's a part of DDIC
->Support ABAP application
2)HANA CDS
->HANA XS
->SAP HANA only(Native Only - support only sap)
->Developed by native developer
->It's not a part of data dictionary
->Supports HANA application
=>Difference between classical view and CDS view
Classical View:
->It doesn't follow the code push
->No outer join
->No union
->No input parameter
->Not supported
->No annotaion
~We have to use SEGW
~We ahve to use JS
->SQL fucntion not possible.
->We can create in  SAP GUI and edit it.
CDS View:
->Code push down follow(Whatever we are executing, we can run the complex logic everything in the database level).
->Outer join possible.
->union is possible.
->Input parameter to filter data
->Nestes View
->Support annotaion a)odata with annotation b)Easy build FIORI app
->Support system variable
->Complex expression
->Extension
->SQL function possible.
->Can't be crated and edited in SAP GUI(Need to install eclipse or SAP HANA studio).
