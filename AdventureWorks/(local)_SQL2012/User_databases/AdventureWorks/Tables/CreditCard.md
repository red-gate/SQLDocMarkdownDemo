
# ![Tables](../../../../Images/Table32.png) [Sales].[CreditCard]

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables_.md) > Sales.CreditCard

## <a name="#description"></a>MS_Description
Customer credit card information.
## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 19118 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:54 14 March 2012 |


## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Identity | Default | Description |
|---|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_CreditCard_CreditCardID: CreditCardID](../../../../Images/pkcluster.png)](#indexes) | CreditCardID | int | 4 | NO | 1 - 1 |  | _Primary key for CreditCard records._ |
|  | CardType | nvarchar(50) | 100 | NO |  |  | _Credit card name._ |
| [![Indexes AK_CreditCard_CardNumber](../../../../Images/Index.png)](#indexes) | CardNumber | nvarchar(25) | 50 | NO |  |  | _Credit card number._ |
|  | ExpMonth | tinyint | 1 | NO |  |  | _Credit card expiration month._ |
|  | ExpYear | smallint | 2 | NO |  |  | _Credit card expiration year._ |
|  | ModifiedDate | datetime | 8 | NO |  | (getdate()) | _Date and time the record was last updated._ |


## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_CreditCard_CreditCardID: CreditCardID](../../../../Images/pkcluster.png)](#indexes) | PK_CreditCard_CreditCardID | CreditCardID | YES | _Primary key (clustered) constraint_ |
|  | AK_CreditCard_CardNumber | CardNumber | YES | _Unique nonclustered index._ |


## <a name="#sqlscript"></a>SQL Script
```sql
CREATE TABLE [Sales].[CreditCard]
(
[CreditCardID] [int] NOT NULL IDENTITY(1, 1),
[CardType] [nvarchar] (50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[CardNumber] [nvarchar] (25) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[ExpMonth] [tinyint] NOT NULL,
[ExpYear] [smallint] NOT NULL,
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_CreditCard_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Sales].[CreditCard] ADD CONSTRAINT [PK_CreditCard_CreditCardID] PRIMARY KEY CLUSTERED  ([CreditCardID]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_CreditCard_CardNumber] ON [Sales].[CreditCard] ([CardNumber]) ON [PRIMARY]
GO
EXEC sp_addextendedproperty N'MS_Description', N'Customer credit card information.', 'SCHEMA', N'Sales', 'TABLE', N'CreditCard', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Credit card number.', 'SCHEMA', N'Sales', 'TABLE', N'CreditCard', 'COLUMN', N'CardNumber'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Credit card name.', 'SCHEMA', N'Sales', 'TABLE', N'CreditCard', 'COLUMN', N'CardType'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key for CreditCard records.', 'SCHEMA', N'Sales', 'TABLE', N'CreditCard', 'COLUMN', N'CreditCardID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Credit card expiration month.', 'SCHEMA', N'Sales', 'TABLE', N'CreditCard', 'COLUMN', N'ExpMonth'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Credit card expiration year.', 'SCHEMA', N'Sales', 'TABLE', N'CreditCard', 'COLUMN', N'ExpYear'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Sales', 'TABLE', N'CreditCard', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Sales', 'TABLE', N'CreditCard', 'CONSTRAINT', N'DF_CreditCard_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Sales', 'TABLE', N'CreditCard', 'CONSTRAINT', N'PK_CreditCard_CreditCardID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index.', 'SCHEMA', N'Sales', 'TABLE', N'CreditCard', 'INDEX', N'AK_CreditCard_CardNumber'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Sales', 'TABLE', N'CreditCard', 'INDEX', N'PK_CreditCard_CreditCardID'
GO

```

## <a name="#uses"></a>Uses
DEPENDENCYLIST
* [Sales](../Security/Schemas/Sales.md)


## <a name="#usedby"></a>Used By
DEPENDENCYLIST
* [[Sales].[PersonCreditCard]](PersonCreditCard.md)
* [[Sales].[SalesOrderHeader]](SalesOrderHeader.md)

FOOTER: FOOTER: Author:  Chris Whitworth
FOOTER: Created: 19 July 2016 09:34
FOOTER: Copyright 2016 - All Rights Reserved

