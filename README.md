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
->Even we didn't the key word and preserve key - key field will automatically created in sql view by fetching the key field from the source table. The key field will be assigned here my source table is ekko. If we don't want the key field from source table we can go with the preservekey annotation
->buffering annotation - whenever we create classical view from our ddic based table , in cds view we can use the below annotation
@AbapCatalog.buffering: {
    status: #SWITCHED_OFF,
    type: #NONE,
    numberOfKeyFields: 000
}
@AbapCatalog: {
    buffering: {
        status: #SWITCHED_OFF,
        type: #NONE,
        numberOfKeyFields: 000
    },
    dbHints: [{
        dbSystem: ,
        hint: ''
    }],
    viewEnhancementCategory: [  ],
    extensibility: {
        extensible: true,
        elementSuffix: '',
        quota: {
            maximumFields: ,
            maximumBytes: 
        },
        dataSources: [ '' ],
        allowNewDatasources: true,
        allowNewCompositions: true
    },
    sqlViewName: '',
    preserveKey: true,
    compiler: {
        compareFilter: true
    },
    dataMaintenance: #RESTRICTED,
    entityBuffer: {
        definitionAllowed: true,
        propagationAllowed: true
    }
}
-> Three type of status in buffering 1)Active 2)Not allowed 3)Switched off
-> Type of buffering - single record buffering , generic buffering , full record buffering , none
-> numberOfKeyFields: 000 - Till which key fields we want to buffer. Key fields should not have null values
->Whenever we are doing buffering it can't contain any another cds view/db view or table function
->Cds view can be created using parameters those also not be buffered
->Database Hint annotation - CDS are not specific to HANA database, CDS can be created in any database
@AbapCatalog.dbHints: [{

    dbSystem: #ADA, "which database we are going to be work with
    hint: ''
}]
->Whenever we execute any select statement and should take the secondary index and get the data faster but it was not possible in cds view , so we are having dbhint to use the particular key. It is not used in HANA but if we are using oracle or some other database we can use this dbhint
->ViewEnhancement Category: [ we can pass multiple values with comma separator]
->Whenever the sap develop the standard cds they give us option to extend the cds view - so we can create extended cds view along with our basic cds view.
->viewEnhancementCategory: [], 1)Group_by(Along with projection list we can use group by also, suppose cds view conatin aggregated functions like max,min.) 2)None(can't extend the particular cds view) 3)Projection_list(Whatever the select list we are using the number of field with additional fields can be used. If enhancement category is projection list then we can't enhance the particular cds view so we should have groupby along with projection list. So that we can add non-aggregated, aggregated fields) 4)Union(If union is not specified, then we can't enhance/extend the particular cds view those contain union having particular value and it used along with projection list)
->Compiler - comparefilter : true - When we create the association, based on one condition we are using the multiple condition and we can use cds view inside another cds view there also we have defined the same conditions. If we put the unnecessary condtions multiple time unknowingly that time we have to put comparefilter:ture  
->DEFINEVIEW ENTITY
@AbapCatalog.viewEnhancementCategory: [#NONE]
@AccessControl.authorizationCheck: #NOT_REQUIRED
@EndUserText.label: 'Data Definition'
@Metadata.ignorePropagatedAnnotations: true
@ObjectModel.usageType:{
    serviceQuality: #X,
    sizeCategory: #S,
    dataClass: #MIXED
}
define view entity Zcds_Dm as select from data_source_name
{
    
}
->DEFINEVIEW ENTITY WITH TO PARENT ASSOCIATION
@AccessControl.authorizationCheck: #NOT_REQUIRED
@EndUserText.label: 'Data Definition'
@Metadata.ignorePropagatedAnnotations: true
define view entity Zcds_Dm as select from data_source_name
association to parent target_data_source_name as _association_name
    on $projection.element_name = _association_name.target_element_name
{
    
    _association_name // Make association public
}
->DEFINE VIEW
@AbapCatalog.sqlViewName: ''
@AbapCatalog.compiler.compareFilter: true
@AbapCatalog.preserveKey: true
@AccessControl.authorizationCheck: #NOT_REQUIRED
@EndUserText.label: 'Data Definition'
@Metadata.ignorePropagatedAnnotations: true
define view Zcds_Dm as select from data_source_name
{
    
}
->Data maintenace annotation - similar to se11 1)Allowed(Not used in cds view) 2)Display only 3)Not allowed 4)Restricted
@AccessControl: {
    authorizationCheck: #NOT_REQUIRED,
    auditFilter: ,
    privilegedAssociations: [ '' ],
    auditing: {
        type: ,
        specification: ''
    },
    personalData: {
        blocking: ,
        blockingIndicator: [ '' ]
    },
    readAccess: {
        logging: {
            logdomain: [{
                area: '',
                domain: ''
            }],
            output: 
        }
    }
}
@AccessControl.authorizationCheck: #CHECK ,#Not_allowed, #Not_Required, #Previlieged_only
->Authority check - It will check particular cds can be access or not - we have dcl(Data control Language)
->To define DCL - right click data definition language - choose New access control(Who can access the particular cds)
->If we are defined in dcl and we are accessing particular cds in our select query that time it will check implicitly , if we have access to get the data or not from the cds based on that it will written the sy-subrc.
->If we didn't create the dcl, or created but didn't specify the role - syntax warning will come. In that case we can use @AccessControl.authorizationCheck: #Not_required (It will give the waring message work like check, if we didn't create the dcl).
->Second thing it will check whether it will written the @AccessControl.authorizationCheck: #CHECK over here.
->It will display if we have written the check over here
@AccessControl.authorizationCheck: #Not_allowed
->Even we defined the dcl or not, it doesn't matter. Because there will be no authority check performed whenever we access the particular cds view.
@AccessControl.authorizationCheck: #Previlieged_only
->It is defined by the SADL framework - it will check whether we have access for the particular cds view or not
@ClientHandling: {
type :
algorithm :
}
->Client Handling Annotation - 1)Type 2)Algorithm
1)Type - client dependent (atleast one table should be client dependent.one of the table in client dependent then the table will automatically become client dependent) and client independent all table should be client independent), Inherited(Derived from source table).
2)Algoritm(Once we deined the client dependent, how it should be handle when we use multiple table) - #Automated, #NONE, #Session_variable
->Automated and session_variable can be used along with inhertited or client dependent
->Automated - Whenever we use own condition automatically it will add the client in the own condition to compare the clients.It make cross join with T000 table having all the client
->None - Client independent 
->Session_variables - suppose we have 2 tables, one is client dependent and the other one is client independent it is difficult to add the own condtion, It will use the T000 table and automatically add the where condition in client dependent.So that it is preferrable to use session variable and also it is faster than automated. If we are getting the data from the normal table, if both are client dependent then there is no issue. 
->CDS View Entities Vs DDIC based View
**CDS VIEW ENTITIES:**
->7.55(In old version you don't get option to create)
->Define View Entity
->No additional DDIC based view created
->Improved performance during view activation
->Optimization and simplification of syntax
->@AbapCatalog.sqlViewName: '' annotaion is not available
->Name list are not supported
->Below annotation not required:
@AbapCatalog.compiler.compareFilter: true
@AbapCatalog.preserveKey: true
->Client handling takes place implicitly and doesn't require any development effort.
->Buffering annotation not supported.
**DDIC BASED CDS VIEW(absolute):**
->Whenever we try to access the cds view using DDIC we have 3 objects. 1) DDIC short name 2)CDS Entity 3)SQL View. bUt we never used the DDIC short name and Sql view anywhere. wherever we are using cds view We are using CDS entity. In select statement we have to use cds entity name or we are calling one cds in another also we are using cds entity.
->For the nameshake only are using sql name to display the view in se11, there is no use because we can't edit the entries.
->7.40 , SP05.
->DEFINE VIEW
->CDS Managed DDIC view created
->These are still supported to ensure downward compatibility.
->Define View is absolute - Reason: 
->Instead of Define View we are going wit Define View Entity
