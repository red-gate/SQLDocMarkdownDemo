#### 

[Project](../../../../../../index.md) > [(local)\\SQL2012](../../../../../index.md) > [User databases](../../../../index.md) > [AdventureWorks](../../../index.md) > [Programmability](../../index.md) > [Functions](../index.md) > [Scalar-valued Functions](Scalar-valued_Functions.md) > dbo.ufnGetStock

# ![Scalar-valued Functions](../../../../../../Images/Function_Scalar32.png) [dbo].[ufnGetStock]

---

## <a name="#description"></a>MS_Description

Scalar function returning the quantity of inventory in LocationID 6 (Miscellaneous Storage)for a specified ProductID.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| ANSI Nulls On | YES |
| Quoted Identifier On | YES |


---

## <a name="#parameters"></a>Parameters

| Name | Data Type | Max Length (Bytes) | Description |
|---|---|---|---|
| @ProductID | int | 4 | _Input parameter for the scalar function ufnGetStock. Enter a valid ProductID from the Production.ProductInventory table._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql

CREATE FUNCTION [dbo].[ufnGetStock](@ProductID [int])
RETURNS [int] 
AS 
-- Returns the stock level for the product. This function is used internally only
BEGIN
    DECLARE @ret int;
    
    SELECT @ret = SUM(p.[Quantity]) 
    FROM [Production].[ProductInventory] p 
    WHERE p.[ProductID] = @ProductID 
        AND p.[LocationID] = '6'; -- Only look at inventory in the misc storage
    
    IF (@ret IS NULL) 
        SET @ret = 0
    
    RETURN @ret
END;
GO
EXEC sp_addextendedproperty N'MS_Description', N'Scalar function returning the quantity of inventory in LocationID 6 (Miscellaneous Storage)for a specified ProductID.', 'SCHEMA', N'dbo', 'FUNCTION', N'ufnGetStock', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Input parameter for the scalar function ufnGetStock. Enter a valid ProductID from the Production.ProductInventory table.', 'SCHEMA', N'dbo', 'FUNCTION', N'ufnGetStock', 'PARAMETER', N'@ProductID'
GO

```


---

## <a name="#uses"></a>Uses

DEPENDENCYLIST* [[Production].[ProductInventory]](../../../Tables/ProductInventory.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

