#### asdasdasd

[Project](../../../../../../index.md) > [(local)\\SQL2012](../../../../../index.md) > [User databases](../../../../index.md) > [AdventureWorks](../../../index.md) > [Programmability](../../index.md) > [Types](../index.md) > [User-Defined Data Types](User-Defined_Data_Types.md) > dbo.Flag

# ![User-Defined Data Types](../../../../../../Images/UserDefinedDataType32.png) [dbo].[Flag]

---

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Allow Nulls | NO |
| Base Type Name | bit |
| Length | 1 |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TYPE [dbo].[Flag] FROM bit NOT NULL
GO

```


---

## <a name="#usedby"></a>Used By

* [[HumanResources].[Employee]](../../../Tables/Employee.md)
* [[Person].[StateProvince]](../../../Tables/StateProvince.md)
* [[Production].[Product]](../../../Tables/Product.md)
* [[Production].[ProductProductPhoto]](../../../Tables/ProductProductPhoto.md)
* [[Purchasing].[Vendor]](../../../Tables/Vendor.md)
* [[Sales].[SalesOrderHeader]](../../../Tables/SalesOrderHeader.md)
* [[HumanResources].[uspUpdateEmployeeHireInfo]](../../Stored_Procedures/uspUpdateEmployeeHireInfo.md)
* [[HumanResources].[uspUpdateEmployeeLogin]](../../Stored_Procedures/uspUpdateEmployeeLogin.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 12:25

