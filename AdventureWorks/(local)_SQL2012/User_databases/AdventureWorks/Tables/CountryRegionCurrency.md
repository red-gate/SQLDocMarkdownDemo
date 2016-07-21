#### asdasdasd

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Sales.CountryRegionCurrency

# ![Tables](../../../../Images/Table32.png) [Sales].[CountryRegionCurrency]

---

## <a name="#description"></a>MS_Description

Cross-reference table mapping ISO currency codes to a country or region.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 109 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:53 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Default | Description |
|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_CountryRegionCurrency_CountryRegionCode_CurrencyCode: CountryRegionCode\CurrencyCode](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_CountryRegionCurrency_CountryRegion_CountryRegionCode: [Person].[CountryRegion].CountryRegionCode](../../../../Images/fk.png)](#foreignkeys) | CountryRegionCode | nvarchar(3) | 6 | NO |  | _ISO code for countries and regions. Foreign key to CountryRegion.CountryRegionCode._ |
| [![Cluster Primary Key PK_CountryRegionCurrency_CountryRegionCode_CurrencyCode: CountryRegionCode\CurrencyCode](../../../../Images/pkcluster.png)](#indexes)[![Indexes IX_CountryRegionCurrency_CurrencyCode](../../../../Images/Index.png)](#indexes)[![Foreign Keys FK_CountryRegionCurrency_Currency_CurrencyCode: [Sales].[Currency].CurrencyCode](../../../../Images/fk.png)](#foreignkeys) | CurrencyCode | nchar(3) | 6 | NO |  | _ISO standard currency code. Foreign key to Currency.CurrencyCode._ |
|  | ModifiedDate | datetime | 8 | NO | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_CountryRegionCurrency_CountryRegionCode_CurrencyCode: CountryRegionCode\CurrencyCode](../../../../Images/pkcluster.png)](#indexes) | PK_CountryRegionCurrency_CountryRegionCode_CurrencyCode | CountryRegionCode, CurrencyCode | YES | _Primary key (clustered) constraint_ |
|  | IX_CountryRegionCurrency_CurrencyCode | CurrencyCode |  | _Nonclustered index._ |


---

## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_CountryRegionCurrency_CountryRegion_CountryRegionCode | CountryRegionCode->[[Person].[CountryRegion].[CountryRegionCode]](CountryRegion.md) | _Foreign key constraint referencing CountryRegion.CountryRegionCode._ |
| FK_CountryRegionCurrency_Currency_CurrencyCode | CurrencyCode->[[Sales].[Currency].[CurrencyCode]](Currency.md) | _Foreign key constraint referencing Currency.CurrencyCode._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Sales].[CountryRegionCurrency]
(
[CountryRegionCode] [nvarchar] (3) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[CurrencyCode] [nchar] (3) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_CountryRegionCurrency_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Sales].[CountryRegionCurrency] ADD CONSTRAINT [PK_CountryRegionCurrency_CountryRegionCode_CurrencyCode] PRIMARY KEY CLUSTERED  ([CountryRegionCode], [CurrencyCode]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_CountryRegionCurrency_CurrencyCode] ON [Sales].[CountryRegionCurrency] ([CurrencyCode]) ON [PRIMARY]
GO
ALTER TABLE [Sales].[CountryRegionCurrency] ADD CONSTRAINT [FK_CountryRegionCurrency_CountryRegion_CountryRegionCode] FOREIGN KEY ([CountryRegionCode]) REFERENCES [Person].[CountryRegion] ([CountryRegionCode])
GO
ALTER TABLE [Sales].[CountryRegionCurrency] ADD CONSTRAINT [FK_CountryRegionCurrency_Currency_CurrencyCode] FOREIGN KEY ([CurrencyCode]) REFERENCES [Sales].[Currency] ([CurrencyCode])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Cross-reference table mapping ISO currency codes to a country or region.', 'SCHEMA', N'Sales', 'TABLE', N'CountryRegionCurrency', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'ISO code for countries and regions. Foreign key to CountryRegion.CountryRegionCode.', 'SCHEMA', N'Sales', 'TABLE', N'CountryRegionCurrency', 'COLUMN', N'CountryRegionCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'ISO standard currency code. Foreign key to Currency.CurrencyCode.', 'SCHEMA', N'Sales', 'TABLE', N'CountryRegionCurrency', 'COLUMN', N'CurrencyCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Sales', 'TABLE', N'CountryRegionCurrency', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Sales', 'TABLE', N'CountryRegionCurrency', 'CONSTRAINT', N'DF_CountryRegionCurrency_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing CountryRegion.CountryRegionCode.', 'SCHEMA', N'Sales', 'TABLE', N'CountryRegionCurrency', 'CONSTRAINT', N'FK_CountryRegionCurrency_CountryRegion_CountryRegionCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Currency.CurrencyCode.', 'SCHEMA', N'Sales', 'TABLE', N'CountryRegionCurrency', 'CONSTRAINT', N'FK_CountryRegionCurrency_Currency_CurrencyCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Sales', 'TABLE', N'CountryRegionCurrency', 'CONSTRAINT', N'PK_CountryRegionCurrency_CountryRegionCode_CurrencyCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Nonclustered index.', 'SCHEMA', N'Sales', 'TABLE', N'CountryRegionCurrency', 'INDEX', N'IX_CountryRegionCurrency_CurrencyCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Sales', 'TABLE', N'CountryRegionCurrency', 'INDEX', N'PK_CountryRegionCurrency_CountryRegionCode_CurrencyCode'
GO

```


---

## <a name="#uses"></a>Uses

* [[Person].[CountryRegion]](CountryRegion.md)
* [[Sales].[Currency]](Currency.md)
* [Sales](../Security/Schemas/Sales.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 12:25

