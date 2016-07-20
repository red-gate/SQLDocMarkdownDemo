#### 

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Production.ProductReview

# ![Tables](../../../../Images/Table32.png) [Production].[ProductReview]

---

## <a name="#description"></a>MS_Description

Customer reviews of products they have purchased.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Full Text Catalog | [AW2008FullTextCatalog](../Storage/Full_Text_Catalogs/AW2008FullTextCatalog.md) |
| Full Text | PK_ProductReview_ProductReviewID |
| Row Count (~) | 4 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:54 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Full Text Indexed | Language | Identity | Default | Description |
|---|---|---|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_ProductReview_ProductReviewID: ProductReviewID](../../../../Images/pkcluster.png)](#indexes) | ProductReviewID | int | 4 | NO |  |  | 1 - 1 |  | _Primary key for ProductReview records._ |
| [![Indexes IX_ProductReview_ProductID_Name](../../../../Images/Index.png)](#indexes)[![Foreign Keys FK_ProductReview_Product_ProductID: [Production].[Product].ProductID](../../../../Images/fk.png)](#foreignkeys) | ProductID | int | 4 | NO |  |  |  |  | _Product identification number. Foreign key to Product.ProductID._ |
| [![Indexes IX_ProductReview_ProductID_Name](../../../../Images/Index.png)](#indexes) | ReviewerName | [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md) | 100 | NO |  |  |  |  | _Name of the reviewer._ |
|  | ReviewDate | datetime | 8 | NO |  |  |  | (getdate()) | _Date review was submitted._ |
|  | EmailAddress | nvarchar(50) | 100 | NO |  |  |  |  | _Reviewer's e-mail address._ |
| [![Check Constraints CK_ProductReview_Rating : ([Rating]>=(1) AND [Rating]<=(5))](../../../../Images/c-constraint.png)](#checkconstraints) | Rating | int | 4 | NO |  |  |  |  | _Product rating given by the reviewer. Scale is 1 to 5 with 5 as the highest rating._ |
| [![Indexes IX_ProductReview_ProductID_Name](../../../../Images/Index.png)](#indexes) | Comments | nvarchar(3850) | 7700 | YES | YES | 1033 |  |  | _Reviewer's comments_ |
|  | ModifiedDate | datetime | 8 | NO |  |  |  | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Included Columns | Unique | Description |
|---|---|---|---|---|---|
| [![Cluster Primary Key PK_ProductReview_ProductReviewID: ProductReviewID](../../../../Images/pkcluster.png)](#indexes) | PK_ProductReview_ProductReviewID | ProductReviewID |  | YES | _Primary key (clustered) constraint_ |
|  | IX_ProductReview_ProductID_Name | ProductID, ReviewerName | Comments |  | _Nonclustered index._ |


---

## <a name="#checkconstraints"></a>Check Constraints

| Name | On Column | Constraint | Description |
|---|---|---|---|
| CK_ProductReview_Rating | Rating | ([Rating]>=(1) AND [Rating]<=(5)) | _Check constraint [Rating] BETWEEN (1) AND (5)_ |


---

## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_ProductReview_Product_ProductID | ProductID->[[Production].[Product].[ProductID]](Product.md) | _Foreign key constraint referencing Product.ProductID._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Production].[ProductReview]
(
[ProductReviewID] [int] NOT NULL IDENTITY(1, 1),
[ProductID] [int] NOT NULL,
[ReviewerName] [dbo].[Name] NOT NULL,
[ReviewDate] [datetime] NOT NULL CONSTRAINT [DF_ProductReview_ReviewDate] DEFAULT (getdate()),
[EmailAddress] [nvarchar] (50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[Rating] [int] NOT NULL,
[Comments] [nvarchar] (3850) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_ProductReview_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Production].[ProductReview] ADD CONSTRAINT [CK_ProductReview_Rating] CHECK (([Rating]>=(1) AND [Rating]<=(5)))
GO
ALTER TABLE [Production].[ProductReview] ADD CONSTRAINT [PK_ProductReview_ProductReviewID] PRIMARY KEY CLUSTERED  ([ProductReviewID]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_ProductReview_ProductID_Name] ON [Production].[ProductReview] ([ProductID], [ReviewerName]) INCLUDE ([Comments]) ON [PRIMARY]
GO
ALTER TABLE [Production].[ProductReview] ADD CONSTRAINT [FK_ProductReview_Product_ProductID] FOREIGN KEY ([ProductID]) REFERENCES [Production].[Product] ([ProductID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Customer reviews of products they have purchased.', 'SCHEMA', N'Production', 'TABLE', N'ProductReview', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Reviewer''s comments', 'SCHEMA', N'Production', 'TABLE', N'ProductReview', 'COLUMN', N'Comments'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Reviewer''s e-mail address.', 'SCHEMA', N'Production', 'TABLE', N'ProductReview', 'COLUMN', N'EmailAddress'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Production', 'TABLE', N'ProductReview', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Product identification number. Foreign key to Product.ProductID.', 'SCHEMA', N'Production', 'TABLE', N'ProductReview', 'COLUMN', N'ProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key for ProductReview records.', 'SCHEMA', N'Production', 'TABLE', N'ProductReview', 'COLUMN', N'ProductReviewID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Product rating given by the reviewer. Scale is 1 to 5 with 5 as the highest rating.', 'SCHEMA', N'Production', 'TABLE', N'ProductReview', 'COLUMN', N'Rating'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date review was submitted.', 'SCHEMA', N'Production', 'TABLE', N'ProductReview', 'COLUMN', N'ReviewDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Name of the reviewer.', 'SCHEMA', N'Production', 'TABLE', N'ProductReview', 'COLUMN', N'ReviewerName'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [Rating] BETWEEN (1) AND (5)', 'SCHEMA', N'Production', 'TABLE', N'ProductReview', 'CONSTRAINT', N'CK_ProductReview_Rating'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Production', 'TABLE', N'ProductReview', 'CONSTRAINT', N'DF_ProductReview_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Production', 'TABLE', N'ProductReview', 'CONSTRAINT', N'DF_ProductReview_ReviewDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Product.ProductID.', 'SCHEMA', N'Production', 'TABLE', N'ProductReview', 'CONSTRAINT', N'FK_ProductReview_Product_ProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Production', 'TABLE', N'ProductReview', 'CONSTRAINT', N'PK_ProductReview_ProductReviewID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Nonclustered index.', 'SCHEMA', N'Production', 'TABLE', N'ProductReview', 'INDEX', N'IX_ProductReview_ProductID_Name'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Production', 'TABLE', N'ProductReview', 'INDEX', N'PK_ProductReview_ProductReviewID'
GO
CREATE FULLTEXT INDEX ON [Production].[ProductReview] KEY INDEX [PK_ProductReview_ProductReviewID] ON [AW2008FullTextCatalog]
GO
ALTER FULLTEXT INDEX ON [Production].[ProductReview] ADD ([Comments] LANGUAGE 1033)
GO

```


---

## <a name="#uses"></a>Uses

DEPENDENCYLIST* [[Production].[Product]](Product.md)
* [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md)
* [Production](../Security/Schemas/Production.md)


---

## <a name="#usedby"></a>Used By

DEPENDENCYLIST* [AW2008FullTextCatalog](../Storage/Full_Text_Catalogs/AW2008FullTextCatalog.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

