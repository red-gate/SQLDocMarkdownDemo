#### asdasdasd

[Project](../../../../../index.md) > [(local)\\SQL2012](../../../../index.md) > [User databases](../../../index.md) > [AdventureWorks](../../index.md) > [Storage](../index.md) > [Full Text Catalogs](Full_Text_Catalogs.md) > AW2008FullTextCatalog

# ![Full Text Catalogs](../../../../../Images/FullTextCatalog32.png) AW2008FullTextCatalog

---

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Owner | dbo |
| Default | YES |
| Accent Sensitive | YES |


---

## <a name="#tables"></a>Tables

* [JobCandidate](../../Tables/JobCandidate.md)
* [Document](../../Tables/Document.md)
* [ProductReview](../../Tables/ProductReview.md)


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE FULLTEXT CATALOG [AW2008FullTextCatalog]
WITH ACCENT_SENSITIVITY = ON
AS DEFAULT
AUTHORIZATION [dbo]
GO
CREATE FULLTEXT INDEX ON [HumanResources].[JobCandidate] KEY INDEX [PK_JobCandidate_JobCandidateID] ON [AW2008FullTextCatalog]
GO
CREATE FULLTEXT INDEX ON [Production].[Document] KEY INDEX [PK_Document_DocumentNode] ON [AW2008FullTextCatalog]
GO
CREATE FULLTEXT INDEX ON [Production].[ProductReview] KEY INDEX [PK_ProductReview_ProductReviewID] ON [AW2008FullTextCatalog]
GO

```


---

## <a name="#uses"></a>Uses

* [[HumanResources].[JobCandidate]](../../Tables/JobCandidate.md)
* [[Production].[Document]](../../Tables/Document.md)
* [[Production].[ProductReview]](../../Tables/ProductReview.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 14:15

