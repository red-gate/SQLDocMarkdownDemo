#### 

[Project](../../../../../index.md) > [(local)\\SQL2012](../../../../index.md) > [User databases](../../../index.md) > [AdventureWorks](../../index.md) > [Security](../index.md) > [Schemas](Schemas.md) > Production

# ![Schemas](../../../../../Images/Schema32.png) Production

---

## <a name="#description"></a>MS_Description

Contains objects related to products, inventory, and manufacturing.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Owner | dbo |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE SCHEMA [Production]
AUTHORIZATION [dbo]
GO
EXEC sp_addextendedproperty N'MS_Description', N'Contains objects related to products, inventory, and manufacturing.', 'SCHEMA', N'Production', NULL, NULL, NULL, NULL
GO

```


---

## <a name="#usedby"></a>Used By

DEPENDENCYLIST* [[Production].[BillOfMaterials]](../../Tables/BillOfMaterials.md)
* [[Production].[Culture]](../../Tables/Culture.md)
* [[Production].[Document]](../../Tables/Document.md)
* [[Production].[Illustration]](../../Tables/Illustration.md)
* [[Production].[Location]](../../Tables/Location.md)
* [[Production].[Product]](../../Tables/Product.md)
* [[Production].[ProductCategory]](../../Tables/ProductCategory.md)
* [[Production].[ProductCostHistory]](../../Tables/ProductCostHistory.md)
* [[Production].[ProductDescription]](../../Tables/ProductDescription.md)
* [[Production].[ProductDocument]](../../Tables/ProductDocument.md)
* [[Production].[ProductInventory]](../../Tables/ProductInventory.md)
* [[Production].[ProductListPriceHistory]](../../Tables/ProductListPriceHistory.md)
* [[Production].[ProductModel]](../../Tables/ProductModel.md)
* [[Production].[ProductModelIllustration]](../../Tables/ProductModelIllustration.md)
* [[Production].[ProductModelProductDescriptionCulture]](../../Tables/ProductModelProductDescriptionCulture.md)
* [[Production].[ProductPhoto]](../../Tables/ProductPhoto.md)
* [[Production].[ProductProductPhoto]](../../Tables/ProductProductPhoto.md)
* [[Production].[ProductReview]](../../Tables/ProductReview.md)
* [[Production].[ProductSubcategory]](../../Tables/ProductSubcategory.md)
* [[Production].[ScrapReason]](../../Tables/ScrapReason.md)
* [[Production].[TransactionHistory]](../../Tables/TransactionHistory.md)
* [[Production].[TransactionHistoryArchive]](../../Tables/TransactionHistoryArchive.md)
* [[Production].[UnitMeasure]](../../Tables/UnitMeasure.md)
* [[Production].[WorkOrder]](../../Tables/WorkOrder.md)
* [[Production].[WorkOrderRouting]](../../Tables/WorkOrderRouting.md)
* [[Production].[vProductAndDescription]](../../Views/vProductAndDescription.md)
* [[Production].[vProductModelCatalogDescription]](../../Views/vProductModelCatalogDescription.md)
* [[Production].[vProductModelInstructions]](../../Views/vProductModelInstructions.md)
* [[Production].[ManuInstructionsSchemaCollection]](../../Programmability/Types/XML_Schema_Collections/ManuInstructionsSchemaCollection.md)
* [[Production].[ProductDescriptionSchemaCollection]](../../Programmability/Types/XML_Schema_Collections/ProductDescriptionSchemaCollection.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

