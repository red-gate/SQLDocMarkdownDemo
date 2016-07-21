#### asdasdasd

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Production.ProductModel

# ![Tables](../../../../Images/Table32.png) [Production].[ProductModel]

---

## <a name="#description"></a>MS_Description

Product model classification.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 128 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:55 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Identity | Default | Description |
|---|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_ProductModel_ProductModelID: ProductModelID](../../../../Images/pkcluster.png)](#indexes) | ProductModelID | int | 4 | NO | 1 - 1 |  | _Primary key for ProductModel records._ |
| [![Indexes AK_ProductModel_Name](../../../../Images/Index.png)](#indexes) | Name | [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md) | 100 | NO |  |  | _Product model description._ |
| [![Indexes PXML_ProductModel_CatalogDescription](../../../../Images/Index.png)](#indexes) | CatalogDescription | [xml([Production].[ProductDescriptionSchemaCollection])](../Programmability/Types/XML_Schema_Collections/ProductDescriptionSchemaCollection.md) | max | YES |  |  | _Detailed product catalog information in xml format._ |
| [![Indexes PXML_ProductModel_Instructions](../../../../Images/Index.png)](#indexes) | Instructions | [xml([Production].[ManuInstructionsSchemaCollection])](../Programmability/Types/XML_Schema_Collections/ManuInstructionsSchemaCollection.md) | max | YES |  |  | _Manufacturing instructions in xml format._ |
| [![Indexes AK_ProductModel_rowguid](../../../../Images/Index.png)](#indexes) | rowguid | uniqueidentifier | 16 | NO |  | (newid()) | _ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample._ |
|  | ModifiedDate | datetime | 8 | NO |  | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Type | Unique | XML Type | Description |
|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_ProductModel_ProductModelID: ProductModelID](../../../../Images/pkcluster.png)](#indexes) | PK_ProductModel_ProductModelID | ProductModelID |  | YES |  | _Primary key (clustered) constraint_ |
|  | AK_ProductModel_Name | Name |  | YES |  | _Unique nonclustered index._ |
|  | AK_ProductModel_rowguid | rowguid |  | YES |  | _Unique nonclustered index. Used to support replication samples._ |
|  | PXML_ProductModel_CatalogDescription | CatalogDescription | xml |  | Primary | _Primary XML index._ |
|  | PXML_ProductModel_Instructions | Instructions | xml |  | Primary | _Primary XML index._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Production].[ProductModel]
(
[ProductModelID] [int] NOT NULL IDENTITY(1, 1),
[Name] [dbo].[Name] NOT NULL,
[CatalogDescription] [xml] (CONTENT [Production].[ProductDescriptionSchemaCollection]) NULL,
[Instructions] [xml] (CONTENT [Production].[ManuInstructionsSchemaCollection]) NULL,
[rowguid] [uniqueidentifier] NOT NULL ROWGUIDCOL CONSTRAINT [DF_ProductModel_rowguid] DEFAULT (newid()),
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_ProductModel_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
ALTER TABLE [Production].[ProductModel] ADD CONSTRAINT [PK_ProductModel_ProductModelID] PRIMARY KEY CLUSTERED  ([ProductModelID]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_ProductModel_Name] ON [Production].[ProductModel] ([Name]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_ProductModel_rowguid] ON [Production].[ProductModel] ([rowguid]) ON [PRIMARY]
GO
CREATE PRIMARY XML INDEX [PXML_ProductModel_CatalogDescription]
ON [Production].[ProductModel] ([CatalogDescription])
GO
CREATE PRIMARY XML INDEX [PXML_ProductModel_Instructions]
ON [Production].[ProductModel] ([Instructions])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Product model classification.', 'SCHEMA', N'Production', 'TABLE', N'ProductModel', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Detailed product catalog information in xml format.', 'SCHEMA', N'Production', 'TABLE', N'ProductModel', 'COLUMN', N'CatalogDescription'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Manufacturing instructions in xml format.', 'SCHEMA', N'Production', 'TABLE', N'ProductModel', 'COLUMN', N'Instructions'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Production', 'TABLE', N'ProductModel', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Product model description.', 'SCHEMA', N'Production', 'TABLE', N'ProductModel', 'COLUMN', N'Name'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key for ProductModel records.', 'SCHEMA', N'Production', 'TABLE', N'ProductModel', 'COLUMN', N'ProductModelID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample.', 'SCHEMA', N'Production', 'TABLE', N'ProductModel', 'COLUMN', N'rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Production', 'TABLE', N'ProductModel', 'CONSTRAINT', N'DF_ProductModel_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of NEWID()', 'SCHEMA', N'Production', 'TABLE', N'ProductModel', 'CONSTRAINT', N'DF_ProductModel_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Production', 'TABLE', N'ProductModel', 'CONSTRAINT', N'PK_ProductModel_ProductModelID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index.', 'SCHEMA', N'Production', 'TABLE', N'ProductModel', 'INDEX', N'AK_ProductModel_Name'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index. Used to support replication samples.', 'SCHEMA', N'Production', 'TABLE', N'ProductModel', 'INDEX', N'AK_ProductModel_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Production', 'TABLE', N'ProductModel', 'INDEX', N'PK_ProductModel_ProductModelID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary XML index.', 'SCHEMA', N'Production', 'TABLE', N'ProductModel', 'INDEX', N'PXML_ProductModel_CatalogDescription'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary XML index.', 'SCHEMA', N'Production', 'TABLE', N'ProductModel', 'INDEX', N'PXML_ProductModel_Instructions'
GO

```


---

## <a name="#uses"></a>Uses

* [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md)
* [Production](../Security/Schemas/Production.md)
* [[Production].[ManuInstructionsSchemaCollection]](../Programmability/Types/XML_Schema_Collections/ManuInstructionsSchemaCollection.md)
* [[Production].[ProductDescriptionSchemaCollection]](../Programmability/Types/XML_Schema_Collections/ProductDescriptionSchemaCollection.md)


---

## <a name="#usedby"></a>Used By

* [[Production].[Product]](Product.md)
* [[Production].[ProductModelIllustration]](ProductModelIllustration.md)
* [[Production].[ProductModelProductDescriptionCulture]](ProductModelProductDescriptionCulture.md)
* [[Production].[vProductAndDescription]](../Views/vProductAndDescription.md)
* [[Production].[vProductModelCatalogDescription]](../Views/vProductModelCatalogDescription.md)
* [[Production].[vProductModelInstructions]](../Views/vProductModelInstructions.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 12:25

