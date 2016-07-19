
# ![Tables](../../../../Images/Table32.png) [Sales].[SalesOrderHeaderSalesReason]

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables_.md) > Sales.SalesOrderHeaderSalesReason

## <a name="#description"></a>MS_Description
Cross-reference table mapping sales orders to sales reason codes.
## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Row Count (~) | 27647 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:55 14 March 2012 |


## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Default | Description |
|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_SalesOrderHeaderSalesReason_SalesOrderID_SalesReasonID: SalesOrderID\\SalesReasonID](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_SalesOrderHeaderSalesReason_SalesOrderHeader_SalesOrderID: [Sales].[SalesOrderHeader].SalesOrderID](../../../../Images/fk.png)](#foreignkeys) | SalesOrderID | int | 4 | NO |  | _Primary key. Foreign key to SalesOrderHeader.SalesOrderID._ |
| [![Cluster Primary Key PK_SalesOrderHeaderSalesReason_SalesOrderID_SalesReasonID: SalesOrderID\\SalesReasonID](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_SalesOrderHeaderSalesReason_SalesReason_SalesReasonID: [Sales].[SalesReason].SalesReasonID](../../../../Images/fk.png)](#foreignkeys) | SalesReasonID | int | 4 | NO |  | _Primary key. Foreign key to SalesReason.SalesReasonID._ |
|  | ModifiedDate | datetime | 8 | NO | (getdate()) | _Date and time the record was last updated._ |


## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_SalesOrderHeaderSalesReason_SalesOrderID_SalesReasonID: SalesOrderID\\SalesReasonID](../../../../Images/pkcluster.png)](#indexes) | PK_SalesOrderHeaderSalesReason_SalesOrderID_SalesReasonID | SalesOrderID, SalesReasonID | YES | _Primary key (clustered) constraint_ |


## <a name="#foreignkeys"></a>Foreign Keys

| Name | Delete | Columns | Description |
|---|---|---|---|
| FK_SalesOrderHeaderSalesReason_SalesOrderHeader_SalesOrderID | Cascade | SalesOrderID->[[Sales].[SalesOrderHeader].[SalesOrderID]](SalesOrderHeader.md) | _Foreign key constraint referencing SalesOrderHeader.SalesOrderID._ |
| FK_SalesOrderHeaderSalesReason_SalesReason_SalesReasonID |  | SalesReasonID->[[Sales].[SalesReason].[SalesReasonID]](SalesReason.md) | _Foreign key constraint referencing SalesReason.SalesReasonID._ |


## <a name="#sqlscript"></a>SQL Script
```sql
CREATE TABLE [Sales].[SalesOrderHeaderSalesReason]
(
[SalesOrderID] [int] NOT NULL,
[SalesReasonID] [int] NOT NULL,
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_SalesOrderHeaderSalesReason_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Sales].[SalesOrderHeaderSalesReason] ADD CONSTRAINT [PK_SalesOrderHeaderSalesReason_SalesOrderID_SalesReasonID] PRIMARY KEY CLUSTERED  ([SalesOrderID], [SalesReasonID]) ON [PRIMARY]
GO
ALTER TABLE [Sales].[SalesOrderHeaderSalesReason] ADD CONSTRAINT [FK_SalesOrderHeaderSalesReason_SalesOrderHeader_SalesOrderID] FOREIGN KEY ([SalesOrderID]) REFERENCES [Sales].[SalesOrderHeader] ([SalesOrderID]) ON DELETE CASCADE
GO
ALTER TABLE [Sales].[SalesOrderHeaderSalesReason] ADD CONSTRAINT [FK_SalesOrderHeaderSalesReason_SalesReason_SalesReasonID] FOREIGN KEY ([SalesReasonID]) REFERENCES [Sales].[SalesReason] ([SalesReasonID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Cross-reference table mapping sales orders to sales reason codes.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeaderSalesReason', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeaderSalesReason', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key. Foreign key to SalesOrderHeader.SalesOrderID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeaderSalesReason', 'COLUMN', N'SalesOrderID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key. Foreign key to SalesReason.SalesReasonID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeaderSalesReason', 'COLUMN', N'SalesReasonID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeaderSalesReason', 'CONSTRAINT', N'DF_SalesOrderHeaderSalesReason_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing SalesOrderHeader.SalesOrderID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeaderSalesReason', 'CONSTRAINT', N'FK_SalesOrderHeaderSalesReason_SalesOrderHeader_SalesOrderID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing SalesReason.SalesReasonID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeaderSalesReason', 'CONSTRAINT', N'FK_SalesOrderHeaderSalesReason_SalesReason_SalesReasonID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeaderSalesReason', 'CONSTRAINT', N'PK_SalesOrderHeaderSalesReason_SalesOrderID_SalesReasonID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeaderSalesReason', 'INDEX', N'PK_SalesOrderHeaderSalesReason_SalesOrderID_SalesReasonID'
GO

```

## <a name="#uses"></a>Uses
DEPENDENCYLIST
* [[Sales].[SalesOrderHeader]](SalesOrderHeader.md)
* [[Sales].[SalesReason]](SalesReason.md)
* [Sales](../Security/Schemas/Sales.md)

FOOTER: FOOTER: Author:  Chris Whitworth
FOOTER: Created: 19 July 2016 09:34
FOOTER: Copyright 2016 - All Rights Reserved

