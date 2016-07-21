#### asdasdasd

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Person.PersonPhone

# ![Tables](../../../../Images/Table32.png) [Person].[PersonPhone]

---

## <a name="#description"></a>MS_Description

Telephone number and type of a person.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 19972 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:54 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Default | Description |
|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_PersonPhone_BusinessEntityID_PhoneNumber_PhoneNumberTypeID: BusinessEntityID\PhoneNumber\PhoneNumberTypeID](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_PersonPhone_Person_BusinessEntityID: [Person].[Person].BusinessEntityID](../../../../Images/fk.png)](#foreignkeys) | BusinessEntityID | int | 4 | NO |  | _Business entity identification number. Foreign key to Person.BusinessEntityID._ |
| [![Cluster Primary Key PK_PersonPhone_BusinessEntityID_PhoneNumber_PhoneNumberTypeID: BusinessEntityID\PhoneNumber\PhoneNumberTypeID](../../../../Images/pkcluster.png)](#indexes)[![Indexes IX_PersonPhone_PhoneNumber](../../../../Images/Index.png)](#indexes) | PhoneNumber | [[dbo].[Phone]](../Programmability/Types/User-Defined_Data_Types/Phone.md) | 50 | NO |  | _Telephone number identification number._ |
| [![Cluster Primary Key PK_PersonPhone_BusinessEntityID_PhoneNumber_PhoneNumberTypeID: BusinessEntityID\PhoneNumber\PhoneNumberTypeID](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_PersonPhone_PhoneNumberType_PhoneNumberTypeID: [Person].[PhoneNumberType].PhoneNumberTypeID](../../../../Images/fk.png)](#foreignkeys) | PhoneNumberTypeID | int | 4 | NO |  | _Kind of phone number. Foreign key to PhoneNumberType.PhoneNumberTypeID._ |
|  | ModifiedDate | datetime | 8 | NO | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_PersonPhone_BusinessEntityID_PhoneNumber_PhoneNumberTypeID: BusinessEntityID\PhoneNumber\PhoneNumberTypeID](../../../../Images/pkcluster.png)](#indexes) | PK_PersonPhone_BusinessEntityID_PhoneNumber_PhoneNumberTypeID | BusinessEntityID, PhoneNumber, PhoneNumberTypeID | YES | _Primary key (clustered) constraint_ |
|  | IX_PersonPhone_PhoneNumber | PhoneNumber |  | _Nonclustered index._ |


---

## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_PersonPhone_Person_BusinessEntityID | BusinessEntityID->[[Person].[Person].[BusinessEntityID]](Person.md) | _Foreign key constraint referencing Person.BusinessEntityID._ |
| FK_PersonPhone_PhoneNumberType_PhoneNumberTypeID | PhoneNumberTypeID->[[Person].[PhoneNumberType].[PhoneNumberTypeID]](PhoneNumberType.md) | _Foreign key constraint referencing PhoneNumberType.PhoneNumberTypeID._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Person].[PersonPhone]
(
[BusinessEntityID] [int] NOT NULL,
[PhoneNumber] [dbo].[Phone] NOT NULL,
[PhoneNumberTypeID] [int] NOT NULL,
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_PersonPhone_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Person].[PersonPhone] ADD CONSTRAINT [PK_PersonPhone_BusinessEntityID_PhoneNumber_PhoneNumberTypeID] PRIMARY KEY CLUSTERED  ([BusinessEntityID], [PhoneNumber], [PhoneNumberTypeID]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_PersonPhone_PhoneNumber] ON [Person].[PersonPhone] ([PhoneNumber]) ON [PRIMARY]
GO
ALTER TABLE [Person].[PersonPhone] ADD CONSTRAINT [FK_PersonPhone_Person_BusinessEntityID] FOREIGN KEY ([BusinessEntityID]) REFERENCES [Person].[Person] ([BusinessEntityID])
GO
ALTER TABLE [Person].[PersonPhone] ADD CONSTRAINT [FK_PersonPhone_PhoneNumberType_PhoneNumberTypeID] FOREIGN KEY ([PhoneNumberTypeID]) REFERENCES [Person].[PhoneNumberType] ([PhoneNumberTypeID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Telephone number and type of a person.', 'SCHEMA', N'Person', 'TABLE', N'PersonPhone', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Business entity identification number. Foreign key to Person.BusinessEntityID.', 'SCHEMA', N'Person', 'TABLE', N'PersonPhone', 'COLUMN', N'BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Person', 'TABLE', N'PersonPhone', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Telephone number identification number.', 'SCHEMA', N'Person', 'TABLE', N'PersonPhone', 'COLUMN', N'PhoneNumber'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Kind of phone number. Foreign key to PhoneNumberType.PhoneNumberTypeID.', 'SCHEMA', N'Person', 'TABLE', N'PersonPhone', 'COLUMN', N'PhoneNumberTypeID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Person', 'TABLE', N'PersonPhone', 'CONSTRAINT', N'DF_PersonPhone_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Person.BusinessEntityID.', 'SCHEMA', N'Person', 'TABLE', N'PersonPhone', 'CONSTRAINT', N'FK_PersonPhone_Person_BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing PhoneNumberType.PhoneNumberTypeID.', 'SCHEMA', N'Person', 'TABLE', N'PersonPhone', 'CONSTRAINT', N'FK_PersonPhone_PhoneNumberType_PhoneNumberTypeID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Person', 'TABLE', N'PersonPhone', 'CONSTRAINT', N'PK_PersonPhone_BusinessEntityID_PhoneNumber_PhoneNumberTypeID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Nonclustered index.', 'SCHEMA', N'Person', 'TABLE', N'PersonPhone', 'INDEX', N'IX_PersonPhone_PhoneNumber'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Person', 'TABLE', N'PersonPhone', 'INDEX', N'PK_PersonPhone_BusinessEntityID_PhoneNumber_PhoneNumberTypeID'
GO

```


---

## <a name="#uses"></a>Uses

* [[Person].[Person]](Person.md)
* [[Person].[PhoneNumberType]](PhoneNumberType.md)
* [[dbo].[Phone]](../Programmability/Types/User-Defined_Data_Types/Phone.md)
* [Person](../Security/Schemas/Person.md)


---

## <a name="#usedby"></a>Used By

* [[HumanResources].[vEmployee]](../Views/vEmployee.md)
* [[Purchasing].[vVendorWithContacts]](../Views/vVendorWithContacts.md)
* [[Sales].[vIndividualCustomer]](../Views/vIndividualCustomer.md)
* [[Sales].[vSalesPerson]](../Views/vSalesPerson.md)
* [[Sales].[vStoreWithContacts]](../Views/vStoreWithContacts.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 14:15

