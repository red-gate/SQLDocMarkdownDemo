#### 

[Project](../../../../../../index.md) > [(local)\\SQL2012](../../../../../index.md) > [User databases](../../../../index.md) > [AdventureWorks](../../../index.md) > [Programmability](../../index.md) > [Functions](../index.md) > [Scalar-valued Functions](Scalar-valued_Functions.md) > dbo.ufnGetAccountingEndDate

# ![Scalar-valued Functions](../../../../../../Images/Function_Scalar32.png) [dbo].[ufnGetAccountingEndDate]

---

## <a name="#description"></a>MS_Description

Scalar function used in the uSalesOrderHeader trigger to set the starting account date.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| ANSI Nulls On | YES |
| Quoted Identifier On | YES |


---

## <a name="#sqlscript"></a>SQL Script

```sql

CREATE FUNCTION [dbo].[ufnGetAccountingEndDate]()
RETURNS [datetime] 
AS 
BEGIN
    RETURN DATEADD(millisecond, -2, CONVERT(datetime, '20040701', 112));
END;
GO
EXEC sp_addextendedproperty N'MS_Description', N'Scalar function used in the uSalesOrderHeader trigger to set the starting account date.', 'SCHEMA', N'dbo', 'FUNCTION', N'ufnGetAccountingEndDate', NULL, NULL
GO

```


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

