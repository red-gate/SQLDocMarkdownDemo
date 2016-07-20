#### 

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Production.BillOfMaterials

# ![Tables](../../../../Images/Table32.png) [Production].[BillOfMaterials]

---

## <a name="#description"></a>MS_Description

Items required to make bicycles and bicycle subassemblies. It identifies the heirarchical relationship between a parent product and its components.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 2679 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:53 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Identity | Default | Description |
|---|---|---|---|---|---|---|---|
| [![Primary Key PK_BillOfMaterials_BillOfMaterialsID: BillOfMaterialsID](../../../../Images/pk.png)](#indexes) | BillOfMaterialsID | int | 4 | NO | 1 - 1 |  | _Primary key for BillOfMaterials records._ |
| [![Cluster Key AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate: ProductAssemblyID\ComponentID\StartDate](../../../../Images/cluster.png)](#indexes)[![Foreign Keys FK_BillOfMaterials_Product_ProductAssemblyID: [Production].[Product].ProductAssemblyID](../../../../Images/fk.png)](#foreignkeys) | ProductAssemblyID | int | 4 | YES |  |  | _Parent product identification number. Foreign key to Product.ProductID._ |
| [![Cluster Key AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate: ProductAssemblyID\ComponentID\StartDate](../../../../Images/cluster.png)](#indexes)[![Foreign Keys FK_BillOfMaterials_Product_ComponentID: [Production].[Product].ComponentID](../../../../Images/fk.png)](#foreignkeys) | ComponentID | int | 4 | NO |  |  | _Component identification number. Foreign key to Product.ProductID._ |
| [![Cluster Key AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate: ProductAssemblyID\ComponentID\StartDate](../../../../Images/cluster.png)](#indexes) | StartDate | datetime | 8 | NO |  | (getdate()) | _Date the component started being used in the assembly item._ |
|  | EndDate | datetime | 8 | YES |  |  | _Date the component stopped being used in the assembly item._ |
| [![Indexes IX_BillOfMaterials_UnitMeasureCode](../../../../Images/Index.png)](#indexes)[![Foreign Keys FK_BillOfMaterials_UnitMeasure_UnitMeasureCode: [Production].[UnitMeasure].UnitMeasureCode](../../../../Images/fk.png)](#foreignkeys) | UnitMeasureCode | nchar(3) | 6 | NO |  |  | _Standard code identifying the unit of measure for the quantity._ |
|  | BOMLevel | smallint | 2 | NO |  |  | _Indicates the depth the component is from its parent (AssemblyID)._ |
| [![Check Constraints CK_BillOfMaterials_PerAssemblyQty : ([PerAssemblyQty]>=(1.00))](../../../../Images/c-constraint.png)](#checkconstraints) | PerAssemblyQty | decimal(8,2) | 5 | NO |  | ((1.00)) | _Quantity of the component needed to create the assembly._ |
|  | ModifiedDate | datetime | 8 | NO |  | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Primary Key PK_BillOfMaterials_BillOfMaterialsID: BillOfMaterialsID](../../../../Images/pk.png)](#indexes) | PK_BillOfMaterials_BillOfMaterialsID | BillOfMaterialsID | YES | _Primary key (clustered) constraint_ |
| [![Cluster Key AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate: ProductAssemblyID\ComponentID\StartDate](../../../../Images/cluster.png)](#indexes) | AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate | ProductAssemblyID, ComponentID, StartDate | YES | _Clustered index._ |
|  | IX_BillOfMaterials_UnitMeasureCode | UnitMeasureCode |  | _Nonclustered index._ |


---

## <a name="#checkconstraints"></a>Check Constraints

| Name | On Column | Constraint | Description |
|---|---|---|---|
| CK_BillOfMaterials_EndDate |  | ([EndDate]>[StartDate] OR [EndDate] IS NULL) | _Check constraint EndDate] > [StartDate] OR [EndDate] IS NULL_ |
| CK_BillOfMaterials_PerAssemblyQty | PerAssemblyQty | ([PerAssemblyQty]>=(1.00)) | _Check constraint [PerAssemblyQty] >= (1.00)_ |
| CK_BillOfMaterials_BOMLevel |  | ([ProductAssemblyID] IS NULL AND [BOMLevel]=(0) AND [PerAssemblyQty]=(1.00) OR [ProductAssemblyID] IS NOT NULL AND [BOMLevel]>=(1)) | _Check constraint [ProductAssemblyID] IS NULL AND [BOMLevel] = (0) AND [PerAssemblyQty] = (1) OR [ProductAssemblyID] IS NOT NULL AND [BOMLevel] >= (1)_ |
| CK_BillOfMaterials_ProductAssemblyID |  | ([ProductAssemblyID]<>[ComponentID]) | _Check constraint [ProductAssemblyID] <> [ComponentID]_ |


---

## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_BillOfMaterials_Product_ComponentID | ComponentID->[[Production].[Product].[ProductID]](Product.md) | _Foreign key constraint referencing Product.ComponentID._ |
| FK_BillOfMaterials_Product_ProductAssemblyID | ProductAssemblyID->[[Production].[Product].[ProductID]](Product.md) | _Foreign key constraint referencing Product.ProductAssemblyID._ |
| FK_BillOfMaterials_UnitMeasure_UnitMeasureCode | UnitMeasureCode->[[Production].[UnitMeasure].[UnitMeasureCode]](UnitMeasure.md) | _Foreign key constraint referencing UnitMeasure.UnitMeasureCode._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Production].[BillOfMaterials]
(
[BillOfMaterialsID] [int] NOT NULL IDENTITY(1, 1),
[ProductAssemblyID] [int] NULL,
[ComponentID] [int] NOT NULL,
[StartDate] [datetime] NOT NULL CONSTRAINT [DF_BillOfMaterials_StartDate] DEFAULT (getdate()),
[EndDate] [datetime] NULL,
[UnitMeasureCode] [nchar] (3) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[BOMLevel] [smallint] NOT NULL,
[PerAssemblyQty] [decimal] (8, 2) NOT NULL CONSTRAINT [DF_BillOfMaterials_PerAssemblyQty] DEFAULT ((1.00)),
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_BillOfMaterials_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Production].[BillOfMaterials] ADD CONSTRAINT [CK_BillOfMaterials_EndDate] CHECK (([EndDate]>[StartDate] OR [EndDate] IS NULL))
GO
ALTER TABLE [Production].[BillOfMaterials] ADD CONSTRAINT [CK_BillOfMaterials_PerAssemblyQty] CHECK (([PerAssemblyQty]>=(1.00)))
GO
ALTER TABLE [Production].[BillOfMaterials] ADD CONSTRAINT [CK_BillOfMaterials_BOMLevel] CHECK (([ProductAssemblyID] IS NULL AND [BOMLevel]=(0) AND [PerAssemblyQty]=(1.00) OR [ProductAssemblyID] IS NOT NULL AND [BOMLevel]>=(1)))
GO
ALTER TABLE [Production].[BillOfMaterials] ADD CONSTRAINT [CK_BillOfMaterials_ProductAssemblyID] CHECK (([ProductAssemblyID]<>[ComponentID]))
GO
ALTER TABLE [Production].[BillOfMaterials] ADD CONSTRAINT [PK_BillOfMaterials_BillOfMaterialsID] PRIMARY KEY NONCLUSTERED  ([BillOfMaterialsID]) ON [PRIMARY]
GO
CREATE UNIQUE CLUSTERED INDEX [AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate] ON [Production].[BillOfMaterials] ([ProductAssemblyID], [ComponentID], [StartDate]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_BillOfMaterials_UnitMeasureCode] ON [Production].[BillOfMaterials] ([UnitMeasureCode]) ON [PRIMARY]
GO
ALTER TABLE [Production].[BillOfMaterials] ADD CONSTRAINT [FK_BillOfMaterials_Product_ComponentID] FOREIGN KEY ([ComponentID]) REFERENCES [Production].[Product] ([ProductID])
GO
ALTER TABLE [Production].[BillOfMaterials] ADD CONSTRAINT [FK_BillOfMaterials_Product_ProductAssemblyID] FOREIGN KEY ([ProductAssemblyID]) REFERENCES [Production].[Product] ([ProductID])
GO
ALTER TABLE [Production].[BillOfMaterials] ADD CONSTRAINT [FK_BillOfMaterials_UnitMeasure_UnitMeasureCode] FOREIGN KEY ([UnitMeasureCode]) REFERENCES [Production].[UnitMeasure] ([UnitMeasureCode])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Items required to make bicycles and bicycle subassemblies. It identifies the heirarchical relationship between a parent product and its components.', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key for BillOfMaterials records.', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'COLUMN', N'BillOfMaterialsID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Indicates the depth the component is from its parent (AssemblyID).', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'COLUMN', N'BOMLevel'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Component identification number. Foreign key to Product.ProductID.', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'COLUMN', N'ComponentID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date the component stopped being used in the assembly item.', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'COLUMN', N'EndDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Quantity of the component needed to create the assembly.', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'COLUMN', N'PerAssemblyQty'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Parent product identification number. Foreign key to Product.ProductID.', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'COLUMN', N'ProductAssemblyID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date the component started being used in the assembly item.', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'COLUMN', N'StartDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Standard code identifying the unit of measure for the quantity.', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'COLUMN', N'UnitMeasureCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [ProductAssemblyID] IS NULL AND [BOMLevel] = (0) AND [PerAssemblyQty] = (1) OR [ProductAssemblyID] IS NOT NULL AND [BOMLevel] >= (1)', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'CONSTRAINT', N'CK_BillOfMaterials_BOMLevel'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint EndDate] > [StartDate] OR [EndDate] IS NULL', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'CONSTRAINT', N'CK_BillOfMaterials_EndDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [PerAssemblyQty] >= (1.00)', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'CONSTRAINT', N'CK_BillOfMaterials_PerAssemblyQty'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [ProductAssemblyID] <> [ComponentID]', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'CONSTRAINT', N'CK_BillOfMaterials_ProductAssemblyID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'CONSTRAINT', N'DF_BillOfMaterials_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 1.0', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'CONSTRAINT', N'DF_BillOfMaterials_PerAssemblyQty'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'CONSTRAINT', N'DF_BillOfMaterials_StartDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Product.ComponentID.', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'CONSTRAINT', N'FK_BillOfMaterials_Product_ComponentID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Product.ProductAssemblyID.', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'CONSTRAINT', N'FK_BillOfMaterials_Product_ProductAssemblyID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing UnitMeasure.UnitMeasureCode.', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'CONSTRAINT', N'FK_BillOfMaterials_UnitMeasure_UnitMeasureCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'CONSTRAINT', N'PK_BillOfMaterials_BillOfMaterialsID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index.', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'INDEX', N'AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Nonclustered index.', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'INDEX', N'IX_BillOfMaterials_UnitMeasureCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Nonclustered index created by a primary key constraint.', 'SCHEMA', N'Production', 'TABLE', N'BillOfMaterials', 'INDEX', N'PK_BillOfMaterials_BillOfMaterialsID'
GO

```


---

## <a name="#uses"></a>Uses

DEPENDENCYLIST* [[Production].[Product]](Product.md)
* [[Production].[UnitMeasure]](UnitMeasure.md)
* [Production](../Security/Schemas/Production.md)


---

## <a name="#usedby"></a>Used By

DEPENDENCYLIST* [[dbo].[uspGetBillOfMaterials]](../Programmability/Stored_Procedures/uspGetBillOfMaterials.md)
* [[dbo].[uspGetWhereUsedProductID]](../Programmability/Stored_Procedures/uspGetWhereUsedProductID.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

