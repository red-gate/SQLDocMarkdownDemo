
# ![Tables](../../../../Images/Table32.png) [Production].[ProductListPriceHistory]

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables_.md) > Production.ProductListPriceHistory

## <a name="#description"></a>MS_Description
Changes in the list price of a product over time.
## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Row Count (~) | 395 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:54 14 March 2012 |


## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Default | Description |
|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_ProductListPriceHistory_ProductID_StartDate: ProductID\\StartDate](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_ProductListPriceHistory_Product_ProductID: [Production].[Product].ProductID](../../../../Images/fk.png)](#foreignkeys) | ProductID | int | 4 | NO |  | _Product identification number. Foreign key to Product.ProductID_ |
| [![Cluster Primary Key PK_ProductListPriceHistory_ProductID_StartDate: ProductID\\StartDate](../../../../Images/pkcluster.png)](#indexes) | StartDate | datetime | 8 | NO |  | _List price start date._ |
|  | EndDate | datetime | 8 | YES |  | _List price end date_ |
| [![Check Constraints CK_ProductListPriceHistory_ListPrice : ([ListPrice]>(0.00))](../../../../Images/c-constraint.png)](#checkconstraints) | ListPrice | money | 8 | NO |  | _Product list price._ |
|  | ModifiedDate | datetime | 8 | NO | (getdate()) | _Date and time the record was last updated._ |


## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_ProductListPriceHistory_ProductID_StartDate: ProductID\\StartDate](../../../../Images/pkcluster.png)](#indexes) | PK_ProductListPriceHistory_ProductID_StartDate | ProductID, StartDate | YES | _Primary key (clustered) constraint_ |


## <a name="#checkconstraints"></a>Check Constraints

| Name | On Column | Constraint | Description |
|---|---|---|---|
| CK_ProductListPriceHistory_EndDate |  | ([EndDate]>=[StartDate] OR [EndDate] IS NULL) | _Check constraint [EndDate] >= [StartDate] OR [EndDate] IS NULL_ |
| CK_ProductListPriceHistory_ListPrice | ListPrice | ([ListPrice]>(0.00)) | _Check constraint [ListPrice] > (0.00)_ |


## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_ProductListPriceHistory_Product_ProductID | ProductID->[[Production].[Product].[ProductID]](Product.md) | _Foreign key constraint referencing Product.ProductID._ |


## <a name="#sqlscript"></a>SQL Script
```sql
CREATE TABLE [Production].[ProductListPriceHistory]
(
[ProductID] [int] NOT NULL,
[StartDate] [datetime] NOT NULL,
[EndDate] [datetime] NULL,
[ListPrice] [money] NOT NULL,
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_ProductListPriceHistory_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Production].[ProductListPriceHistory] ADD CONSTRAINT [CK_ProductListPriceHistory_EndDate] CHECK (([EndDate]>=[StartDate] OR [EndDate] IS NULL))
GO
ALTER TABLE [Production].[ProductListPriceHistory] ADD CONSTRAINT [CK_ProductListPriceHistory_ListPrice] CHECK (([ListPrice]>(0.00)))
GO
ALTER TABLE [Production].[ProductListPriceHistory] ADD CONSTRAINT [PK_ProductListPriceHistory_ProductID_StartDate] PRIMARY KEY CLUSTERED  ([ProductID], [StartDate]) ON [PRIMARY]
GO
ALTER TABLE [Production].[ProductListPriceHistory] ADD CONSTRAINT [FK_ProductListPriceHistory_Product_ProductID] FOREIGN KEY ([ProductID]) REFERENCES [Production].[Product] ([ProductID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Changes in the list price of a product over time.', 'SCHEMA', N'Production', 'TABLE', N'ProductListPriceHistory', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'List price end date', 'SCHEMA', N'Production', 'TABLE', N'ProductListPriceHistory', 'COLUMN', N'EndDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Product list price.', 'SCHEMA', N'Production', 'TABLE', N'ProductListPriceHistory', 'COLUMN', N'ListPrice'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Production', 'TABLE', N'ProductListPriceHistory', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Product identification number. Foreign key to Product.ProductID', 'SCHEMA', N'Production', 'TABLE', N'ProductListPriceHistory', 'COLUMN', N'ProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'List price start date.', 'SCHEMA', N'Production', 'TABLE', N'ProductListPriceHistory', 'COLUMN', N'StartDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [EndDate] >= [StartDate] OR [EndDate] IS NULL', 'SCHEMA', N'Production', 'TABLE', N'ProductListPriceHistory', 'CONSTRAINT', N'CK_ProductListPriceHistory_EndDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [ListPrice] > (0.00)', 'SCHEMA', N'Production', 'TABLE', N'ProductListPriceHistory', 'CONSTRAINT', N'CK_ProductListPriceHistory_ListPrice'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Production', 'TABLE', N'ProductListPriceHistory', 'CONSTRAINT', N'DF_ProductListPriceHistory_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Product.ProductID.', 'SCHEMA', N'Production', 'TABLE', N'ProductListPriceHistory', 'CONSTRAINT', N'FK_ProductListPriceHistory_Product_ProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Production', 'TABLE', N'ProductListPriceHistory', 'CONSTRAINT', N'PK_ProductListPriceHistory_ProductID_StartDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Production', 'TABLE', N'ProductListPriceHistory', 'INDEX', N'PK_ProductListPriceHistory_ProductID_StartDate'
GO

```

## <a name="#uses"></a>Uses
DEPENDENCYLIST
* [[Production].[Product]](Product.md)
* [Production](../Security/Schemas/Production.md)


## <a name="#usedby"></a>Used By
DEPENDENCYLIST
* [[dbo].[ufnGetProductDealerPrice]](../Programmability/Functions/Scalar-valued_Functions/ufnGetProductDealerPrice.md)
* [[dbo].[ufnGetProductListPrice]](../Programmability/Functions/Scalar-valued_Functions/ufnGetProductListPrice.md)

FOOTER: FOOTER: Author:  Chris Whitworth
FOOTER: Created: 19 July 2016 09:34
FOOTER: Copyright 2016 - All Rights Reserved

