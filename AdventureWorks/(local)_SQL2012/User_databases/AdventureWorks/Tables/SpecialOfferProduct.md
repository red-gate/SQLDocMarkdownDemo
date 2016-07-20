#### 

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Sales.SpecialOfferProduct

# ![Tables](../../../../Images/Table32.png) [Sales].[SpecialOfferProduct]

---

## <a name="#description"></a>MS_Description

Cross-reference table mapping products to special offer discounts.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Row Count (~) | 538 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:55 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Default | Description |
|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_SpecialOfferProduct_SpecialOfferID_ProductID: SpecialOfferID\ProductID](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_SpecialOfferProduct_SpecialOffer_SpecialOfferID: [Sales].[SpecialOffer].SpecialOfferID](../../../../Images/fk.png)](#foreignkeys) | SpecialOfferID | int | 4 | NO |  | _Primary key for SpecialOfferProduct records._ |
| [![Cluster Primary Key PK_SpecialOfferProduct_SpecialOfferID_ProductID: SpecialOfferID\ProductID](../../../../Images/pkcluster.png)](#indexes)[![Indexes IX_SpecialOfferProduct_ProductID](../../../../Images/Index.png)](#indexes)[![Foreign Keys FK_SpecialOfferProduct_Product_ProductID: [Production].[Product].ProductID](../../../../Images/fk.png)](#foreignkeys) | ProductID | int | 4 | NO |  | _Product identification number. Foreign key to Product.ProductID._ |
| [![Indexes AK_SpecialOfferProduct_rowguid](../../../../Images/Index.png)](#indexes) | rowguid | uniqueidentifier | 16 | NO | (newid()) | _ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample._ |
|  | ModifiedDate | datetime | 8 | NO | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_SpecialOfferProduct_SpecialOfferID_ProductID: SpecialOfferID\ProductID](../../../../Images/pkcluster.png)](#indexes) | PK_SpecialOfferProduct_SpecialOfferID_ProductID | SpecialOfferID, ProductID | YES | _Primary key (clustered) constraint_ |
|  | AK_SpecialOfferProduct_rowguid | rowguid | YES | _Unique nonclustered index. Used to support replication samples._ |
|  | IX_SpecialOfferProduct_ProductID | ProductID |  | _Nonclustered index._ |


---

## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_SpecialOfferProduct_Product_ProductID | ProductID->[[Production].[Product].[ProductID]](Product.md) | _Foreign key constraint referencing Product.ProductID._ |
| FK_SpecialOfferProduct_SpecialOffer_SpecialOfferID | SpecialOfferID->[[Sales].[SpecialOffer].[SpecialOfferID]](SpecialOffer.md) | _Foreign key constraint referencing SpecialOffer.SpecialOfferID._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Sales].[SpecialOfferProduct]
(
[SpecialOfferID] [int] NOT NULL,
[ProductID] [int] NOT NULL,
[rowguid] [uniqueidentifier] NOT NULL ROWGUIDCOL CONSTRAINT [DF_SpecialOfferProduct_rowguid] DEFAULT (newid()),
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_SpecialOfferProduct_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Sales].[SpecialOfferProduct] ADD CONSTRAINT [PK_SpecialOfferProduct_SpecialOfferID_ProductID] PRIMARY KEY CLUSTERED  ([SpecialOfferID], [ProductID]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_SpecialOfferProduct_ProductID] ON [Sales].[SpecialOfferProduct] ([ProductID]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_SpecialOfferProduct_rowguid] ON [Sales].[SpecialOfferProduct] ([rowguid]) ON [PRIMARY]
GO
ALTER TABLE [Sales].[SpecialOfferProduct] ADD CONSTRAINT [FK_SpecialOfferProduct_Product_ProductID] FOREIGN KEY ([ProductID]) REFERENCES [Production].[Product] ([ProductID])
GO
ALTER TABLE [Sales].[SpecialOfferProduct] ADD CONSTRAINT [FK_SpecialOfferProduct_SpecialOffer_SpecialOfferID] FOREIGN KEY ([SpecialOfferID]) REFERENCES [Sales].[SpecialOffer] ([SpecialOfferID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Cross-reference table mapping products to special offer discounts.', 'SCHEMA', N'Sales', 'TABLE', N'SpecialOfferProduct', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Sales', 'TABLE', N'SpecialOfferProduct', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Product identification number. Foreign key to Product.ProductID.', 'SCHEMA', N'Sales', 'TABLE', N'SpecialOfferProduct', 'COLUMN', N'ProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample.', 'SCHEMA', N'Sales', 'TABLE', N'SpecialOfferProduct', 'COLUMN', N'rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key for SpecialOfferProduct records.', 'SCHEMA', N'Sales', 'TABLE', N'SpecialOfferProduct', 'COLUMN', N'SpecialOfferID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Sales', 'TABLE', N'SpecialOfferProduct', 'CONSTRAINT', N'DF_SpecialOfferProduct_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of NEWID()', 'SCHEMA', N'Sales', 'TABLE', N'SpecialOfferProduct', 'CONSTRAINT', N'DF_SpecialOfferProduct_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Product.ProductID.', 'SCHEMA', N'Sales', 'TABLE', N'SpecialOfferProduct', 'CONSTRAINT', N'FK_SpecialOfferProduct_Product_ProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing SpecialOffer.SpecialOfferID.', 'SCHEMA', N'Sales', 'TABLE', N'SpecialOfferProduct', 'CONSTRAINT', N'FK_SpecialOfferProduct_SpecialOffer_SpecialOfferID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Sales', 'TABLE', N'SpecialOfferProduct', 'CONSTRAINT', N'PK_SpecialOfferProduct_SpecialOfferID_ProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index. Used to support replication samples.', 'SCHEMA', N'Sales', 'TABLE', N'SpecialOfferProduct', 'INDEX', N'AK_SpecialOfferProduct_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Nonclustered index.', 'SCHEMA', N'Sales', 'TABLE', N'SpecialOfferProduct', 'INDEX', N'IX_SpecialOfferProduct_ProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Sales', 'TABLE', N'SpecialOfferProduct', 'INDEX', N'PK_SpecialOfferProduct_SpecialOfferID_ProductID'
GO

```


---

## <a name="#uses"></a>Uses

DEPENDENCYLIST* [[Production].[Product]](Product.md)
* [[Sales].[SpecialOffer]](SpecialOffer.md)
* [Sales](../Security/Schemas/Sales.md)


---

## <a name="#usedby"></a>Used By

DEPENDENCYLIST* [[Sales].[SalesOrderDetail]](SalesOrderDetail.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

