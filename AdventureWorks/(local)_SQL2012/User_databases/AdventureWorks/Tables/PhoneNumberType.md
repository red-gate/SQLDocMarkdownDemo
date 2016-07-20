#### 

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Person.PhoneNumberType

# ![Tables](../../../../Images/Table32.png) [Person].[PhoneNumberType]

---

## <a name="#description"></a>MS_Description

Type of phone number of a person.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 3 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:54 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Identity | Default | Description |
|---|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_PhoneNumberType_PhoneNumberTypeID: PhoneNumberTypeID](../../../../Images/pkcluster.png)](#indexes) | PhoneNumberTypeID | int | 4 | NO | 1 - 1 |  | _Primary key for telephone number type records._ |
|  | Name | [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md) | 100 | NO |  |  | _Name of the telephone number type_ |
|  | ModifiedDate | datetime | 8 | NO |  | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_PhoneNumberType_PhoneNumberTypeID: PhoneNumberTypeID](../../../../Images/pkcluster.png)](#indexes) | PK_PhoneNumberType_PhoneNumberTypeID | PhoneNumberTypeID | YES | _Primary key (clustered) constraint_ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Person].[PhoneNumberType]
(
[PhoneNumberTypeID] [int] NOT NULL IDENTITY(1, 1),
[Name] [dbo].[Name] NOT NULL,
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_PhoneNumberType_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Person].[PhoneNumberType] ADD CONSTRAINT [PK_PhoneNumberType_PhoneNumberTypeID] PRIMARY KEY CLUSTERED  ([PhoneNumberTypeID]) ON [PRIMARY]
GO
EXEC sp_addextendedproperty N'MS_Description', N'Type of phone number of a person.', 'SCHEMA', N'Person', 'TABLE', N'PhoneNumberType', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Person', 'TABLE', N'PhoneNumberType', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Name of the telephone number type', 'SCHEMA', N'Person', 'TABLE', N'PhoneNumberType', 'COLUMN', N'Name'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key for telephone number type records.', 'SCHEMA', N'Person', 'TABLE', N'PhoneNumberType', 'COLUMN', N'PhoneNumberTypeID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Person', 'TABLE', N'PhoneNumberType', 'CONSTRAINT', N'DF_PhoneNumberType_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Person', 'TABLE', N'PhoneNumberType', 'CONSTRAINT', N'PK_PhoneNumberType_PhoneNumberTypeID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Person', 'TABLE', N'PhoneNumberType', 'INDEX', N'PK_PhoneNumberType_PhoneNumberTypeID'
GO

```


---

## <a name="#uses"></a>Uses

DEPENDENCYLIST* [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md)
* [Person](../Security/Schemas/Person.md)


---

## <a name="#usedby"></a>Used By

DEPENDENCYLIST* [[Person].[PersonPhone]](PersonPhone.md)
* [[HumanResources].[vEmployee]](../Views/vEmployee.md)
* [[Purchasing].[vVendorWithContacts]](../Views/vVendorWithContacts.md)
* [[Sales].[vIndividualCustomer]](../Views/vIndividualCustomer.md)
* [[Sales].[vSalesPerson]](../Views/vSalesPerson.md)
* [[Sales].[vStoreWithContacts]](../Views/vStoreWithContacts.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

