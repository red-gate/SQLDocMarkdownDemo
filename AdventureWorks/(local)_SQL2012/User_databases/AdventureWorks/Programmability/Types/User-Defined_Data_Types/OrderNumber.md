
# ![User-Defined Data Types](../../../../../../Images/UserDefinedDataType32.png) [dbo].[OrderNumber]

[Project](../../../../../../index.md) > [(local)\\SQL2012](../../../../../index.md) > [User databases](../../../../index.md) > [AdventureWorks](../../../index.md) > [Programmability](../../index.md) > [Types](../index.md) > [User-Defined Data Types](User-Defined_Data_Types_.md) > dbo.OrderNumber

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Allow Nulls | YES |
| Base Type Name | nvarchar |
| Length | 25 |


## <a name="#sqlscript"></a>SQL Script
```sql
CREATE TYPE [dbo].[OrderNumber] FROM nvarchar (25) NULL
GO

```

## <a name="#usedby"></a>Used By
DEPENDENCYLIST
* [[Sales].[SalesOrderHeader]](../../../Tables/SalesOrderHeader.md)

FOOTER: FOOTER: Author:  Chris Whitworth
FOOTER: Created: 19 July 2016 09:34
FOOTER: Copyright 2016 - All Rights Reserved
