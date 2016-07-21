#### asdasdasd

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Sales.CurrencyRate

# ![Tables](../../../../Images/Table32.png) [Sales].[CurrencyRate]

---

## <a name="#description"></a>MS_Description

Currency exchange rates.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 13532 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:54 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Identity | Default | Description |
|---|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_CurrencyRate_CurrencyRateID: CurrencyRateID](../../../../Images/pkcluster.png)](#indexes) | CurrencyRateID | int | 4 | NO | 1 - 1 |  | _Primary key for CurrencyRate records._ |
| [![Indexes AK_CurrencyRate_CurrencyRateDate_FromCurrencyCode_ToCurrencyCode](../../../../Images/Index.png)](#indexes) | CurrencyRateDate | datetime | 8 | NO |  |  | _Date and time the exchange rate was obtained._ |
| [![Indexes AK_CurrencyRate_CurrencyRateDate_FromCurrencyCode_ToCurrencyCode](../../../../Images/Index.png)](#indexes)[![Foreign Keys FK_CurrencyRate_Currency_FromCurrencyCode: [Sales].[Currency].FromCurrencyCode](../../../../Images/fk.png)](#foreignkeys) | FromCurrencyCode | nchar(3) | 6 | NO |  |  | _Exchange rate was converted from this currency code._ |
| [![Indexes AK_CurrencyRate_CurrencyRateDate_FromCurrencyCode_ToCurrencyCode](../../../../Images/Index.png)](#indexes)[![Foreign Keys FK_CurrencyRate_Currency_ToCurrencyCode: [Sales].[Currency].ToCurrencyCode](../../../../Images/fk.png)](#foreignkeys) | ToCurrencyCode | nchar(3) | 6 | NO |  |  | _Exchange rate was converted to this currency code._ |
|  | AverageRate | money | 8 | NO |  |  | _Average exchange rate for the day._ |
|  | EndOfDayRate | money | 8 | NO |  |  | _Final exchange rate for the day._ |
|  | ModifiedDate | datetime | 8 | NO |  | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_CurrencyRate_CurrencyRateID: CurrencyRateID](../../../../Images/pkcluster.png)](#indexes) | PK_CurrencyRate_CurrencyRateID | CurrencyRateID | YES | _Primary key (clustered) constraint_ |
|  | AK_CurrencyRate_CurrencyRateDate_FromCurrencyCode_ToCurrencyCode | CurrencyRateDate, FromCurrencyCode, ToCurrencyCode | YES | _Unique nonclustered index._ |


---

## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_CurrencyRate_Currency_FromCurrencyCode | FromCurrencyCode->[[Sales].[Currency].[CurrencyCode]](Currency.md) | _Foreign key constraint referencing Currency.FromCurrencyCode._ |
| FK_CurrencyRate_Currency_ToCurrencyCode | ToCurrencyCode->[[Sales].[Currency].[CurrencyCode]](Currency.md) | _Foreign key constraint referencing Currency.ToCurrencyCode._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Sales].[CurrencyRate]
(
[CurrencyRateID] [int] NOT NULL IDENTITY(1, 1),
[CurrencyRateDate] [datetime] NOT NULL,
[FromCurrencyCode] [nchar] (3) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[ToCurrencyCode] [nchar] (3) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[AverageRate] [money] NOT NULL,
[EndOfDayRate] [money] NOT NULL,
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_CurrencyRate_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Sales].[CurrencyRate] ADD CONSTRAINT [PK_CurrencyRate_CurrencyRateID] PRIMARY KEY CLUSTERED  ([CurrencyRateID]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_CurrencyRate_CurrencyRateDate_FromCurrencyCode_ToCurrencyCode] ON [Sales].[CurrencyRate] ([CurrencyRateDate], [FromCurrencyCode], [ToCurrencyCode]) ON [PRIMARY]
GO
ALTER TABLE [Sales].[CurrencyRate] ADD CONSTRAINT [FK_CurrencyRate_Currency_FromCurrencyCode] FOREIGN KEY ([FromCurrencyCode]) REFERENCES [Sales].[Currency] ([CurrencyCode])
GO
ALTER TABLE [Sales].[CurrencyRate] ADD CONSTRAINT [FK_CurrencyRate_Currency_ToCurrencyCode] FOREIGN KEY ([ToCurrencyCode]) REFERENCES [Sales].[Currency] ([CurrencyCode])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Currency exchange rates.', 'SCHEMA', N'Sales', 'TABLE', N'CurrencyRate', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Average exchange rate for the day.', 'SCHEMA', N'Sales', 'TABLE', N'CurrencyRate', 'COLUMN', N'AverageRate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the exchange rate was obtained.', 'SCHEMA', N'Sales', 'TABLE', N'CurrencyRate', 'COLUMN', N'CurrencyRateDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key for CurrencyRate records.', 'SCHEMA', N'Sales', 'TABLE', N'CurrencyRate', 'COLUMN', N'CurrencyRateID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Final exchange rate for the day.', 'SCHEMA', N'Sales', 'TABLE', N'CurrencyRate', 'COLUMN', N'EndOfDayRate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Exchange rate was converted from this currency code.', 'SCHEMA', N'Sales', 'TABLE', N'CurrencyRate', 'COLUMN', N'FromCurrencyCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Sales', 'TABLE', N'CurrencyRate', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Exchange rate was converted to this currency code.', 'SCHEMA', N'Sales', 'TABLE', N'CurrencyRate', 'COLUMN', N'ToCurrencyCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Sales', 'TABLE', N'CurrencyRate', 'CONSTRAINT', N'DF_CurrencyRate_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Currency.FromCurrencyCode.', 'SCHEMA', N'Sales', 'TABLE', N'CurrencyRate', 'CONSTRAINT', N'FK_CurrencyRate_Currency_FromCurrencyCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Currency.ToCurrencyCode.', 'SCHEMA', N'Sales', 'TABLE', N'CurrencyRate', 'CONSTRAINT', N'FK_CurrencyRate_Currency_ToCurrencyCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Sales', 'TABLE', N'CurrencyRate', 'CONSTRAINT', N'PK_CurrencyRate_CurrencyRateID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index.', 'SCHEMA', N'Sales', 'TABLE', N'CurrencyRate', 'INDEX', N'AK_CurrencyRate_CurrencyRateDate_FromCurrencyCode_ToCurrencyCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Sales', 'TABLE', N'CurrencyRate', 'INDEX', N'PK_CurrencyRate_CurrencyRateID'
GO

```


---

## <a name="#uses"></a>Uses

* [[Sales].[Currency]](Currency.md)
* [Sales](../Security/Schemas/Sales.md)


---

## <a name="#usedby"></a>Used By

* [[Sales].[SalesOrderHeader]](SalesOrderHeader.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 12:25

