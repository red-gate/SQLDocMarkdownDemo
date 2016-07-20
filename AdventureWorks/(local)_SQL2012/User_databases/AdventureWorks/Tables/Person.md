#### 

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Person.Person

# ![Tables](../../../../Images/Table32.png) [Person].[Person]

---

## <a name="#description"></a>MS_Description

Human beings involved with AdventureWorks: employees, customer contacts, and vendor contacts.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 19972 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:55 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Default | Description |
|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_Person_BusinessEntityID: BusinessEntityID](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_Person_BusinessEntity_BusinessEntityID: [Person].[BusinessEntity].BusinessEntityID](../../../../Images/fk.png)](#foreignkeys) | BusinessEntityID | int | 4 | NO |  | _Primary key for Person records._ |
| [![Check Constraints CK_Person_PersonType : ([PersonType] IS NULL OR upper([PersonType])='GC' OR upper([PersonType])='SP' OR upper([PersonType])='EM' OR upper([PersonType])='IN' OR upper([PersonType])='VC' OR upper([PersonType])='SC')](../../../../Images/c-constraint.png)](#checkconstraints) | PersonType | nchar(2) | 4 | NO |  | _Primary type of person: SC = Store Contact, IN = Individual (retail) customer, SP = Sales person, EM = Employee (non-sales), VC = Vendor contact, GC = General contact_ |
|  | NameStyle | [[dbo].[NameStyle]](../Programmability/Types/User-Defined_Data_Types/NameStyle.md) | 1 | NO | ((0)) | _0 = The data in FirstName and LastName are stored in western style (first name, last name) order.  1 = Eastern style (last name, first name) order._ |
|  | Title | nvarchar(8) | 16 | YES |  | _A courtesy title. For example, Mr. or Ms._ |
| [![Indexes IX_Person_LastName_FirstName_MiddleName](../../../../Images/Index.png)](#indexes) | FirstName | [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md) | 100 | NO |  | _First name of the person._ |
| [![Indexes IX_Person_LastName_FirstName_MiddleName](../../../../Images/Index.png)](#indexes) | MiddleName | [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md) | 100 | YES |  | _Middle name or middle initial of the person._ |
| [![Indexes IX_Person_LastName_FirstName_MiddleName](../../../../Images/Index.png)](#indexes) | LastName | [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md) | 100 | NO |  | _Last name of the person._ |
|  | Suffix | nvarchar(10) | 20 | YES |  | _Surname suffix. For example, Sr. or Jr._ |
| [![Check Constraints CK_Person_EmailPromotion : ([EmailPromotion]>=(0) AND [EmailPromotion]<=(2))](../../../../Images/c-constraint.png)](#checkconstraints) | EmailPromotion | int | 4 | NO | ((0)) | _0 = Contact does not wish to receive e-mail promotions, 1 = Contact does wish to receive e-mail promotions from AdventureWorks, 2 = Contact does wish to receive e-mail promotions from AdventureWorks and selected partners. _ |
| [![Indexes PXML_Person_AddContact](../../../../Images/Index.png)](#indexes) | AdditionalContactInfo | [xml([Person].[AdditionalContactInfoSchemaCollection])](../Programmability/Types/XML_Schema_Collections/AdditionalContactInfoSchemaCollection.md) | max | YES |  | _Additional contact information about the person stored in xml format. _ |
| [![Indexes PXML_Person_Demographics
XMLPATH_Person_Demographics
XMLPROPERTY_Person_Demographics
XMLVALUE_Person_Demographics](../../../../Images/Index.png)](#indexes)(4) | Demographics | [xml([Person].[IndividualSurveySchemaCollection])](../Programmability/Types/XML_Schema_Collections/IndividualSurveySchemaCollection.md) | max | YES |  | _Personal information such as hobbies, and income collected from online shoppers. Used for sales analysis._ |
| [![Indexes AK_Person_rowguid](../../../../Images/Index.png)](#indexes) | rowguid | uniqueidentifier | 16 | NO | (newid()) | _ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample._ |
|  | ModifiedDate | datetime | 8 | NO | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Type | Unique | XML Type | Description |
|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_Person_BusinessEntityID: BusinessEntityID](../../../../Images/pkcluster.png)](#indexes) | PK_Person_BusinessEntityID | BusinessEntityID |  | YES |  | _Primary key (clustered) constraint_ |
|  | AK_Person_rowguid | rowguid |  | YES |  | _Unique nonclustered index. Used to support replication samples._ |
|  | IX_Person_LastName_FirstName_MiddleName | LastName, FirstName, MiddleName |  |  |  |  |
|  | PXML_Person_AddContact | AdditionalContactInfo | xml |  | Primary | _Primary XML index._ |
|  | PXML_Person_Demographics | Demographics | xml |  | Primary | _Primary XML index._ |
|  | XMLPATH_Person_Demographics | Demographics | xml |  | Secondary | _Secondary XML index for path._ |
|  | XMLPROPERTY_Person_Demographics | Demographics | xml |  | Secondary | _Secondary XML index for property._ |
|  | XMLVALUE_Person_Demographics | Demographics | xml |  | Secondary | _Secondary XML index for value._ |


---

## <a name="#triggers"></a>Triggers

| Name | ANSI Nulls On | Quoted Identifier On | On | Not For Replication | Description |
|---|---|---|---|---|---|
| iuPerson | YES | YES | After Insert Update | YES | _AFTER INSERT, UPDATE trigger inserting Individual only if the Customer does not exist in the Store table and setting the ModifiedDate column in the Person table to the current date._ |


---

## <a name="#checkconstraints"></a>Check Constraints

| Name | On Column | Constraint | Description |
|---|---|---|---|
| CK_Person_EmailPromotion | EmailPromotion | ([EmailPromotion]>=(0) AND [EmailPromotion]<=(2)) | _Check constraint [EmailPromotion] >= (0) AND [EmailPromotion] <= (2)_ |
| CK_Person_PersonType | PersonType | ([PersonType] IS NULL OR upper([PersonType])='GC' OR upper([PersonType])='SP' OR upper([PersonType])='EM' OR upper([PersonType])='IN' OR upper([PersonType])='VC' OR upper([PersonType])='SC') | _Check constraint [PersonType] is one of SC, VC, IN, EM or SP._ |


---

## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_Person_BusinessEntity_BusinessEntityID | BusinessEntityID->[[Person].[BusinessEntity].[BusinessEntityID]](BusinessEntity.md) | _Foreign key constraint referencing BusinessEntity.BusinessEntityID._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Person].[Person]
(
[BusinessEntityID] [int] NOT NULL,
[PersonType] [nchar] (2) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[NameStyle] [dbo].[NameStyle] NOT NULL CONSTRAINT [DF_Person_NameStyle] DEFAULT ((0)),
[Title] [nvarchar] (8) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
[FirstName] [dbo].[Name] NOT NULL,
[MiddleName] [dbo].[Name] NULL,
[LastName] [dbo].[Name] NOT NULL,
[Suffix] [nvarchar] (10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
[EmailPromotion] [int] NOT NULL CONSTRAINT [DF_Person_EmailPromotion] DEFAULT ((0)),
[AdditionalContactInfo] [xml] (CONTENT [Person].[AdditionalContactInfoSchemaCollection]) NULL,
[Demographics] [xml] (CONTENT [Person].[IndividualSurveySchemaCollection]) NULL,
[rowguid] [uniqueidentifier] NOT NULL ROWGUIDCOL CONSTRAINT [DF_Person_rowguid] DEFAULT (newid()),
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_Person_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO

CREATE TRIGGER [Person].[iuPerson] ON [Person].[Person] 
AFTER INSERT, UPDATE NOT FOR REPLICATION AS 
BEGIN
    DECLARE @Count int;

    SET @Count = @@ROWCOUNT;
    IF @Count = 0 
        RETURN;

    SET NOCOUNT ON;

    IF UPDATE([BusinessEntityID]) OR UPDATE([Demographics]) 
    BEGIN
        UPDATE [Person].[Person] 
        SET [Person].[Person].[Demographics] = N'<IndividualSurvey xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/IndividualSurvey"> 
            <TotalPurchaseYTD>0.00</TotalPurchaseYTD> 
            </IndividualSurvey>' 
        FROM inserted 
        WHERE [Person].[Person].[BusinessEntityID] = inserted.[BusinessEntityID] 
            AND inserted.[Demographics] IS NULL;
        
        UPDATE [Person].[Person] 
        SET [Demographics].modify(N'declare default element namespace "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/IndividualSurvey"; 
            insert <TotalPurchaseYTD>0.00</TotalPurchaseYTD> 
            as first 
            into (/IndividualSurvey)[1]') 
        FROM inserted 
        WHERE [Person].[Person].[BusinessEntityID] = inserted.[BusinessEntityID] 
            AND inserted.[Demographics] IS NOT NULL 
            AND inserted.[Demographics].exist(N'declare default element namespace 
                "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/IndividualSurvey"; 
                /IndividualSurvey/TotalPurchaseYTD') <> 1;
    END;
END;
GO
ALTER TABLE [Person].[Person] ADD CONSTRAINT [CK_Person_EmailPromotion] CHECK (([EmailPromotion]>=(0) AND [EmailPromotion]<=(2)))
GO
ALTER TABLE [Person].[Person] ADD CONSTRAINT [CK_Person_PersonType] CHECK (([PersonType] IS NULL OR upper([PersonType])='GC' OR upper([PersonType])='SP' OR upper([PersonType])='EM' OR upper([PersonType])='IN' OR upper([PersonType])='VC' OR upper([PersonType])='SC'))
GO
ALTER TABLE [Person].[Person] ADD CONSTRAINT [PK_Person_BusinessEntityID] PRIMARY KEY CLUSTERED  ([BusinessEntityID]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_Person_LastName_FirstName_MiddleName] ON [Person].[Person] ([LastName], [FirstName], [MiddleName]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_Person_rowguid] ON [Person].[Person] ([rowguid]) ON [PRIMARY]
GO
CREATE PRIMARY XML INDEX [PXML_Person_AddContact]
ON [Person].[Person] ([AdditionalContactInfo])
GO
CREATE PRIMARY XML INDEX [PXML_Person_Demographics]
ON [Person].[Person] ([Demographics])
GO
CREATE XML INDEX [XMLPATH_Person_Demographics]
ON [Person].[Person] ([Demographics])
USING XML INDEX [PXML_Person_Demographics]
FOR PATH
GO
CREATE XML INDEX [XMLPROPERTY_Person_Demographics]
ON [Person].[Person] ([Demographics])
USING XML INDEX [PXML_Person_Demographics]
FOR PROPERTY
GO
CREATE XML INDEX [XMLVALUE_Person_Demographics]
ON [Person].[Person] ([Demographics])
USING XML INDEX [PXML_Person_Demographics]
FOR VALUE
GO
ALTER TABLE [Person].[Person] ADD CONSTRAINT [FK_Person_BusinessEntity_BusinessEntityID] FOREIGN KEY ([BusinessEntityID]) REFERENCES [Person].[BusinessEntity] ([BusinessEntityID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Human beings involved with AdventureWorks: employees, customer contacts, and vendor contacts.', 'SCHEMA', N'Person', 'TABLE', N'Person', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Additional contact information about the person stored in xml format. ', 'SCHEMA', N'Person', 'TABLE', N'Person', 'COLUMN', N'AdditionalContactInfo'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key for Person records.', 'SCHEMA', N'Person', 'TABLE', N'Person', 'COLUMN', N'BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Personal information such as hobbies, and income collected from online shoppers. Used for sales analysis.', 'SCHEMA', N'Person', 'TABLE', N'Person', 'COLUMN', N'Demographics'
GO
EXEC sp_addextendedproperty N'MS_Description', N'0 = Contact does not wish to receive e-mail promotions, 1 = Contact does wish to receive e-mail promotions from AdventureWorks, 2 = Contact does wish to receive e-mail promotions from AdventureWorks and selected partners. ', 'SCHEMA', N'Person', 'TABLE', N'Person', 'COLUMN', N'EmailPromotion'
GO
EXEC sp_addextendedproperty N'MS_Description', N'First name of the person.', 'SCHEMA', N'Person', 'TABLE', N'Person', 'COLUMN', N'FirstName'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Last name of the person.', 'SCHEMA', N'Person', 'TABLE', N'Person', 'COLUMN', N'LastName'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Middle name or middle initial of the person.', 'SCHEMA', N'Person', 'TABLE', N'Person', 'COLUMN', N'MiddleName'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Person', 'TABLE', N'Person', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'0 = The data in FirstName and LastName are stored in western style (first name, last name) order.  1 = Eastern style (last name, first name) order.', 'SCHEMA', N'Person', 'TABLE', N'Person', 'COLUMN', N'NameStyle'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary type of person: SC = Store Contact, IN = Individual (retail) customer, SP = Sales person, EM = Employee (non-sales), VC = Vendor contact, GC = General contact', 'SCHEMA', N'Person', 'TABLE', N'Person', 'COLUMN', N'PersonType'
GO
EXEC sp_addextendedproperty N'MS_Description', N'ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample.', 'SCHEMA', N'Person', 'TABLE', N'Person', 'COLUMN', N'rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Surname suffix. For example, Sr. or Jr.', 'SCHEMA', N'Person', 'TABLE', N'Person', 'COLUMN', N'Suffix'
GO
EXEC sp_addextendedproperty N'MS_Description', N'A courtesy title. For example, Mr. or Ms.', 'SCHEMA', N'Person', 'TABLE', N'Person', 'COLUMN', N'Title'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [EmailPromotion] >= (0) AND [EmailPromotion] <= (2)', 'SCHEMA', N'Person', 'TABLE', N'Person', 'CONSTRAINT', N'CK_Person_EmailPromotion'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [PersonType] is one of SC, VC, IN, EM or SP.', 'SCHEMA', N'Person', 'TABLE', N'Person', 'CONSTRAINT', N'CK_Person_PersonType'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 0', 'SCHEMA', N'Person', 'TABLE', N'Person', 'CONSTRAINT', N'DF_Person_EmailPromotion'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Person', 'TABLE', N'Person', 'CONSTRAINT', N'DF_Person_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 0', 'SCHEMA', N'Person', 'TABLE', N'Person', 'CONSTRAINT', N'DF_Person_NameStyle'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of NEWID()', 'SCHEMA', N'Person', 'TABLE', N'Person', 'CONSTRAINT', N'DF_Person_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing BusinessEntity.BusinessEntityID.', 'SCHEMA', N'Person', 'TABLE', N'Person', 'CONSTRAINT', N'FK_Person_BusinessEntity_BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Person', 'TABLE', N'Person', 'CONSTRAINT', N'PK_Person_BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index. Used to support replication samples.', 'SCHEMA', N'Person', 'TABLE', N'Person', 'INDEX', N'AK_Person_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Person', 'TABLE', N'Person', 'INDEX', N'PK_Person_BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary XML index.', 'SCHEMA', N'Person', 'TABLE', N'Person', 'INDEX', N'PXML_Person_AddContact'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary XML index.', 'SCHEMA', N'Person', 'TABLE', N'Person', 'INDEX', N'PXML_Person_Demographics'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Secondary XML index for path.', 'SCHEMA', N'Person', 'TABLE', N'Person', 'INDEX', N'XMLPATH_Person_Demographics'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Secondary XML index for property.', 'SCHEMA', N'Person', 'TABLE', N'Person', 'INDEX', N'XMLPROPERTY_Person_Demographics'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Secondary XML index for value.', 'SCHEMA', N'Person', 'TABLE', N'Person', 'INDEX', N'XMLVALUE_Person_Demographics'
GO
EXEC sp_addextendedproperty N'MS_Description', N'AFTER INSERT, UPDATE trigger inserting Individual only if the Customer does not exist in the Store table and setting the ModifiedDate column in the Person table to the current date.', 'SCHEMA', N'Person', 'TABLE', N'Person', 'TRIGGER', N'iuPerson'
GO

```


---

## <a name="#uses"></a>Uses

DEPENDENCYLIST* [[Person].[BusinessEntity]](BusinessEntity.md)
* [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md)
* [[dbo].[NameStyle]](../Programmability/Types/User-Defined_Data_Types/NameStyle.md)
* [Person](../Security/Schemas/Person.md)
* [[Person].[AdditionalContactInfoSchemaCollection]](../Programmability/Types/XML_Schema_Collections/AdditionalContactInfoSchemaCollection.md)
* [[Person].[IndividualSurveySchemaCollection]](../Programmability/Types/XML_Schema_Collections/IndividualSurveySchemaCollection.md)


---

## <a name="#usedby"></a>Used By

DEPENDENCYLIST* [[HumanResources].[Employee]](Employee.md)
* [[Person].[BusinessEntityContact]](BusinessEntityContact.md)
* [[Person].[EmailAddress]](EmailAddress.md)
* [[Person].[Password]](Password.md)
* [[Person].[PersonPhone]](PersonPhone.md)
* [[Sales].[Customer]](Customer.md)
* [[Sales].[PersonCreditCard]](PersonCreditCard.md)
* [[HumanResources].[vEmployee]](../Views/vEmployee.md)
* [[HumanResources].[vEmployeeDepartment]](../Views/vEmployeeDepartment.md)
* [[HumanResources].[vEmployeeDepartmentHistory]](../Views/vEmployeeDepartmentHistory.md)
* [[Person].[vAdditionalContactInfo]](../Views/vAdditionalContactInfo.md)
* [[Purchasing].[vVendorWithContacts]](../Views/vVendorWithContacts.md)
* [[Sales].[vIndividualCustomer]](../Views/vIndividualCustomer.md)
* [[Sales].[vPersonDemographics]](../Views/vPersonDemographics.md)
* [[Sales].[vSalesPerson]](../Views/vSalesPerson.md)
* [[Sales].[vSalesPersonSalesByFiscalYears]](../Views/vSalesPersonSalesByFiscalYears.md)
* [[Sales].[vStoreWithContacts]](../Views/vStoreWithContacts.md)
* [[dbo].[uspGetEmployeeManagers]](../Programmability/Stored_Procedures/uspGetEmployeeManagers.md)
* [[dbo].[uspGetManagerEmployees]](../Programmability/Stored_Procedures/uspGetManagerEmployees.md)
* [[dbo].[ufnGetContactInformation]](../Programmability/Functions/Table-valued_Functions/ufnGetContactInformation.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

