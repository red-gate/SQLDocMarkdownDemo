#### asdasdasd

[Project](../../../../../../index.md) > [(local)\\SQL2012](../../../../../index.md) > [User databases](../../../../index.md) > [AdventureWorks](../../../index.md) > [Programmability](../../index.md) > [Types](../index.md) > [User-Defined Data Types](User-Defined_Data_Types.md) > dbo.OrderNumber

# ![User-Defined Data Types](../../../../../../Images/UserDefinedDataType32.png) [dbo].[OrderNumber]

---

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Allow Nulls | YES |
| Base Type Name | nvarchar |
| Length | 25 |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TYPE [dbo].[OrderNumber] FROM nvarchar (25) NULL
GO

```


---

## <a name="#usedby"></a>Used By

* [[Sales].[SalesOrderHeader]](../../../Tables/SalesOrderHeader.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 12:25

