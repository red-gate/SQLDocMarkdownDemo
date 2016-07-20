#### 

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Views](Views.md) > Sales.vSalesPerson

# ![Views](../../../../Images/View32.png) [Sales].[vSalesPerson]

---

## <a name="#description"></a>MS_Description

Sales representiatives (names and addresses) and their sales-related information.

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
| Title |
| FirstName |
| MiddleName |
| LastName |
| Suffix |
| JobTitle |
| PhoneNumber |
| PhoneNumberType |
| EmailAddress |
| EmailPromotion |
| AddressLine1 |
| AddressLine2 |
| City |
| StateProvinceName |
| PostalCode |
| CountryRegionName |
| TerritoryName |
| TerritoryGroup |
| SalesQuota |
| SalesYTD |
| SalesLastYear |


---

## <a name="#sqlscript"></a>SQL Script

```sql

CREATE VIEW [Sales].[vSalesPerson] 
AS 
SELECT 
    s.[BusinessEntityID]
    ,p.[Title]
    ,p.[FirstName]
    ,p.[MiddleName]
    ,p.[LastName]
    ,p.[Suffix]
    ,e.[JobTitle]
    ,pp.[PhoneNumber]
	,pnt.[Name] AS [PhoneNumberType]
    ,ea.[EmailAddress]
    ,p.[EmailPromotion]
    ,a.[AddressLine1]
    ,a.[AddressLine2]
    ,a.[City]
    ,[StateProvinceName] = sp.[Name]
    ,a.[PostalCode]
    ,[CountryRegionName] = cr.[Name]
    ,[TerritoryName] = st.[Name]
    ,[TerritoryGroup] = st.[Group]
    ,s.[SalesQuota]
    ,s.[SalesYTD]
    ,s.[SalesLastYear]
FROM [Sales].[SalesPerson] s
    INNER JOIN [HumanResources].[Employee] e 
    ON e.[BusinessEntityID] = s.[BusinessEntityID]
	INNER JOIN [Person].[Person] p
	ON p.[BusinessEntityID] = s.[BusinessEntityID]
    INNER JOIN [Person].[BusinessEntityAddress] bea 
    ON bea.[BusinessEntityID] = s.[BusinessEntityID] 
    INNER JOIN [Person].[Address] a 
    ON a.[AddressID] = bea.[AddressID]
    INNER JOIN [Person].[StateProvince] sp 
    ON sp.[StateProvinceID] = a.[StateProvinceID]
    INNER JOIN [Person].[CountryRegion] cr 
    ON cr.[CountryRegionCode] = sp.[CountryRegionCode]
    LEFT OUTER JOIN [Sales].[SalesTerritory] st 
    ON st.[TerritoryID] = s.[TerritoryID]
	LEFT OUTER JOIN [Person].[EmailAddress] ea
	ON ea.[BusinessEntityID] = p.[BusinessEntityID]
	LEFT OUTER JOIN [Person].[PersonPhone] pp
	ON pp.[BusinessEntityID] = p.[BusinessEntityID]
	LEFT OUTER JOIN [Person].[PhoneNumberType] pnt
	ON pnt.[PhoneNumberTypeID] = pp.[PhoneNumberTypeID];
GO
EXEC sp_addextendedproperty N'MS_Description', N'Sales representiatives (names and addresses) and their sales-related information.', 'SCHEMA', N'Sales', 'VIEW', N'vSalesPerson', NULL, NULL
GO

```


---

## <a name="#uses"></a>Uses

DEPENDENCYLIST* [[HumanResources].[Employee]](../Tables/Employee.md)
* [[Person].[Address]](../Tables/Address.md)
* [[Person].[BusinessEntityAddress]](../Tables/BusinessEntityAddress.md)
* [[Person].[CountryRegion]](../Tables/CountryRegion.md)
* [[Person].[EmailAddress]](../Tables/EmailAddress.md)
* [[Person].[Person]](../Tables/Person.md)
* [[Person].[PersonPhone]](../Tables/PersonPhone.md)
* [[Person].[PhoneNumberType]](../Tables/PhoneNumberType.md)
* [[Person].[StateProvince]](../Tables/StateProvince.md)
* [[Sales].[SalesPerson]](../Tables/SalesPerson.md)
* [[Sales].[SalesTerritory]](../Tables/SalesTerritory.md)
* [Sales](../Security/Schemas/Sales.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

