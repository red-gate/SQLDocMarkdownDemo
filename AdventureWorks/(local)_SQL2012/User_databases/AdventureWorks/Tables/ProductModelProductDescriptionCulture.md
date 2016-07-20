#### 

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Production.ProductModelProductDescriptionCulture

# ![Tables](../../../../Images/Table32.png) [Production].[ProductModelProductDescriptionCulture]

---

## <a name="#description"></a>MS_Description

Cross-reference table mapping product descriptions and the language the description is written in.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 762 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:55 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Default | Description |
|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_ProductModelProductDescriptionCulture_ProductModelID_ProductDescriptionID_CultureID: ProductModelID\ProductDescriptionID\CultureID](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_ProductModelProductDescriptionCulture_ProductModel_ProductModelID: [Production].[ProductModel].ProductModelID](../../../../Images/fk.png)](#foreignkeys) | ProductModelID | int | 4 | NO |  | _Primary key. Foreign key to ProductModel.ProductModelID._ |
| [![Cluster Primary Key PK_ProductModelProductDescriptionCulture_ProductModelID_ProductDescriptionID_CultureID: ProductModelID\ProductDescriptionID\CultureID](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_ProductModelProductDescriptionCulture_ProductDescription_ProductDescriptionID: [Production].[ProductDescription].ProductDescriptionID](../../../../Images/fk.png)](#foreignkeys) | ProductDescriptionID | int | 4 | NO |  | _Primary key. Foreign key to ProductDescription.ProductDescriptionID._ |
| [![Cluster Primary Key PK_ProductModelProductDescriptionCulture_ProductModelID_ProductDescriptionID_CultureID: ProductModelID\ProductDescriptionID\CultureID](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_ProductModelProductDescriptionCulture_Culture_CultureID: [Production].[Culture].CultureID](../../../../Images/fk.png)](#foreignkeys) | CultureID | nchar(6) | 12 | NO |  | _Culture identification number. Foreign key to Culture.CultureID._ |
|  | ModifiedDate | datetime | 8 | NO | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_ProductModelProductDescriptionCulture_ProductModelID_ProductDescriptionID_CultureID: ProductModelID\ProductDescriptionID\CultureID](../../../../Images/pkcluster.png)](#indexes) | PK_ProductModelProductDescriptionCulture_ProductModelID_ProductDescriptionID_CultureID | ProductModelID, ProductDescriptionID, CultureID | YES | _Primary key (clustered) constraint_ |


---

## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_ProductModelProductDescriptionCulture_Culture_CultureID | CultureID->[[Production].[Culture].[CultureID]](Culture.md) | _Foreign key constraint referencing Culture.CultureID._ |
| FK_ProductModelProductDescriptionCulture_ProductDescription_ProductDescriptionID | ProductDescriptionID->[[Production].[ProductDescription].[ProductDescriptionID]](ProductDescription.md) | _Foreign key constraint referencing ProductDescription.ProductDescriptionID._ |
| FK_ProductModelProductDescriptionCulture_ProductModel_ProductModelID | ProductModelID->[[Production].[ProductModel].[ProductModelID]](ProductModel.md) | _Foreign key constraint referencing ProductModel.ProductModelID._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Production].[ProductModelProductDescriptionCulture]
(
[ProductModelID] [int] NOT NULL,
[ProductDescriptionID] [int] NOT NULL,
[CultureID] [nchar] (6) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_ProductModelProductDescriptionCulture_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Production].[ProductModelProductDescriptionCulture] ADD CONSTRAINT [PK_ProductModelProductDescriptionCulture_ProductModelID_ProductDescriptionID_CultureID] PRIMARY KEY CLUSTERED  ([ProductModelID], [ProductDescriptionID], [CultureID]) ON [PRIMARY]
GO
ALTER TABLE [Production].[ProductModelProductDescriptionCulture] ADD CONSTRAINT [FK_ProductModelProductDescriptionCulture_Culture_CultureID] FOREIGN KEY ([CultureID]) REFERENCES [Production].[Culture] ([CultureID])
GO
ALTER TABLE [Production].[ProductModelProductDescriptionCulture] ADD CONSTRAINT [FK_ProductModelProductDescriptionCulture_ProductDescription_ProductDescriptionID] FOREIGN KEY ([ProductDescriptionID]) REFERENCES [Production].[ProductDescription] ([ProductDescriptionID])
GO
ALTER TABLE [Production].[ProductModelProductDescriptionCulture] ADD CONSTRAINT [FK_ProductModelProductDescriptionCulture_ProductModel_ProductModelID] FOREIGN KEY ([ProductModelID]) REFERENCES [Production].[ProductModel] ([ProductModelID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Cross-reference table mapping product descriptions and the language the description is written in.', 'SCHEMA', N'Production', 'TABLE', N'ProductModelProductDescriptionCulture', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Culture identification number. Foreign key to Culture.CultureID.', 'SCHEMA', N'Production', 'TABLE', N'ProductModelProductDescriptionCulture', 'COLUMN', N'CultureID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Production', 'TABLE', N'ProductModelProductDescriptionCulture', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key. Foreign key to ProductDescription.ProductDescriptionID.', 'SCHEMA', N'Production', 'TABLE', N'ProductModelProductDescriptionCulture', 'COLUMN', N'ProductDescriptionID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key. Foreign key to ProductModel.ProductModelID.', 'SCHEMA', N'Production', 'TABLE', N'ProductModelProductDescriptionCulture', 'COLUMN', N'ProductModelID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Production', 'TABLE', N'ProductModelProductDescriptionCulture', 'CONSTRAINT', N'DF_ProductModelProductDescriptionCulture_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Culture.CultureID.', 'SCHEMA', N'Production', 'TABLE', N'ProductModelProductDescriptionCulture', 'CONSTRAINT', N'FK_ProductModelProductDescriptionCulture_Culture_CultureID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing ProductDescription.ProductDescriptionID.', 'SCHEMA', N'Production', 'TABLE', N'ProductModelProductDescriptionCulture', 'CONSTRAINT', N'FK_ProductModelProductDescriptionCulture_ProductDescription_ProductDescriptionID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing ProductModel.ProductModelID.', 'SCHEMA', N'Production', 'TABLE', N'ProductModelProductDescriptionCulture', 'CONSTRAINT', N'FK_ProductModelProductDescriptionCulture_ProductModel_ProductModelID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Production', 'TABLE', N'ProductModelProductDescriptionCulture', 'CONSTRAINT', N'PK_ProductModelProductDescriptionCulture_ProductModelID_ProductDescriptionID_CultureID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Production', 'TABLE', N'ProductModelProductDescriptionCulture', 'INDEX', N'PK_ProductModelProductDescriptionCulture_ProductModelID_ProductDescriptionID_CultureID'
GO

```


---

## <a name="#uses"></a>Uses

DEPENDENCYLIST* [[Production].[Culture]](Culture.md)
* [[Production].[ProductDescription]](ProductDescription.md)
* [[Production].[ProductModel]](ProductModel.md)
* [Production](../Security/Schemas/Production.md)


---

## <a name="#usedby"></a>Used By

DEPENDENCYLIST* [[Production].[vProductAndDescription]](../Views/vProductAndDescription.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

