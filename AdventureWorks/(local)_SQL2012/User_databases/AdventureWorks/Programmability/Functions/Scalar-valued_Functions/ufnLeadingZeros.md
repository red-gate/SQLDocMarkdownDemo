#### asdasdasd

[Project](../../../../../../index.md) > [(local)\\SQL2012](../../../../../index.md) > [User databases](../../../../index.md) > [AdventureWorks](../../../index.md) > [Programmability](../../index.md) > [Functions](../index.md) > [Scalar-valued Functions](Scalar-valued_Functions.md) > dbo.ufnLeadingZeros

# ![Scalar-valued Functions](../../../../../../Images/Function_Scalar32.png) [dbo].[ufnLeadingZeros]

---

## <a name="#description"></a>MS_Description

Scalar function used by the Sales.Customer table to help set the account number.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| ANSI Nulls On | YES |
| Quoted Identifier On | YES |
| Schema Bound | YES |


---

## <a name="#parameters"></a>Parameters

| Name | Data Type | Max Length (Bytes) | Description |
|---|---|---|---|
| @Value | int | 4 | _Input parameter for the scalar function ufnLeadingZeros. Enter a valid integer._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql

CREATE FUNCTION [dbo].[ufnLeadingZeros](
    @Value int
) 
RETURNS varchar(8) 
WITH SCHEMABINDING 
AS 
BEGIN
    DECLARE @ReturnValue varchar(8);

    SET @ReturnValue = CONVERT(varchar(8), @Value);
    SET @ReturnValue = REPLICATE('0', 8 - DATALENGTH(@ReturnValue)) + @ReturnValue;

    RETURN (@ReturnValue);
END;
GO
EXEC sp_addextendedproperty N'MS_Description', N'Scalar function used by the Sales.Customer table to help set the account number.', 'SCHEMA', N'dbo', 'FUNCTION', N'ufnLeadingZeros', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Input parameter for the scalar function ufnLeadingZeros. Enter a valid integer.', 'SCHEMA', N'dbo', 'FUNCTION', N'ufnLeadingZeros', 'PARAMETER', N'@Value'
GO

```


---

## <a name="#usedby"></a>Used By

* [[Sales].[Customer]](../../../Tables/Customer.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 14:15

