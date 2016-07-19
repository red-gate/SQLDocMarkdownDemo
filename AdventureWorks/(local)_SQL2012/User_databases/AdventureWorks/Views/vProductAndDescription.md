
# ![Views](../../../../Images/View32.png) [Production].[vProductAndDescription]

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Views](Views_.md) > Production.vProductAndDescription

## <a name="#description"></a>MS_Description
Product names and descriptions. Product descriptions are provided in multiple languages.
## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| ANSI Nulls On | YES |
| Quoted Identifier On | YES |
| Schema Bound | YES |
| Created | 13:14:55 14 March 2012 |
| Last Modified | 13:14:55 14 March 2012 |


## <a name="#columns"></a>Columns

| Key | Name |
|---|---|
| [![Cluster Key IX_vProductAndDescription: CultureID\\ProductID](../../../../Images/cluster.png)](#indexes) | ProductID |
|  | Name |
|  | ProductModel |
| [![Cluster Key IX_vProductAndDescription: CultureID\\ProductID](../../../../Images/cluster.png)](#indexes) | CultureID |
|  | Description |


## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Key IX_vProductAndDescription: CultureID\\ProductID](../../../../Images/cluster.png)](#indexes) | IX_vProductAndDescription | CultureID, ProductID | YES | _Clustered index on the view vProductAndDescription._ |


## <a name="#sqlscript"></a>SQL Script
```sql

CREATE VIEW [Production].[vProductAndDescription] 
WITH SCHEMABINDING 
AS 
-- View (indexed or standard) to display products and product descriptions by language.
SELECT 
    p.[ProductID] 
    ,p.[Name] 
    ,pm.[Name] AS [ProductModel] 
    ,pmx.[CultureID] 
    ,pd.[Description] 
FROM [Production].[Product] p 
    INNER JOIN [Production].[ProductModel] pm 
    ON p.[ProductModelID] = pm.[ProductModelID] 
    INNER JOIN [Production].[ProductModelProductDescriptionCulture] pmx 
    ON pm.[ProductModelID] = pmx.[ProductModelID] 
    INNER JOIN [Production].[ProductDescription] pd 
    ON pmx.[ProductDescriptionID] = pd.[ProductDescriptionID];
GO
CREATE UNIQUE CLUSTERED INDEX [IX_vProductAndDescription] ON [Production].[vProductAndDescription] ([CultureID], [ProductID]) ON [PRIMARY]
GO
EXEC sp_addextendedproperty N'MS_Description', N'Product names and descriptions. Product descriptions are provided in multiple languages.', 'SCHEMA', N'Production', 'VIEW', N'vProductAndDescription', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index on the view vProductAndDescription.', 'SCHEMA', N'Production', 'VIEW', N'vProductAndDescription', 'INDEX', N'IX_vProductAndDescription'
GO

```

## <a name="#uses"></a>Uses
DEPENDENCYLIST
* [[Production].[Product]](../Tables/Product.md)
* [[Production].[ProductDescription]](../Tables/ProductDescription.md)
* [[Production].[ProductModel]](../Tables/ProductModel.md)
* [[Production].[ProductModelProductDescriptionCulture]](../Tables/ProductModelProductDescriptionCulture.md)
* [Production](../Security/Schemas/Production.md)

FOOTER: FOOTER: Author:  Chris Whitworth
FOOTER: Created: 19 July 2016 09:34
FOOTER: Copyright 2016 - All Rights Reserved

