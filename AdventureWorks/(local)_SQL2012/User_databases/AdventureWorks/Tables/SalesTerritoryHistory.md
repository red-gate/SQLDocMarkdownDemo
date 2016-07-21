#### asdasdasd

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Sales.SalesTerritoryHistory

# ![Tables](../../../../Images/Table32.png) [Sales].[SalesTerritoryHistory]

---

## <a name="#description"></a>MS_Description

Sales representative transfers to other sales territories.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Row Count (~) | 17 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:55 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Default | Description |
|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_SalesTerritoryHistory_BusinessEntityID_StartDate_TerritoryID: BusinessEntityID\StartDate\TerritoryID](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_SalesTerritoryHistory_SalesPerson_BusinessEntityID: [Sales].[SalesPerson].BusinessEntityID](../../../../Images/fk.png)](#foreignkeys) | BusinessEntityID | int | 4 | NO |  | _Primary key. The sales rep.  Foreign key to SalesPerson.BusinessEntityID._ |
| [![Cluster Primary Key PK_SalesTerritoryHistory_BusinessEntityID_StartDate_TerritoryID: BusinessEntityID\StartDate\TerritoryID](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_SalesTerritoryHistory_SalesTerritory_TerritoryID: [Sales].[SalesTerritory].TerritoryID](../../../../Images/fk.png)](#foreignkeys) | TerritoryID | int | 4 | NO |  | _Primary key. Territory identification number. Foreign key to SalesTerritory.SalesTerritoryID._ |
| [![Cluster Primary Key PK_SalesTerritoryHistory_BusinessEntityID_StartDate_TerritoryID: BusinessEntityID\StartDate\TerritoryID](../../../../Images/pkcluster.png)](#indexes) | StartDate | datetime | 8 | NO |  | _Primary key. Date the sales representive started work in the territory._ |
|  | EndDate | datetime | 8 | YES |  | _Date the sales representative left work in the territory._ |
| [![Indexes AK_SalesTerritoryHistory_rowguid](../../../../Images/Index.png)](#indexes) | rowguid | uniqueidentifier | 16 | NO | (newid()) | _ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample._ |
|  | ModifiedDate | datetime | 8 | NO | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_SalesTerritoryHistory_BusinessEntityID_StartDate_TerritoryID: BusinessEntityID\StartDate\TerritoryID](../../../../Images/pkcluster.png)](#indexes) | PK_SalesTerritoryHistory_BusinessEntityID_StartDate_TerritoryID | BusinessEntityID, StartDate, TerritoryID | YES | _Primary key (clustered) constraint_ |
|  | AK_SalesTerritoryHistory_rowguid | rowguid | YES | _Unique nonclustered index. Used to support replication samples._ |


---

## <a name="#checkconstraints"></a>Check Constraints

| Name | Constraint | Description |
|---|---|---|
| CK_SalesTerritoryHistory_EndDate | ([EndDate]>=[StartDate] OR [EndDate] IS NULL) | _Check constraint [EndDate] >= [StartDate] OR [EndDate] IS NULL_ |


---

## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_SalesTerritoryHistory_SalesPerson_BusinessEntityID | BusinessEntityID->[[Sales].[SalesPerson].[BusinessEntityID]](SalesPerson.md) | _Foreign key constraint referencing SalesPerson.SalesPersonID._ |
| FK_SalesTerritoryHistory_SalesTerritory_TerritoryID | TerritoryID->[[Sales].[SalesTerritory].[TerritoryID]](SalesTerritory.md) | _Foreign key constraint referencing SalesTerritory.TerritoryID._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Sales].[SalesTerritoryHistory]
(
[BusinessEntityID] [int] NOT NULL,
[TerritoryID] [int] NOT NULL,
[StartDate] [datetime] NOT NULL,
[EndDate] [datetime] NULL,
[rowguid] [uniqueidentifier] NOT NULL ROWGUIDCOL CONSTRAINT [DF_SalesTerritoryHistory_rowguid] DEFAULT (newid()),
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_SalesTerritoryHistory_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Sales].[SalesTerritoryHistory] ADD CONSTRAINT [CK_SalesTerritoryHistory_EndDate] CHECK (([EndDate]>=[StartDate] OR [EndDate] IS NULL))
GO
ALTER TABLE [Sales].[SalesTerritoryHistory] ADD CONSTRAINT [PK_SalesTerritoryHistory_BusinessEntityID_StartDate_TerritoryID] PRIMARY KEY CLUSTERED  ([BusinessEntityID], [StartDate], [TerritoryID]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_SalesTerritoryHistory_rowguid] ON [Sales].[SalesTerritoryHistory] ([rowguid]) ON [PRIMARY]
GO
ALTER TABLE [Sales].[SalesTerritoryHistory] ADD CONSTRAINT [FK_SalesTerritoryHistory_SalesPerson_BusinessEntityID] FOREIGN KEY ([BusinessEntityID]) REFERENCES [Sales].[SalesPerson] ([BusinessEntityID])
GO
ALTER TABLE [Sales].[SalesTerritoryHistory] ADD CONSTRAINT [FK_SalesTerritoryHistory_SalesTerritory_TerritoryID] FOREIGN KEY ([TerritoryID]) REFERENCES [Sales].[SalesTerritory] ([TerritoryID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Sales representative transfers to other sales territories.', 'SCHEMA', N'Sales', 'TABLE', N'SalesTerritoryHistory', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key. The sales rep.  Foreign key to SalesPerson.BusinessEntityID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesTerritoryHistory', 'COLUMN', N'BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date the sales representative left work in the territory.', 'SCHEMA', N'Sales', 'TABLE', N'SalesTerritoryHistory', 'COLUMN', N'EndDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Sales', 'TABLE', N'SalesTerritoryHistory', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample.', 'SCHEMA', N'Sales', 'TABLE', N'SalesTerritoryHistory', 'COLUMN', N'rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key. Date the sales representive started work in the territory.', 'SCHEMA', N'Sales', 'TABLE', N'SalesTerritoryHistory', 'COLUMN', N'StartDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key. Territory identification number. Foreign key to SalesTerritory.SalesTerritoryID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesTerritoryHistory', 'COLUMN', N'TerritoryID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [EndDate] >= [StartDate] OR [EndDate] IS NULL', 'SCHEMA', N'Sales', 'TABLE', N'SalesTerritoryHistory', 'CONSTRAINT', N'CK_SalesTerritoryHistory_EndDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Sales', 'TABLE', N'SalesTerritoryHistory', 'CONSTRAINT', N'DF_SalesTerritoryHistory_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of NEWID()', 'SCHEMA', N'Sales', 'TABLE', N'SalesTerritoryHistory', 'CONSTRAINT', N'DF_SalesTerritoryHistory_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing SalesPerson.SalesPersonID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesTerritoryHistory', 'CONSTRAINT', N'FK_SalesTerritoryHistory_SalesPerson_BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing SalesTerritory.TerritoryID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesTerritoryHistory', 'CONSTRAINT', N'FK_SalesTerritoryHistory_SalesTerritory_TerritoryID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Sales', 'TABLE', N'SalesTerritoryHistory', 'CONSTRAINT', N'PK_SalesTerritoryHistory_BusinessEntityID_StartDate_TerritoryID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index. Used to support replication samples.', 'SCHEMA', N'Sales', 'TABLE', N'SalesTerritoryHistory', 'INDEX', N'AK_SalesTerritoryHistory_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Sales', 'TABLE', N'SalesTerritoryHistory', 'INDEX', N'PK_SalesTerritoryHistory_BusinessEntityID_StartDate_TerritoryID'
GO

```


---

## <a name="#uses"></a>Uses

* [[Sales].[SalesPerson]](SalesPerson.md)
* [[Sales].[SalesTerritory]](SalesTerritory.md)
* [Sales](../Security/Schemas/Sales.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 12:25

