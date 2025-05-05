Working in creation of SAP ABAP Notes 
Working in Odata file.
In future will upload all the concepts in SAP ABAP
OData - Open Data Protocol
Protocol - A set of rules defined to access specific data.
SAP also uses OData Service to transfer data to external systems through REST APIs.
CDS - Core Data Service(Set of domain specific language and services)
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
->Nested View
->Support annotaion a)odata with annotation b)Easy build FIORI app
->Support system variable
->Complex expression
->Extension
->SQL function possible.
->Can't be crated and edited in SAP GUI(Need to install eclipse or SAP HANA studio).
CDS CREATION
-> CDS can be created by either EDT(Eclipse Developmet Toll) or in HANA studio, Wd can't use SAP GUI for cration or modification of cds.
->Whenever we are created CDS there is 3 part - 1)DDL Editor 2)DDL source 3)ABAP Dictionary
->DDLS(Data Definition Language Source) object activated then - > SQL View + CDS entity (HANA View in DB) - we can transport the DDLS to another system - Why because DDL source name will be captured by TR. DDLS is responsible for checking the syntax and activating the code.
STEPS:
->Go to eclipse - package - Other ABAP repository object - search data definition - Give DDL source name - next - assign the TR - Finish ( It will ask to use any template)
-> Write a program - Define view <cds view name>
->If we are using template
@AbapCatalog.sqlViewName: 'zcds_view' "mandatory annotation
@AbapCatalog.compiler.compareFilter: true
@AbapCatalog.preserveKey: true
@AccessControl.authorizationCheck: #NOT_REQUIRED
@EndUserText.label: 'Data Definition'
@Metadata.ignorePropagatedAnnotations: true
define view zcds_dm as select from data_source_name
{
    key ebeln as EBELN,
    bukrs as BUKRS,
    lifnr as ELIFN,
    ekorg as EKORG,
    ekgrp as EKGRP
}
ZCDS_DM - cds entity name ,  zcds_view - sql name
alt+F8 - To open Transaction code 
->Once activated the cds view, we can able to view it in SE11, we can't rename the sql name as well as cds view name. If want to rename we have to delete the ddls and create new ddls
->check this zcds_view in database table , check this zcds_dm in view
-> To command the line on cds /* */ and ctrl+shift+< and use --
->keyward can be lower case, Upper case and camel case
->To get output press F8
->click sql console - it will give from which we are getting the data - ZCDS_DM (cds entity) name is used to get the data
->When we right click and click show SQL CREATE statement - It is used to find what query will be executedat the database level to create the database view
->Annotation - Extra information to CDS
->2 Kind of annotaion - 1)ABAP specific annotation - evaluated by runtime environmanet 2) Framework specific annotation - evaluated by the framework
->@EndUserText.label: 'Data Definition' - basic annotaion - endusertext.label - to give some meaningful text infromation or descriptions
->@AbapCatalog.preserveKey: true - whenever we are using the preserve key = true - whatever we have defined in the cds key fields should be the key fields
->Even we didn't the key word and preserve key - key field will automatically created in sql view by fetching the key field from the source table the key field will be assigned here my source table is ekko. If we don't want the key field from source table we can go with the preservekey annotation
->buffering - whenever we create classical view from our ddic based table , in cds view we can use the below annotation
@AbapCatalog.buffering: {
    status: #SWITCHED_OFF,
    type: #NONE,
    numberOfKeyFields: 000
}
-> Three type of status in buffering 1)Active 2)Not allowed 3)Switched off
-> Type of buffering - single record buffering , generic buffering , full record buffering , none
