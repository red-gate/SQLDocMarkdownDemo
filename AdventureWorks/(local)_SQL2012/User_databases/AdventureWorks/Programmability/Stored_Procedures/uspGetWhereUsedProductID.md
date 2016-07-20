#### 

[Project](../../../../../index.md) > [(local)\\SQL2012](../../../../index.md) > [User databases](../../../index.md) > [AdventureWorks](../../index.md) > [Programmability](../index.md) > [Stored Procedures](Stored_Procedures.md) > dbo.uspGetWhereUsedProductID

# ![Stored Procedures](../../../../../Images/StoredProcedure32.png) [dbo].[uspGetWhereUsedProductID]

---

## <a name="#description"></a>MS_Description

Stored procedure using a recursive query to return all components or assemblies that directly or indirectly use the specified ProductID.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| ANSI Nulls On | YES |
| Quoted Identifier On | YES |


---

## <a name="#parameters"></a>Parameters

| Name | Data Type | Max Length (Bytes) | Description |
|---|---|---|---|
| @StartProductID | int | 4 | _Input parameter for the stored procedure uspGetWhereUsedProductID. Enter a valid ProductID from the Production.Product table._ |
| @CheckDate | datetime | 8 | _Input parameter for the stored procedure uspGetWhereUsedProductID used to eliminate components not used after that date. Enter a valid date._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql

CREATE PROCEDURE [dbo].[uspGetWhereUsedProductID]
    @StartProductID [int],
    @CheckDate [datetime]
AS
BEGIN
    SET NOCOUNT ON;

    --Use recursive query to generate a multi-level Bill of Material (i.e. all level 1 components of a level 0 assembly, all level 2 components of a level 1 assembly)
    WITH [BOM_cte]([ProductAssemblyID], [ComponentID], [ComponentDesc], [PerAssemblyQty], [StandardCost], [ListPrice], [BOMLevel], [RecursionLevel]) -- CTE name and columns
    AS (
        SELECT b.[ProductAssemblyID], b.[ComponentID], p.[Name], b.[PerAssemblyQty], p.[StandardCost], p.[ListPrice], b.[BOMLevel], 0 -- Get the initial list of components for the bike assembly
        FROM [Production].[BillOfMaterials] b
            INNER JOIN [Production].[Product] p 
            ON b.[ProductAssemblyID] = p.[ProductID] 
        WHERE b.[ComponentID] = @StartProductID 
            AND @CheckDate >= b.[StartDate] 
            AND @CheckDate <= ISNULL(b.[EndDate], @CheckDate)
        UNION ALL
        SELECT b.[ProductAssemblyID], b.[ComponentID], p.[Name], b.[PerAssemblyQty], p.[StandardCost], p.[ListPrice], b.[BOMLevel], [RecursionLevel] + 1 -- Join recursive member to anchor
        FROM [BOM_cte] cte
            INNER JOIN [Production].[BillOfMaterials] b 
            ON cte.[ProductAssemblyID] = b.[ComponentID]
            INNER JOIN [Production].[Product] p 
            ON b.[ProductAssemblyID] = p.[ProductID] 
        WHERE @CheckDate >= b.[StartDate] 
            AND @CheckDate <= ISNULL(b.[EndDate], @CheckDate)
        )
    -- Outer select from the CTE
    SELECT b.[ProductAssemblyID], b.[ComponentID], b.[ComponentDesc], SUM(b.[PerAssemblyQty]) AS [TotalQuantity] , b.[StandardCost], b.[ListPrice], b.[BOMLevel], b.[RecursionLevel]
    FROM [BOM_cte] b
    GROUP BY b.[ComponentID], b.[ComponentDesc], b.[ProductAssemblyID], b.[BOMLevel], b.[RecursionLevel], b.[StandardCost], b.[ListPrice]
    ORDER BY b.[BOMLevel], b.[ProductAssemblyID], b.[ComponentID]
    OPTION (MAXRECURSION 25) 
END;
GO
EXEC sp_addextendedproperty N'MS_Description', N'Stored procedure using a recursive query to return all components or assemblies that directly or indirectly use the specified ProductID.', 'SCHEMA', N'dbo', 'PROCEDURE', N'uspGetWhereUsedProductID', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Input parameter for the stored procedure uspGetWhereUsedProductID used to eliminate components not used after that date. Enter a valid date.', 'SCHEMA', N'dbo', 'PROCEDURE', N'uspGetWhereUsedProductID', 'PARAMETER', N'@CheckDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Input parameter for the stored procedure uspGetWhereUsedProductID. Enter a valid ProductID from the Production.Product table.', 'SCHEMA', N'dbo', 'PROCEDURE', N'uspGetWhereUsedProductID', 'PARAMETER', N'@StartProductID'
GO

```


---

## <a name="#uses"></a>Uses

DEPENDENCYLIST* [[Production].[BillOfMaterials]](../../Tables/BillOfMaterials.md)
* [[Production].[Product]](../../Tables/Product.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

