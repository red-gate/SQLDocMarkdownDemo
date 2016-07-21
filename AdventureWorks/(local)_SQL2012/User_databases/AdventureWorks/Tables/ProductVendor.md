#### asdasdasd

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Purchasing.ProductVendor

# ![Tables](../../../../Images/Table32.png) [Purchasing].[ProductVendor]

---

## <a name="#description"></a>MS_Description

Cross-reference table mapping vendors with the products they supply.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 460 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:54 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Default | Description |
|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_ProductVendor_ProductID_BusinessEntityID: ProductID\BusinessEntityID](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_ProductVendor_Product_ProductID: [Production].[Product].ProductID](../../../../Images/fk.png)](#foreignkeys) | ProductID | int | 4 | NO |  | _Primary key. Foreign key to Product.ProductID._ |
| [![Cluster Primary Key PK_ProductVendor_ProductID_BusinessEntityID: ProductID\BusinessEntityID](../../../../Images/pkcluster.png)](#indexes)[![Indexes IX_ProductVendor_BusinessEntityID](../../../../Images/Index.png)](#indexes)[![Foreign Keys FK_ProductVendor_Vendor_BusinessEntityID: [Purchasing].[Vendor].BusinessEntityID](../../../../Images/fk.png)](#foreignkeys) | BusinessEntityID | int | 4 | NO |  | _Primary key. Foreign key to Vendor.BusinessEntityID._ |
| [![Check Constraints CK_ProductVendor_AverageLeadTime : ([AverageLeadTime]>=(1))](../../../../Images/c-constraint.png)](#checkconstraints) | AverageLeadTime | int | 4 | NO |  | _The average span of time (in days) between placing an order with the vendor and receiving the purchased product._ |
| [![Check Constraints CK_ProductVendor_StandardPrice : ([StandardPrice]>(0.00))](../../../../Images/c-constraint.png)](#checkconstraints) | StandardPrice | money | 8 | NO |  | _The vendor's usual selling price._ |
| [![Check Constraints CK_ProductVendor_LastReceiptCost : ([LastReceiptCost]>(0.00))](../../../../Images/c-constraint.png)](#checkconstraints) | LastReceiptCost | money | 8 | YES |  | _The selling price when last purchased._ |
|  | LastReceiptDate | datetime | 8 | YES |  | _Date the product was last received by the vendor._ |
| [![Check Constraints CK_ProductVendor_MinOrderQty : ([MinOrderQty]>=(1))](../../../../Images/c-constraint.png)](#checkconstraints) | MinOrderQty | int | 4 | NO |  | _The maximum quantity that should be ordered._ |
| [![Check Constraints CK_ProductVendor_MaxOrderQty : ([MaxOrderQty]>=(1))](../../../../Images/c-constraint.png)](#checkconstraints) | MaxOrderQty | int | 4 | NO |  | _The minimum quantity that should be ordered._ |
| [![Check Constraints CK_ProductVendor_OnOrderQty : ([OnOrderQty]>=(0))](../../../../Images/c-constraint.png)](#checkconstraints) | OnOrderQty | int | 4 | YES |  | _The quantity currently on order._ |
| [![Indexes IX_ProductVendor_UnitMeasureCode](../../../../Images/Index.png)](#indexes)[![Foreign Keys FK_ProductVendor_UnitMeasure_UnitMeasureCode: [Production].[UnitMeasure].UnitMeasureCode](../../../../Images/fk.png)](#foreignkeys) | UnitMeasureCode | nchar(3) | 6 | NO |  | _The product's unit of measure._ |
|  | ModifiedDate | datetime | 8 | NO | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_ProductVendor_ProductID_BusinessEntityID: ProductID\BusinessEntityID](../../../../Images/pkcluster.png)](#indexes) | PK_ProductVendor_ProductID_BusinessEntityID | ProductID, BusinessEntityID | YES | _Primary key (clustered) constraint_ |
|  | IX_ProductVendor_BusinessEntityID | BusinessEntityID |  | _Nonclustered index._ |
|  | IX_ProductVendor_UnitMeasureCode | UnitMeasureCode |  | _Nonclustered index._ |


---

## <a name="#checkconstraints"></a>Check Constraints

| Name | On Column | Constraint | Description |
|---|---|---|---|
| CK_ProductVendor_AverageLeadTime | AverageLeadTime | ([AverageLeadTime]>=(1)) | _Check constraint [AverageLeadTime] >= (1)_ |
| CK_ProductVendor_LastReceiptCost | LastReceiptCost | ([LastReceiptCost]>(0.00)) | _Check constraint [LastReceiptCost] > (0.00)_ |
| CK_ProductVendor_MaxOrderQty | MaxOrderQty | ([MaxOrderQty]>=(1)) | _Check constraint [MaxOrderQty] >= (1)_ |
| CK_ProductVendor_MinOrderQty | MinOrderQty | ([MinOrderQty]>=(1)) | _Check constraint [MinOrderQty] >= (1)_ |
| CK_ProductVendor_OnOrderQty | OnOrderQty | ([OnOrderQty]>=(0)) | _Check constraint [OnOrderQty] >= (0)_ |
| CK_ProductVendor_StandardPrice | StandardPrice | ([StandardPrice]>(0.00)) | _Check constraint [StandardPrice] > (0.00)_ |


---

## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_ProductVendor_Product_ProductID | ProductID->[[Production].[Product].[ProductID]](Product.md) | _Foreign key constraint referencing Product.ProductID._ |
| FK_ProductVendor_UnitMeasure_UnitMeasureCode | UnitMeasureCode->[[Production].[UnitMeasure].[UnitMeasureCode]](UnitMeasure.md) | _Foreign key constraint referencing UnitMeasure.UnitMeasureCode._ |
| FK_ProductVendor_Vendor_BusinessEntityID | BusinessEntityID->[[Purchasing].[Vendor].[BusinessEntityID]](Vendor.md) | _Foreign key constraint referencing Vendor.BusinessEntityID._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Purchasing].[ProductVendor]
(
[ProductID] [int] NOT NULL,
[BusinessEntityID] [int] NOT NULL,
[AverageLeadTime] [int] NOT NULL,
[StandardPrice] [money] NOT NULL,
[LastReceiptCost] [money] NULL,
[LastReceiptDate] [datetime] NULL,
[MinOrderQty] [int] NOT NULL,
[MaxOrderQty] [int] NOT NULL,
[OnOrderQty] [int] NULL,
[UnitMeasureCode] [nchar] (3) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_ProductVendor_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Purchasing].[ProductVendor] ADD CONSTRAINT [CK_ProductVendor_AverageLeadTime] CHECK (([AverageLeadTime]>=(1)))
GO
ALTER TABLE [Purchasing].[ProductVendor] ADD CONSTRAINT [CK_ProductVendor_LastReceiptCost] CHECK (([LastReceiptCost]>(0.00)))
GO
ALTER TABLE [Purchasing].[ProductVendor] ADD CONSTRAINT [CK_ProductVendor_MaxOrderQty] CHECK (([MaxOrderQty]>=(1)))
GO
ALTER TABLE [Purchasing].[ProductVendor] ADD CONSTRAINT [CK_ProductVendor_MinOrderQty] CHECK (([MinOrderQty]>=(1)))
GO
ALTER TABLE [Purchasing].[ProductVendor] ADD CONSTRAINT [CK_ProductVendor_OnOrderQty] CHECK (([OnOrderQty]>=(0)))
GO
ALTER TABLE [Purchasing].[ProductVendor] ADD CONSTRAINT [CK_ProductVendor_StandardPrice] CHECK (([StandardPrice]>(0.00)))
GO
ALTER TABLE [Purchasing].[ProductVendor] ADD CONSTRAINT [PK_ProductVendor_ProductID_BusinessEntityID] PRIMARY KEY CLUSTERED  ([ProductID], [BusinessEntityID]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_ProductVendor_BusinessEntityID] ON [Purchasing].[ProductVendor] ([BusinessEntityID]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_ProductVendor_UnitMeasureCode] ON [Purchasing].[ProductVendor] ([UnitMeasureCode]) ON [PRIMARY]
GO
ALTER TABLE [Purchasing].[ProductVendor] ADD CONSTRAINT [FK_ProductVendor_Product_ProductID] FOREIGN KEY ([ProductID]) REFERENCES [Production].[Product] ([ProductID])
GO
ALTER TABLE [Purchasing].[ProductVendor] ADD CONSTRAINT [FK_ProductVendor_UnitMeasure_UnitMeasureCode] FOREIGN KEY ([UnitMeasureCode]) REFERENCES [Production].[UnitMeasure] ([UnitMeasureCode])
GO
ALTER TABLE [Purchasing].[ProductVendor] ADD CONSTRAINT [FK_ProductVendor_Vendor_BusinessEntityID] FOREIGN KEY ([BusinessEntityID]) REFERENCES [Purchasing].[Vendor] ([BusinessEntityID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Cross-reference table mapping vendors with the products they supply.', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'The average span of time (in days) between placing an order with the vendor and receiving the purchased product.', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'COLUMN', N'AverageLeadTime'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key. Foreign key to Vendor.BusinessEntityID.', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'COLUMN', N'BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'The selling price when last purchased.', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'COLUMN', N'LastReceiptCost'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date the product was last received by the vendor.', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'COLUMN', N'LastReceiptDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'The minimum quantity that should be ordered.', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'COLUMN', N'MaxOrderQty'
GO
EXEC sp_addextendedproperty N'MS_Description', N'The maximum quantity that should be ordered.', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'COLUMN', N'MinOrderQty'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'The quantity currently on order.', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'COLUMN', N'OnOrderQty'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key. Foreign key to Product.ProductID.', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'COLUMN', N'ProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'The vendor''s usual selling price.', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'COLUMN', N'StandardPrice'
GO
EXEC sp_addextendedproperty N'MS_Description', N'The product''s unit of measure.', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'COLUMN', N'UnitMeasureCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [AverageLeadTime] >= (1)', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'CONSTRAINT', N'CK_ProductVendor_AverageLeadTime'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [LastReceiptCost] > (0.00)', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'CONSTRAINT', N'CK_ProductVendor_LastReceiptCost'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [MaxOrderQty] >= (1)', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'CONSTRAINT', N'CK_ProductVendor_MaxOrderQty'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [MinOrderQty] >= (1)', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'CONSTRAINT', N'CK_ProductVendor_MinOrderQty'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [OnOrderQty] >= (0)', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'CONSTRAINT', N'CK_ProductVendor_OnOrderQty'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [StandardPrice] > (0.00)', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'CONSTRAINT', N'CK_ProductVendor_StandardPrice'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'CONSTRAINT', N'DF_ProductVendor_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Product.ProductID.', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'CONSTRAINT', N'FK_ProductVendor_Product_ProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing UnitMeasure.UnitMeasureCode.', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'CONSTRAINT', N'FK_ProductVendor_UnitMeasure_UnitMeasureCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Vendor.BusinessEntityID.', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'CONSTRAINT', N'FK_ProductVendor_Vendor_BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'CONSTRAINT', N'PK_ProductVendor_ProductID_BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Nonclustered index.', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'INDEX', N'IX_ProductVendor_BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Nonclustered index.', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'INDEX', N'IX_ProductVendor_UnitMeasureCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Purchasing', 'TABLE', N'ProductVendor', 'INDEX', N'PK_ProductVendor_ProductID_BusinessEntityID'
GO

```


---

## <a name="#uses"></a>Uses

* [[Production].[Product]](Product.md)
* [[Production].[UnitMeasure]](UnitMeasure.md)
* [[Purchasing].[Vendor]](Vendor.md)
* [Purchasing](../Security/Schemas/Purchasing.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 14:15

