#### 

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Views](Views.md) > Sales.vSalesPersonSalesByFiscalYears

# ![Views](../../../../Images/View32.png) [Sales].[vSalesPersonSalesByFiscalYears]

---

## <a name="#description"></a>MS_Description

Uses PIVOT to return aggregated sales information for each sales representative.

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
| SalesPersonID |
| FullName |
| JobTitle |
| SalesTerritory |
| 2002 |
| 2003 |
| 2004 |


---

## <a name="#sqlscript"></a>SQL Script

```sql

CREATE VIEW [Sales].[vSalesPersonSalesByFiscalYears] 
AS 
SELECT 
    pvt.[SalesPersonID]
    ,pvt.[FullName]
    ,pvt.[JobTitle]
    ,pvt.[SalesTerritory]
    ,pvt.[2002]
    ,pvt.[2003]
    ,pvt.[2004] 
FROM (SELECT 
        soh.[SalesPersonID]
        ,p.[FirstName] + ' ' + COALESCE(p.[MiddleName], '') + ' ' + p.[LastName] AS [FullName]
        ,e.[JobTitle]
        ,st.[Name] AS [SalesTerritory]
        ,soh.[SubTotal]
        ,YEAR(DATEADD(m, 6, soh.[OrderDate])) AS [FiscalYear] 
    FROM [Sales].[SalesPerson] sp 
        INNER JOIN [Sales].[SalesOrderHeader] soh 
        ON sp.[BusinessEntityID] = soh.[SalesPersonID]
        INNER JOIN [Sales].[SalesTerritory] st 
        ON sp.[TerritoryID] = st.[TerritoryID] 
        INNER JOIN [HumanResources].[Employee] e 
        ON soh.[SalesPersonID] = e.[BusinessEntityID] 
		INNER JOIN [Person].[Person] p
		ON p.[BusinessEntityID] = sp.[BusinessEntityID]
	 ) AS soh 
PIVOT 
(
    SUM([SubTotal]) 
    FOR [FiscalYear] 
    IN ([2002], [2003], [2004])
) AS pvt;
GO
EXEC sp_addextendedproperty N'MS_Description', N'Uses PIVOT to return aggregated sales information for each sales representative.', 'SCHEMA', N'Sales', 'VIEW', N'vSalesPersonSalesByFiscalYears', NULL, NULL
GO

```


---

## <a name="#uses"></a>Uses

DEPENDENCYLIST* [[HumanResources].[Employee]](../Tables/Employee.md)
* [[Person].[Person]](../Tables/Person.md)
* [[Sales].[SalesOrderHeader]](../Tables/SalesOrderHeader.md)
* [[Sales].[SalesPerson]](../Tables/SalesPerson.md)
* [[Sales].[SalesTerritory]](../Tables/SalesTerritory.md)
* [Sales](../Security/Schemas/Sales.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

