#### asdasdasd

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Sales.ShoppingCartItem

# ![Tables](../../../../Images/Table32.png) [Sales].[ShoppingCartItem]

---

## <a name="#description"></a>MS_Description

Contains online customer orders until the order is submitted or cancelled.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 3 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:55 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Identity | Default | Description |
|---|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_ShoppingCartItem_ShoppingCartItemID: ShoppingCartItemID](../../../../Images/pkcluster.png)](#indexes) | ShoppingCartItemID | int | 4 | NO | 1 - 1 |  | _Primary key for ShoppingCartItem records._ |
| [![Indexes IX_ShoppingCartItem_ShoppingCartID_ProductID](../../../../Images/Index.png)](#indexes) | ShoppingCartID | nvarchar(50) | 100 | NO |  |  | _Shopping cart identification number._ |
| [![Check Constraints CK_ShoppingCartItem_Quantity : ([Quantity]>=(1))](../../../../Images/c-constraint.png)](#checkconstraints) | Quantity | int | 4 | NO |  | ((1)) | _Product quantity ordered._ |
| [![Indexes IX_ShoppingCartItem_ShoppingCartID_ProductID](../../../../Images/Index.png)](#indexes)[![Foreign Keys FK_ShoppingCartItem_Product_ProductID: [Production].[Product].ProductID](../../../../Images/fk.png)](#foreignkeys) | ProductID | int | 4 | NO |  |  | _Product ordered. Foreign key to Product.ProductID._ |
|  | DateCreated | datetime | 8 | NO |  | (getdate()) | _Date the time the record was created._ |
|  | ModifiedDate | datetime | 8 | NO |  | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_ShoppingCartItem_ShoppingCartItemID: ShoppingCartItemID](../../../../Images/pkcluster.png)](#indexes) | PK_ShoppingCartItem_ShoppingCartItemID | ShoppingCartItemID | YES | _Primary key (clustered) constraint_ |
|  | IX_ShoppingCartItem_ShoppingCartID_ProductID | ShoppingCartID, ProductID |  | _Nonclustered index._ |


---

## <a name="#checkconstraints"></a>Check Constraints

| Name | On Column | Constraint | Description |
|---|---|---|---|
| CK_ShoppingCartItem_Quantity | Quantity | ([Quantity]>=(1)) | _Check constraint [Quantity] >= (1)_ |


---

## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_ShoppingCartItem_Product_ProductID | ProductID->[[Production].[Product].[ProductID]](Product.md) | _Foreign key constraint referencing Product.ProductID._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Sales].[ShoppingCartItem]
(
[ShoppingCartItemID] [int] NOT NULL IDENTITY(1, 1),
[ShoppingCartID] [nvarchar] (50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[Quantity] [int] NOT NULL CONSTRAINT [DF_ShoppingCartItem_Quantity] DEFAULT ((1)),
[ProductID] [int] NOT NULL,
[DateCreated] [datetime] NOT NULL CONSTRAINT [DF_ShoppingCartItem_DateCreated] DEFAULT (getdate()),
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_ShoppingCartItem_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Sales].[ShoppingCartItem] ADD CONSTRAINT [CK_ShoppingCartItem_Quantity] CHECK (([Quantity]>=(1)))
GO
ALTER TABLE [Sales].[ShoppingCartItem] ADD CONSTRAINT [PK_ShoppingCartItem_ShoppingCartItemID] PRIMARY KEY CLUSTERED  ([ShoppingCartItemID]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_ShoppingCartItem_ShoppingCartID_ProductID] ON [Sales].[ShoppingCartItem] ([ShoppingCartID], [ProductID]) ON [PRIMARY]
GO
ALTER TABLE [Sales].[ShoppingCartItem] ADD CONSTRAINT [FK_ShoppingCartItem_Product_ProductID] FOREIGN KEY ([ProductID]) REFERENCES [Production].[Product] ([ProductID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Contains online customer orders until the order is submitted or cancelled.', 'SCHEMA', N'Sales', 'TABLE', N'ShoppingCartItem', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date the time the record was created.', 'SCHEMA', N'Sales', 'TABLE', N'ShoppingCartItem', 'COLUMN', N'DateCreated'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Sales', 'TABLE', N'ShoppingCartItem', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Product ordered. Foreign key to Product.ProductID.', 'SCHEMA', N'Sales', 'TABLE', N'ShoppingCartItem', 'COLUMN', N'ProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Product quantity ordered.', 'SCHEMA', N'Sales', 'TABLE', N'ShoppingCartItem', 'COLUMN', N'Quantity'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Shopping cart identification number.', 'SCHEMA', N'Sales', 'TABLE', N'ShoppingCartItem', 'COLUMN', N'ShoppingCartID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key for ShoppingCartItem records.', 'SCHEMA', N'Sales', 'TABLE', N'ShoppingCartItem', 'COLUMN', N'ShoppingCartItemID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [Quantity] >= (1)', 'SCHEMA', N'Sales', 'TABLE', N'ShoppingCartItem', 'CONSTRAINT', N'CK_ShoppingCartItem_Quantity'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Sales', 'TABLE', N'ShoppingCartItem', 'CONSTRAINT', N'DF_ShoppingCartItem_DateCreated'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Sales', 'TABLE', N'ShoppingCartItem', 'CONSTRAINT', N'DF_ShoppingCartItem_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 1', 'SCHEMA', N'Sales', 'TABLE', N'ShoppingCartItem', 'CONSTRAINT', N'DF_ShoppingCartItem_Quantity'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Product.ProductID.', 'SCHEMA', N'Sales', 'TABLE', N'ShoppingCartItem', 'CONSTRAINT', N'FK_ShoppingCartItem_Product_ProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Sales', 'TABLE', N'ShoppingCartItem', 'CONSTRAINT', N'PK_ShoppingCartItem_ShoppingCartItemID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Nonclustered index.', 'SCHEMA', N'Sales', 'TABLE', N'ShoppingCartItem', 'INDEX', N'IX_ShoppingCartItem_ShoppingCartID_ProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Sales', 'TABLE', N'ShoppingCartItem', 'INDEX', N'PK_ShoppingCartItem_ShoppingCartItemID'
GO

```


---

## <a name="#uses"></a>Uses

* [[Production].[Product]](Product.md)
* [Sales](../Security/Schemas/Sales.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 14:15

