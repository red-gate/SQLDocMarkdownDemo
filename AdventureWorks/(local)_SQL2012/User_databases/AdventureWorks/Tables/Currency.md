#### asdasdasd

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Sales.Currency

# ![Tables](../../../../Images/Table32.png) [Sales].[Currency]

---

## <a name="#description"></a>MS_Description

Lookup table containing standard ISO currencies.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 105 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:54 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Default | Description |
|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_Currency_CurrencyCode: CurrencyCode](../../../../Images/pkcluster.png)](#indexes) | CurrencyCode | nchar(3) | 6 | NO |  | _The ISO code for the Currency._ |
| [![Indexes AK_Currency_Name](../../../../Images/Index.png)](#indexes) | Name | [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md) | 100 | NO |  | _Currency name._ |
|  | ModifiedDate | datetime | 8 | NO | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_Currency_CurrencyCode: CurrencyCode](../../../../Images/pkcluster.png)](#indexes) | PK_Currency_CurrencyCode | CurrencyCode | YES | _Primary key (clustered) constraint_ |
|  | AK_Currency_Name | Name | YES | _Unique nonclustered index._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Sales].[Currency]
(
[CurrencyCode] [nchar] (3) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[Name] [dbo].[Name] NOT NULL,
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_Currency_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Sales].[Currency] ADD CONSTRAINT [PK_Currency_CurrencyCode] PRIMARY KEY CLUSTERED  ([CurrencyCode]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_Currency_Name] ON [Sales].[Currency] ([Name]) ON [PRIMARY]
GO
EXEC sp_addextendedproperty N'MS_Description', N'Lookup table containing standard ISO currencies.', 'SCHEMA', N'Sales', 'TABLE', N'Currency', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'The ISO code for the Currency.', 'SCHEMA', N'Sales', 'TABLE', N'Currency', 'COLUMN', N'CurrencyCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Sales', 'TABLE', N'Currency', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Currency name.', 'SCHEMA', N'Sales', 'TABLE', N'Currency', 'COLUMN', N'Name'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Sales', 'TABLE', N'Currency', 'CONSTRAINT', N'DF_Currency_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Sales', 'TABLE', N'Currency', 'CONSTRAINT', N'PK_Currency_CurrencyCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index.', 'SCHEMA', N'Sales', 'TABLE', N'Currency', 'INDEX', N'AK_Currency_Name'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Sales', 'TABLE', N'Currency', 'INDEX', N'PK_Currency_CurrencyCode'
GO

```


---

## <a name="#uses"></a>Uses

* [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md)
* [Sales](../Security/Schemas/Sales.md)


---

## <a name="#usedby"></a>Used By

* [[Sales].[CountryRegionCurrency]](CountryRegionCurrency.md)
* [[Sales].[CurrencyRate]](CurrencyRate.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 14:15

