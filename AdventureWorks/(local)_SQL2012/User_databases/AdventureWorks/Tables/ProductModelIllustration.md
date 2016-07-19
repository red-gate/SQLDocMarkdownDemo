
# ![Tables](../../../../Images/Table32.png) [Production].[ProductModelIllustration]

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables_.md) > Production.ProductModelIllustration

## <a name="#description"></a>MS_Description
Cross-reference table mapping product models and illustrations.
## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Row Count (~) | 7 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:54 14 March 2012 |


## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Default | Description |
|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_ProductModelIllustration_ProductModelID_IllustrationID: ProductModelID\\IllustrationID](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_ProductModelIllustration_ProductModel_ProductModelID: [Production].[ProductModel].ProductModelID](../../../../Images/fk.png)](#foreignkeys) | ProductModelID | int | 4 | NO |  | _Primary key. Foreign key to ProductModel.ProductModelID._ |
| [![Cluster Primary Key PK_ProductModelIllustration_ProductModelID_IllustrationID: ProductModelID\\IllustrationID](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_ProductModelIllustration_Illustration_IllustrationID: [Production].[Illustration].IllustrationID](../../../../Images/fk.png)](#foreignkeys) | IllustrationID | int | 4 | NO |  | _Primary key. Foreign key to Illustration.IllustrationID._ |
|  | ModifiedDate | datetime | 8 | NO | (getdate()) | _Date and time the record was last updated._ |


## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_ProductModelIllustration_ProductModelID_IllustrationID: ProductModelID\\IllustrationID](../../../../Images/pkcluster.png)](#indexes) | PK_ProductModelIllustration_ProductModelID_IllustrationID | ProductModelID, IllustrationID | YES | _Primary key (clustered) constraint_ |


## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_ProductModelIllustration_Illustration_IllustrationID | IllustrationID->[[Production].[Illustration].[IllustrationID]](Illustration.md) | _Foreign key constraint referencing Illustration.IllustrationID._ |
| FK_ProductModelIllustration_ProductModel_ProductModelID | ProductModelID->[[Production].[ProductModel].[ProductModelID]](ProductModel.md) | _Foreign key constraint referencing ProductModel.ProductModelID._ |


## <a name="#sqlscript"></a>SQL Script
```sql
CREATE TABLE [Production].[ProductModelIllustration]
(
[ProductModelID] [int] NOT NULL,
[IllustrationID] [int] NOT NULL,
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_ProductModelIllustration_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Production].[ProductModelIllustration] ADD CONSTRAINT [PK_ProductModelIllustration_ProductModelID_IllustrationID] PRIMARY KEY CLUSTERED  ([ProductModelID], [IllustrationID]) ON [PRIMARY]
GO
ALTER TABLE [Production].[ProductModelIllustration] ADD CONSTRAINT [FK_ProductModelIllustration_Illustration_IllustrationID] FOREIGN KEY ([IllustrationID]) REFERENCES [Production].[Illustration] ([IllustrationID])
GO
ALTER TABLE [Production].[ProductModelIllustration] ADD CONSTRAINT [FK_ProductModelIllustration_ProductModel_ProductModelID] FOREIGN KEY ([ProductModelID]) REFERENCES [Production].[ProductModel] ([ProductModelID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Cross-reference table mapping product models and illustrations.', 'SCHEMA', N'Production', 'TABLE', N'ProductModelIllustration', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key. Foreign key to Illustration.IllustrationID.', 'SCHEMA', N'Production', 'TABLE', N'ProductModelIllustration', 'COLUMN', N'IllustrationID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Production', 'TABLE', N'ProductModelIllustration', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key. Foreign key to ProductModel.ProductModelID.', 'SCHEMA', N'Production', 'TABLE', N'ProductModelIllustration', 'COLUMN', N'ProductModelID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Production', 'TABLE', N'ProductModelIllustration', 'CONSTRAINT', N'DF_ProductModelIllustration_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Illustration.IllustrationID.', 'SCHEMA', N'Production', 'TABLE', N'ProductModelIllustration', 'CONSTRAINT', N'FK_ProductModelIllustration_Illustration_IllustrationID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing ProductModel.ProductModelID.', 'SCHEMA', N'Production', 'TABLE', N'ProductModelIllustration', 'CONSTRAINT', N'FK_ProductModelIllustration_ProductModel_ProductModelID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Production', 'TABLE', N'ProductModelIllustration', 'CONSTRAINT', N'PK_ProductModelIllustration_ProductModelID_IllustrationID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Production', 'TABLE', N'ProductModelIllustration', 'INDEX', N'PK_ProductModelIllustration_ProductModelID_IllustrationID'
GO

```

## <a name="#uses"></a>Uses
DEPENDENCYLIST
* [[Production].[Illustration]](Illustration.md)
* [[Production].[ProductModel]](ProductModel.md)
* [Production](../Security/Schemas/Production.md)

FOOTER: FOOTER: Author:  Chris Whitworth
FOOTER: Created: 19 July 2016 09:34
FOOTER: Copyright 2016 - All Rights Reserved

