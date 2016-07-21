#### asdasdasd

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Production.TransactionHistoryArchive

# ![Tables](../../../../Images/Table32.png) [Production].[TransactionHistoryArchive]

---

## <a name="#description"></a>MS_Description

Transactions for previous years.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 89253 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:47 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Default | Description |
|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_TransactionHistoryArchive_TransactionID: TransactionID](../../../../Images/pkcluster.png)](#indexes) | TransactionID | int | 4 | NO |  | _Primary key for TransactionHistoryArchive records._ |
| [![Indexes IX_TransactionHistoryArchive_ProductID](../../../../Images/Index.png)](#indexes) | ProductID | int | 4 | NO |  | _Product identification number. Foreign key to Product.ProductID._ |
| [![Indexes IX_TransactionHistoryArchive_ReferenceOrderID_ReferenceOrderLineID](../../../../Images/Index.png)](#indexes) | ReferenceOrderID | int | 4 | NO |  | _Purchase order, sales order, or work order identification number._ |
| [![Indexes IX_TransactionHistoryArchive_ReferenceOrderID_ReferenceOrderLineID](../../../../Images/Index.png)](#indexes) | ReferenceOrderLineID | int | 4 | NO | ((0)) | _Line number associated with the purchase order, sales order, or work order._ |
|  | TransactionDate | datetime | 8 | NO | (getdate()) | _Date and time of the transaction._ |
| [![Check Constraints CK_TransactionHistoryArchive_TransactionType : (upper([TransactionType])='P' OR upper([TransactionType])='S' OR upper([TransactionType])='W')](../../../../Images/c-constraint.png)](#checkconstraints) | TransactionType | nchar(1) | 2 | NO |  | _W = Work Order, S = Sales Order, P = Purchase Order_ |
|  | Quantity | int | 4 | NO |  | _Product quantity._ |
|  | ActualCost | money | 8 | NO |  | _Product cost._ |
|  | ModifiedDate | datetime | 8 | NO | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_TransactionHistoryArchive_TransactionID: TransactionID](../../../../Images/pkcluster.png)](#indexes) | PK_TransactionHistoryArchive_TransactionID | TransactionID | YES | _Primary key (clustered) constraint_ |
|  | IX_TransactionHistoryArchive_ProductID | ProductID |  | _Nonclustered index._ |
|  | IX_TransactionHistoryArchive_ReferenceOrderID_ReferenceOrderLineID | ReferenceOrderID, ReferenceOrderLineID |  | _Nonclustered index._ |


---

## <a name="#checkconstraints"></a>Check Constraints

| Name | On Column | Constraint | Description |
|---|---|---|---|
| CK_TransactionHistoryArchive_TransactionType | TransactionType | (upper([TransactionType])='P' OR upper([TransactionType])='S' OR upper([TransactionType])='W') | _Check constraint [TransactionType]='p' OR [TransactionType]='s' OR [TransactionType]='w' OR [TransactionType]='P' OR [TransactionType]='S' OR [TransactionType]='W'_ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Production].[TransactionHistoryArchive]
(
[TransactionID] [int] NOT NULL,
[ProductID] [int] NOT NULL,
[ReferenceOrderID] [int] NOT NULL,
[ReferenceOrderLineID] [int] NOT NULL CONSTRAINT [DF_TransactionHistoryArchive_ReferenceOrderLineID] DEFAULT ((0)),
[TransactionDate] [datetime] NOT NULL CONSTRAINT [DF_TransactionHistoryArchive_TransactionDate] DEFAULT (getdate()),
[TransactionType] [nchar] (1) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[Quantity] [int] NOT NULL,
[ActualCost] [money] NOT NULL,
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_TransactionHistoryArchive_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Production].[TransactionHistoryArchive] ADD CONSTRAINT [CK_TransactionHistoryArchive_TransactionType] CHECK ((upper([TransactionType])='P' OR upper([TransactionType])='S' OR upper([TransactionType])='W'))
GO
ALTER TABLE [Production].[TransactionHistoryArchive] ADD CONSTRAINT [PK_TransactionHistoryArchive_TransactionID] PRIMARY KEY CLUSTERED  ([TransactionID]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_TransactionHistoryArchive_ProductID] ON [Production].[TransactionHistoryArchive] ([ProductID]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_TransactionHistoryArchive_ReferenceOrderID_ReferenceOrderLineID] ON [Production].[TransactionHistoryArchive] ([ReferenceOrderID], [ReferenceOrderLineID]) ON [PRIMARY]
GO
EXEC sp_addextendedproperty N'MS_Description', N'Transactions for previous years.', 'SCHEMA', N'Production', 'TABLE', N'TransactionHistoryArchive', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Product cost.', 'SCHEMA', N'Production', 'TABLE', N'TransactionHistoryArchive', 'COLUMN', N'ActualCost'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Production', 'TABLE', N'TransactionHistoryArchive', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Product identification number. Foreign key to Product.ProductID.', 'SCHEMA', N'Production', 'TABLE', N'TransactionHistoryArchive', 'COLUMN', N'ProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Product quantity.', 'SCHEMA', N'Production', 'TABLE', N'TransactionHistoryArchive', 'COLUMN', N'Quantity'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Purchase order, sales order, or work order identification number.', 'SCHEMA', N'Production', 'TABLE', N'TransactionHistoryArchive', 'COLUMN', N'ReferenceOrderID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Line number associated with the purchase order, sales order, or work order.', 'SCHEMA', N'Production', 'TABLE', N'TransactionHistoryArchive', 'COLUMN', N'ReferenceOrderLineID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time of the transaction.', 'SCHEMA', N'Production', 'TABLE', N'TransactionHistoryArchive', 'COLUMN', N'TransactionDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key for TransactionHistoryArchive records.', 'SCHEMA', N'Production', 'TABLE', N'TransactionHistoryArchive', 'COLUMN', N'TransactionID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'W = Work Order, S = Sales Order, P = Purchase Order', 'SCHEMA', N'Production', 'TABLE', N'TransactionHistoryArchive', 'COLUMN', N'TransactionType'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [TransactionType]=''p'' OR [TransactionType]=''s'' OR [TransactionType]=''w'' OR [TransactionType]=''P'' OR [TransactionType]=''S'' OR [TransactionType]=''W''', 'SCHEMA', N'Production', 'TABLE', N'TransactionHistoryArchive', 'CONSTRAINT', N'CK_TransactionHistoryArchive_TransactionType'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Production', 'TABLE', N'TransactionHistoryArchive', 'CONSTRAINT', N'DF_TransactionHistoryArchive_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 0', 'SCHEMA', N'Production', 'TABLE', N'TransactionHistoryArchive', 'CONSTRAINT', N'DF_TransactionHistoryArchive_ReferenceOrderLineID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Production', 'TABLE', N'TransactionHistoryArchive', 'CONSTRAINT', N'DF_TransactionHistoryArchive_TransactionDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Production', 'TABLE', N'TransactionHistoryArchive', 'CONSTRAINT', N'PK_TransactionHistoryArchive_TransactionID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Nonclustered index.', 'SCHEMA', N'Production', 'TABLE', N'TransactionHistoryArchive', 'INDEX', N'IX_TransactionHistoryArchive_ProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Nonclustered index.', 'SCHEMA', N'Production', 'TABLE', N'TransactionHistoryArchive', 'INDEX', N'IX_TransactionHistoryArchive_ReferenceOrderID_ReferenceOrderLineID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Production', 'TABLE', N'TransactionHistoryArchive', 'INDEX', N'PK_TransactionHistoryArchive_TransactionID'
GO

```


---

## <a name="#uses"></a>Uses

* [Production](../Security/Schemas/Production.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 14:15

