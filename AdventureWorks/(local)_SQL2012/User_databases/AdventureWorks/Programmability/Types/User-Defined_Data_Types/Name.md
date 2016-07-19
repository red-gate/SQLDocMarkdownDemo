
# ![User-Defined Data Types](../../../../../../Images/UserDefinedDataType32.png) [dbo].[Name]

[Project](../../../../../../index.md) > [(local)\\SQL2012](../../../../../index.md) > [User databases](../../../../index.md) > [AdventureWorks](../../../index.md) > [Programmability](../../index.md) > [Types](../index.md) > [User-Defined Data Types](User-Defined_Data_Types_.md) > dbo.Name

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Allow Nulls | YES |
| Base Type Name | nvarchar |
| Length | 50 |


## <a name="#sqlscript"></a>SQL Script
```sql
CREATE TYPE [dbo].[Name] FROM nvarchar (50) NULL
GO

```

## <a name="#usedby"></a>Used By
DEPENDENCYLIST
* [[HumanResources].[Department]](../../../Tables/Department.md)
* [[HumanResources].[Shift]](../../../Tables/Shift.md)
* [[Person].[AddressType]](../../../Tables/AddressType.md)
* [[Person].[ContactType]](../../../Tables/ContactType.md)
* [[Person].[CountryRegion]](../../../Tables/CountryRegion.md)
* [[Person].[Person]](../../../Tables/Person.md)
* [[Person].[PhoneNumberType]](../../../Tables/PhoneNumberType.md)
* [[Person].[StateProvince]](../../../Tables/StateProvince.md)
* [[Production].[Culture]](../../../Tables/Culture.md)
* [[Production].[Location]](../../../Tables/Location.md)
* [[Production].[Product]](../../../Tables/Product.md)
* [[Production].[ProductCategory]](../../../Tables/ProductCategory.md)
* [[Production].[ProductModel]](../../../Tables/ProductModel.md)
* [[Production].[ProductReview]](../../../Tables/ProductReview.md)
* [[Production].[ProductSubcategory]](../../../Tables/ProductSubcategory.md)
* [[Production].[ScrapReason]](../../../Tables/ScrapReason.md)
* [[Production].[UnitMeasure]](../../../Tables/UnitMeasure.md)
* [[Purchasing].[ShipMethod]](../../../Tables/ShipMethod.md)
* [[Purchasing].[Vendor]](../../../Tables/Vendor.md)
* [[Sales].[Currency]](../../../Tables/Currency.md)
* [[Sales].[SalesReason]](../../../Tables/SalesReason.md)
* [[Sales].[SalesTaxRate]](../../../Tables/SalesTaxRate.md)
* [[Sales].[SalesTerritory]](../../../Tables/SalesTerritory.md)
* [[Sales].[Store]](../../../Tables/Store.md)

FOOTER: FOOTER: Author:  Chris Whitworth
FOOTER: Created: 19 July 2016 09:34
FOOTER: Copyright 2016 - All Rights Reserved

