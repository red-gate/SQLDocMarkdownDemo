#### 

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Production.ProductProductPhoto

# ![Tables](../../../../Images/Table32.png) [Production].[ProductProductPhoto]

---

## <a name="#description"></a>MS_Description

Cross-reference table mapping products and product photos.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Heap | YES |
| Row Count (~) | 504 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:54 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Default | Description |
|---|---|---|---|---|---|---|
| [![Primary Key PK_ProductProductPhoto_ProductID_ProductPhotoID: ProductID\ProductPhotoID](../../../../Images/pk.png)](#indexes)[![Foreign Keys FK_ProductProductPhoto_Product_ProductID: [Production].[Product].ProductID](../../../../Images/fk.png)](#foreignkeys) | ProductID | int | 4 | NO |  | _Product identification number. Foreign key to Product.ProductID._ |
| [![Primary Key PK_ProductProductPhoto_ProductID_ProductPhotoID: ProductID\ProductPhotoID](../../../../Images/pk.png)](#indexes)[![Foreign Keys FK_ProductProductPhoto_ProductPhoto_ProductPhotoID: [Production].[ProductPhoto].ProductPhotoID](../../../../Images/fk.png)](#foreignkeys) | ProductPhotoID | int | 4 | NO |  | _Product photo identification number. Foreign key to ProductPhoto.ProductPhotoID._ |
|  | Primary | [[dbo].[Flag]](../Programmability/Types/User-Defined_Data_Types/Flag.md) | 1 | NO | ((0)) | _0 = Photo is not the principal image. 1 = Photo is the principal image._ |
|  | ModifiedDate | datetime | 8 | NO | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Primary Key PK_ProductProductPhoto_ProductID_ProductPhotoID: ProductID\ProductPhotoID](../../../../Images/pk.png)](#indexes) | PK_ProductProductPhoto_ProductID_ProductPhotoID | ProductID, ProductPhotoID | YES | _Primary key (clustered) constraint_ |


---

## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_ProductProductPhoto_Product_ProductID | ProductID->[[Production].[Product].[ProductID]](Product.md) | _Foreign key constraint referencing Product.ProductID._ |
| FK_ProductProductPhoto_ProductPhoto_ProductPhotoID | ProductPhotoID->[[Production].[ProductPhoto].[ProductPhotoID]](ProductPhoto.md) | _Foreign key constraint referencing ProductPhoto.ProductPhotoID._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Production].[ProductProductPhoto]
(
[ProductID] [int] NOT NULL,
[ProductPhotoID] [int] NOT NULL,
[Primary] [dbo].[Flag] NOT NULL CONSTRAINT [DF_ProductProductPhoto_Primary] DEFAULT ((0)),
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_ProductProductPhoto_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Production].[ProductProductPhoto] ADD CONSTRAINT [PK_ProductProductPhoto_ProductID_ProductPhotoID] PRIMARY KEY NONCLUSTERED  ([ProductID], [ProductPhotoID]) ON [PRIMARY]
GO
ALTER TABLE [Production].[ProductProductPhoto] ADD CONSTRAINT [FK_ProductProductPhoto_Product_ProductID] FOREIGN KEY ([ProductID]) REFERENCES [Production].[Product] ([ProductID])
GO
ALTER TABLE [Production].[ProductProductPhoto] ADD CONSTRAINT [FK_ProductProductPhoto_ProductPhoto_ProductPhotoID] FOREIGN KEY ([ProductPhotoID]) REFERENCES [Production].[ProductPhoto] ([ProductPhotoID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Cross-reference table mapping products and product photos.', 'SCHEMA', N'Production', 'TABLE', N'ProductProductPhoto', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Production', 'TABLE', N'ProductProductPhoto', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'0 = Photo is not the principal image. 1 = Photo is the principal image.', 'SCHEMA', N'Production', 'TABLE', N'ProductProductPhoto', 'COLUMN', N'Primary'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Product identification number. Foreign key to Product.ProductID.', 'SCHEMA', N'Production', 'TABLE', N'ProductProductPhoto', 'COLUMN', N'ProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Product photo identification number. Foreign key to ProductPhoto.ProductPhotoID.', 'SCHEMA', N'Production', 'TABLE', N'ProductProductPhoto', 'COLUMN', N'ProductPhotoID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Production', 'TABLE', N'ProductProductPhoto', 'CONSTRAINT', N'DF_ProductProductPhoto_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 0 (FALSE)', 'SCHEMA', N'Production', 'TABLE', N'ProductProductPhoto', 'CONSTRAINT', N'DF_ProductProductPhoto_Primary'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Product.ProductID.', 'SCHEMA', N'Production', 'TABLE', N'ProductProductPhoto', 'CONSTRAINT', N'FK_ProductProductPhoto_Product_ProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing ProductPhoto.ProductPhotoID.', 'SCHEMA', N'Production', 'TABLE', N'ProductProductPhoto', 'CONSTRAINT', N'FK_ProductProductPhoto_ProductPhoto_ProductPhotoID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Production', 'TABLE', N'ProductProductPhoto', 'CONSTRAINT', N'PK_ProductProductPhoto_ProductID_ProductPhotoID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Nonclustered index created by a primary key constraint.', 'SCHEMA', N'Production', 'TABLE', N'ProductProductPhoto', 'INDEX', N'PK_ProductProductPhoto_ProductID_ProductPhotoID'
GO

```


---

## <a name="#uses"></a>Uses

DEPENDENCYLIST* [[Production].[Product]](Product.md)
* [[Production].[ProductPhoto]](ProductPhoto.md)
* [[dbo].[Flag]](../Programmability/Types/User-Defined_Data_Types/Flag.md)
* [Production](../Security/Schemas/Production.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

