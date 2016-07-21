#### asdasdasd

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Person.AddressType

# ![Tables](../../../../Images/Table32.png) [Person].[AddressType]

---

## <a name="#description"></a>MS_Description

Types of addresses stored in the Address table. 

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 6 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:53 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Identity | Default | Description |
|---|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_AddressType_AddressTypeID: AddressTypeID](../../../../Images/pkcluster.png)](#indexes) | AddressTypeID | int | 4 | NO | 1 - 1 |  | _Primary key for AddressType records._ |
| [![Indexes AK_AddressType_Name](../../../../Images/Index.png)](#indexes) | Name | [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md) | 100 | NO |  |  | _Address type description. For example, Billing, Home, or Shipping._ |
| [![Indexes AK_AddressType_rowguid](../../../../Images/Index.png)](#indexes) | rowguid | uniqueidentifier | 16 | NO |  | (newid()) | _ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample._ |
|  | ModifiedDate | datetime | 8 | NO |  | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_AddressType_AddressTypeID: AddressTypeID](../../../../Images/pkcluster.png)](#indexes) | PK_AddressType_AddressTypeID | AddressTypeID | YES | _Primary key (clustered) constraint_ |
|  | AK_AddressType_Name | Name | YES | _Unique nonclustered index._ |
|  | AK_AddressType_rowguid | rowguid | YES | _Unique nonclustered index. Used to support replication samples._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Person].[AddressType]
(
[AddressTypeID] [int] NOT NULL IDENTITY(1, 1),
[Name] [dbo].[Name] NOT NULL,
[rowguid] [uniqueidentifier] NOT NULL ROWGUIDCOL CONSTRAINT [DF_AddressType_rowguid] DEFAULT (newid()),
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_AddressType_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Person].[AddressType] ADD CONSTRAINT [PK_AddressType_AddressTypeID] PRIMARY KEY CLUSTERED  ([AddressTypeID]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_AddressType_Name] ON [Person].[AddressType] ([Name]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_AddressType_rowguid] ON [Person].[AddressType] ([rowguid]) ON [PRIMARY]
GO
EXEC sp_addextendedproperty N'MS_Description', N'Types of addresses stored in the Address table. ', 'SCHEMA', N'Person', 'TABLE', N'AddressType', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key for AddressType records.', 'SCHEMA', N'Person', 'TABLE', N'AddressType', 'COLUMN', N'AddressTypeID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Person', 'TABLE', N'AddressType', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Address type description. For example, Billing, Home, or Shipping.', 'SCHEMA', N'Person', 'TABLE', N'AddressType', 'COLUMN', N'Name'
GO
EXEC sp_addextendedproperty N'MS_Description', N'ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample.', 'SCHEMA', N'Person', 'TABLE', N'AddressType', 'COLUMN', N'rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Person', 'TABLE', N'AddressType', 'CONSTRAINT', N'DF_AddressType_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of NEWID()', 'SCHEMA', N'Person', 'TABLE', N'AddressType', 'CONSTRAINT', N'DF_AddressType_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Person', 'TABLE', N'AddressType', 'CONSTRAINT', N'PK_AddressType_AddressTypeID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index.', 'SCHEMA', N'Person', 'TABLE', N'AddressType', 'INDEX', N'AK_AddressType_Name'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index. Used to support replication samples.', 'SCHEMA', N'Person', 'TABLE', N'AddressType', 'INDEX', N'AK_AddressType_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Person', 'TABLE', N'AddressType', 'INDEX', N'PK_AddressType_AddressTypeID'
GO

```


---

## <a name="#uses"></a>Uses

* [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md)
* [Person](../Security/Schemas/Person.md)


---

## <a name="#usedby"></a>Used By

* [[Person].[BusinessEntityAddress]](BusinessEntityAddress.md)
* [[Purchasing].[vVendorWithAddresses]](../Views/vVendorWithAddresses.md)
* [[Sales].[vIndividualCustomer]](../Views/vIndividualCustomer.md)
* [[Sales].[vStoreWithAddresses]](../Views/vStoreWithAddresses.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 14:15

