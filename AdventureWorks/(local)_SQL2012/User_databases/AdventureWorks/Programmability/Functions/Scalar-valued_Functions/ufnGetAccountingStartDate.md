
# ![Scalar-valued Functions](../../../../../../Images/Function_Scalar32.png) [dbo].[ufnGetAccountingStartDate]

[Project](../../../../../../index.md) > [(local)\\SQL2012](../../../../../index.md) > [User databases](../../../../index.md) > [AdventureWorks](../../../index.md) > [Programmability](../../index.md) > [Functions](../index.md) > [Scalar-valued Functions](Scalar-valued_Functions_.md) > dbo.ufnGetAccountingStartDate

## <a name="#description"></a>MS_Description
Scalar function used in the uSalesOrderHeader trigger to set the ending account date.
## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| ANSI Nulls On | YES |
| Quoted Identifier On | YES |


## <a name="#sqlscript"></a>SQL Script
```sql

CREATE FUNCTION [dbo].[ufnGetAccountingStartDate]()
RETURNS [datetime] 
AS 
BEGIN
    RETURN CONVERT(datetime, '20030701', 112);
END;
GO
EXEC sp_addextendedproperty N'MS_Description', N'Scalar function used in the uSalesOrderHeader trigger to set the ending account date.', 'SCHEMA', N'dbo', 'FUNCTION', N'ufnGetAccountingStartDate', NULL, NULL
GO

```
FOOTER: FOOTER: Author:  Chris Whitworth
FOOTER: Created: 19 July 2016 09:34
FOOTER: Copyright 2016 - All Rights Reserved
