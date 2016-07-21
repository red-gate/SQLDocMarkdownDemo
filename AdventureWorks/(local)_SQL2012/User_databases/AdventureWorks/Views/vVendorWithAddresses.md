#### asdasdasd

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Views](Views.md) > Purchasing.vVendorWithAddresses

# ![Views](../../../../Images/View32.png) [Purchasing].[vVendorWithAddresses]

---

## <a name="#description"></a>MS_Description

Vendor (company) names and addresses .

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| ANSI Nulls On | YES |
| Quoted Identifier On | YES |
| Created | 13:14:55 14 March 2012 |
| Last Modified | 13:14:55 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Name |
|---|
| BusinessEntityID |
| Name |
| AddressType |
| AddressLine1 |
| AddressLine2 |
| City |
| StateProvinceName |
| PostalCode |
| CountryRegionName |


---

## <a name="#sqlscript"></a>SQL Script

```sql

CREATE VIEW [Purchasing].[vVendorWithAddresses] AS 
SELECT 
    v.[BusinessEntityID]
    ,v.[Name]
    ,at.[Name] AS [AddressType]
    ,a.[AddressLine1] 
    ,a.[AddressLine2] 
    ,a.[City] 
    ,sp.[Name] AS [StateProvinceName] 
    ,a.[PostalCode] 
    ,cr.[Name] AS [CountryRegionName] 
FROM [Purchasing].[Vendor] v
    INNER JOIN [Person].[BusinessEntityAddress] bea 
    ON bea.[BusinessEntityID] = v.[BusinessEntityID] 
    INNER JOIN [Person].[Address] a 
    ON a.[AddressID] = bea.[AddressID]
    INNER JOIN [Person].[StateProvince] sp 
    ON sp.[StateProvinceID] = a.[StateProvinceID]
    INNER JOIN [Person].[CountryRegion] cr 
    ON cr.[CountryRegionCode] = sp.[CountryRegionCode]
    INNER JOIN [Person].[AddressType] at 
    ON at.[AddressTypeID] = bea.[AddressTypeID];
GO
EXEC sp_addextendedproperty N'MS_Description', N'Vendor (company) names and addresses .', 'SCHEMA', N'Purchasing', 'VIEW', N'vVendorWithAddresses', NULL, NULL
GO

```


---

## <a name="#uses"></a>Uses

* [[Person].[Address]](../Tables/Address.md)
* [[Person].[AddressType]](../Tables/AddressType.md)
* [[Person].[BusinessEntityAddress]](../Tables/BusinessEntityAddress.md)
* [[Person].[CountryRegion]](../Tables/CountryRegion.md)
* [[Person].[StateProvince]](../Tables/StateProvince.md)
* [[Purchasing].[Vendor]](../Tables/Vendor.md)
* [Purchasing](../Security/Schemas/Purchasing.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 14:15

