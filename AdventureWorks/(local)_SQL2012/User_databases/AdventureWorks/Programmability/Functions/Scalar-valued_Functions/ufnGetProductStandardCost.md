#### 

[Project](../../../../../../index.md) > [(local)\\SQL2012](../../../../../index.md) > [User databases](../../../../index.md) > [AdventureWorks](../../../index.md) > [Programmability](../../index.md) > [Functions](../index.md) > [Scalar-valued Functions](Scalar-valued_Functions.md) > dbo.ufnGetProductStandardCost

# ![Scalar-valued Functions](../../../../../../Images/Function_Scalar32.png) [dbo].[ufnGetProductStandardCost]

---

## <a name="#description"></a>MS_Description

Scalar function returning the standard cost for a given product on a particular order date.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| ANSI Nulls On | YES |
| Quoted Identifier On | YES |


---

## <a name="#parameters"></a>Parameters

| Name | Data Type | Max Length (Bytes) | Description |
|---|---|---|---|
| @ProductID | int | 4 | _Input parameter for the scalar function ufnGetProductStandardCost. Enter a valid ProductID from the Production.Product table._ |
| @OrderDate | datetime | 8 | _Input parameter for the scalar function ufnGetProductStandardCost. Enter a valid order date._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql

CREATE FUNCTION [dbo].[ufnGetProductStandardCost](@ProductID [int], @OrderDate [datetime])
RETURNS [money] 
AS 
-- Returns the standard cost for the product on a specific date.
BEGIN
    DECLARE @StandardCost money;

    SELECT @StandardCost = pch.[StandardCost] 
    FROM [Production].[Product] p 
        INNER JOIN [Production].[ProductCostHistory] pch 
        ON p.[ProductID] = pch.[ProductID] 
            AND p.[ProductID] = @ProductID 
            AND @OrderDate BETWEEN pch.[StartDate] AND COALESCE(pch.[EndDate], CONVERT(datetime, '99991231', 112)); -- Make sure we get all the prices!

    RETURN @StandardCost;
END;
GO
EXEC sp_addextendedproperty N'MS_Description', N'Scalar function returning the standard cost for a given product on a particular order date.', 'SCHEMA', N'dbo', 'FUNCTION', N'ufnGetProductStandardCost', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Input parameter for the scalar function ufnGetProductStandardCost. Enter a valid order date.', 'SCHEMA', N'dbo', 'FUNCTION', N'ufnGetProductStandardCost', 'PARAMETER', N'@OrderDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Input parameter for the scalar function ufnGetProductStandardCost. Enter a valid ProductID from the Production.Product table.', 'SCHEMA', N'dbo', 'FUNCTION', N'ufnGetProductStandardCost', 'PARAMETER', N'@ProductID'
GO

```


---

## <a name="#uses"></a>Uses

DEPENDENCYLIST* [[Production].[Product]](../../../Tables/Product.md)
* [[Production].[ProductCostHistory]](../../../Tables/ProductCostHistory.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

