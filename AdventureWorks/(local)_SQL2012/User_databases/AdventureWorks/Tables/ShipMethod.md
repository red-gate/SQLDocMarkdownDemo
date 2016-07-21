#### asdasdasd

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Purchasing.ShipMethod

# ![Tables](../../../../Images/Table32.png) [Purchasing].[ShipMethod]

---

## <a name="#description"></a>MS_Description

Shipping company lookup table.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 5 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:54 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Identity | Default | Description |
|---|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_ShipMethod_ShipMethodID: ShipMethodID](../../../../Images/pkcluster.png)](#indexes) | ShipMethodID | int | 4 | NO | 1 - 1 |  | _Primary key for ShipMethod records._ |
| [![Indexes AK_ShipMethod_Name](../../../../Images/Index.png)](#indexes) | Name | [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md) | 100 | NO |  |  | _Shipping company name._ |
| [![Check Constraints CK_ShipMethod_ShipBase : ([ShipBase]>(0.00))](../../../../Images/c-constraint.png)](#checkconstraints) | ShipBase | money | 8 | NO |  | ((0.00)) | _Minimum shipping charge._ |
| [![Check Constraints CK_ShipMethod_ShipRate : ([ShipRate]>(0.00))](../../../../Images/c-constraint.png)](#checkconstraints) | ShipRate | money | 8 | NO |  | ((0.00)) | _Shipping charge per pound._ |
| [![Indexes AK_ShipMethod_rowguid](../../../../Images/Index.png)](#indexes) | rowguid | uniqueidentifier | 16 | NO |  | (newid()) | _ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample._ |
|  | ModifiedDate | datetime | 8 | NO |  | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_ShipMethod_ShipMethodID: ShipMethodID](../../../../Images/pkcluster.png)](#indexes) | PK_ShipMethod_ShipMethodID | ShipMethodID | YES | _Primary key (clustered) constraint_ |
|  | AK_ShipMethod_Name | Name | YES | _Unique nonclustered index._ |
|  | AK_ShipMethod_rowguid | rowguid | YES | _Unique nonclustered index. Used to support replication samples._ |


---

## <a name="#checkconstraints"></a>Check Constraints

| Name | On Column | Constraint | Description |
|---|---|---|---|
| CK_ShipMethod_ShipBase | ShipBase | ([ShipBase]>(0.00)) | _Check constraint [ShipBase] > (0.00)_ |
| CK_ShipMethod_ShipRate | ShipRate | ([ShipRate]>(0.00)) | _Check constraint [ShipRate] > (0.00)_ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Purchasing].[ShipMethod]
(
[ShipMethodID] [int] NOT NULL IDENTITY(1, 1),
[Name] [dbo].[Name] NOT NULL,
[ShipBase] [money] NOT NULL CONSTRAINT [DF_ShipMethod_ShipBase] DEFAULT ((0.00)),
[ShipRate] [money] NOT NULL CONSTRAINT [DF_ShipMethod_ShipRate] DEFAULT ((0.00)),
[rowguid] [uniqueidentifier] NOT NULL ROWGUIDCOL CONSTRAINT [DF_ShipMethod_rowguid] DEFAULT (newid()),
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_ShipMethod_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Purchasing].[ShipMethod] ADD CONSTRAINT [CK_ShipMethod_ShipBase] CHECK (([ShipBase]>(0.00)))
GO
ALTER TABLE [Purchasing].[ShipMethod] ADD CONSTRAINT [CK_ShipMethod_ShipRate] CHECK (([ShipRate]>(0.00)))
GO
ALTER TABLE [Purchasing].[ShipMethod] ADD CONSTRAINT [PK_ShipMethod_ShipMethodID] PRIMARY KEY CLUSTERED  ([ShipMethodID]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_ShipMethod_Name] ON [Purchasing].[ShipMethod] ([Name]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_ShipMethod_rowguid] ON [Purchasing].[ShipMethod] ([rowguid]) ON [PRIMARY]
GO
EXEC sp_addextendedproperty N'MS_Description', N'Shipping company lookup table.', 'SCHEMA', N'Purchasing', 'TABLE', N'ShipMethod', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Purchasing', 'TABLE', N'ShipMethod', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Shipping company name.', 'SCHEMA', N'Purchasing', 'TABLE', N'ShipMethod', 'COLUMN', N'Name'
GO
EXEC sp_addextendedproperty N'MS_Description', N'ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample.', 'SCHEMA', N'Purchasing', 'TABLE', N'ShipMethod', 'COLUMN', N'rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Minimum shipping charge.', 'SCHEMA', N'Purchasing', 'TABLE', N'ShipMethod', 'COLUMN', N'ShipBase'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key for ShipMethod records.', 'SCHEMA', N'Purchasing', 'TABLE', N'ShipMethod', 'COLUMN', N'ShipMethodID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Shipping charge per pound.', 'SCHEMA', N'Purchasing', 'TABLE', N'ShipMethod', 'COLUMN', N'ShipRate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [ShipBase] > (0.00)', 'SCHEMA', N'Purchasing', 'TABLE', N'ShipMethod', 'CONSTRAINT', N'CK_ShipMethod_ShipBase'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [ShipRate] > (0.00)', 'SCHEMA', N'Purchasing', 'TABLE', N'ShipMethod', 'CONSTRAINT', N'CK_ShipMethod_ShipRate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Purchasing', 'TABLE', N'ShipMethod', 'CONSTRAINT', N'DF_ShipMethod_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of NEWID()', 'SCHEMA', N'Purchasing', 'TABLE', N'ShipMethod', 'CONSTRAINT', N'DF_ShipMethod_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 0.0', 'SCHEMA', N'Purchasing', 'TABLE', N'ShipMethod', 'CONSTRAINT', N'DF_ShipMethod_ShipBase'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 0.0', 'SCHEMA', N'Purchasing', 'TABLE', N'ShipMethod', 'CONSTRAINT', N'DF_ShipMethod_ShipRate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Purchasing', 'TABLE', N'ShipMethod', 'CONSTRAINT', N'PK_ShipMethod_ShipMethodID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index.', 'SCHEMA', N'Purchasing', 'TABLE', N'ShipMethod', 'INDEX', N'AK_ShipMethod_Name'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index. Used to support replication samples.', 'SCHEMA', N'Purchasing', 'TABLE', N'ShipMethod', 'INDEX', N'AK_ShipMethod_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Purchasing', 'TABLE', N'ShipMethod', 'INDEX', N'PK_ShipMethod_ShipMethodID'
GO

```


---

## <a name="#uses"></a>Uses

* [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md)
* [Purchasing](../Security/Schemas/Purchasing.md)


---

## <a name="#usedby"></a>Used By

* [[Purchasing].[PurchaseOrderHeader]](PurchaseOrderHeader.md)
* [[Sales].[SalesOrderHeader]](SalesOrderHeader.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 12:25

