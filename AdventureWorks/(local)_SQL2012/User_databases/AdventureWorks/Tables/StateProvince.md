#### asdasdasd

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Person.StateProvince

# ![Tables](../../../../Images/Table32.png) [Person].[StateProvince]

---

## <a name="#description"></a>MS_Description

State and province lookup table.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 181 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:55 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Identity | Default | Description |
|---|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_StateProvince_StateProvinceID: StateProvinceID](../../../../Images/pkcluster.png)](#indexes) | StateProvinceID | int | 4 | NO | 1 - 1 |  | _Primary key for StateProvince records._ |
| [![Indexes AK_StateProvince_StateProvinceCode_CountryRegionCode](../../../../Images/Index.png)](#indexes) | StateProvinceCode | nchar(3) | 6 | NO |  |  | _ISO standard state or province code._ |
| [![Indexes AK_StateProvince_StateProvinceCode_CountryRegionCode](../../../../Images/Index.png)](#indexes)[![Foreign Keys FK_StateProvince_CountryRegion_CountryRegionCode: [Person].[CountryRegion].CountryRegionCode](../../../../Images/fk.png)](#foreignkeys) | CountryRegionCode | nvarchar(3) | 6 | NO |  |  | _ISO standard country or region code. Foreign key to CountryRegion.CountryRegionCode. _ |
|  | IsOnlyStateProvinceFlag | [[dbo].[Flag]](../Programmability/Types/User-Defined_Data_Types/Flag.md) | 1 | NO |  | ((1)) | _0 = StateProvinceCode exists. 1 = StateProvinceCode unavailable, using CountryRegionCode._ |
| [![Indexes AK_StateProvince_Name](../../../../Images/Index.png)](#indexes) | Name | [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md) | 100 | NO |  |  | _State or province description._ |
| [![Foreign Keys FK_StateProvince_SalesTerritory_TerritoryID: [Sales].[SalesTerritory].TerritoryID](../../../../Images/fk.png)](#foreignkeys) | TerritoryID | int | 4 | NO |  |  | _ID of the territory in which the state or province is located. Foreign key to SalesTerritory.SalesTerritoryID._ |
| [![Indexes AK_StateProvince_rowguid](../../../../Images/Index.png)](#indexes) | rowguid | uniqueidentifier | 16 | NO |  | (newid()) | _ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample._ |
|  | ModifiedDate | datetime | 8 | NO |  | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_StateProvince_StateProvinceID: StateProvinceID](../../../../Images/pkcluster.png)](#indexes) | PK_StateProvince_StateProvinceID | StateProvinceID | YES | _Primary key (clustered) constraint_ |
|  | AK_StateProvince_Name | Name | YES | _Unique nonclustered index._ |
|  | AK_StateProvince_StateProvinceCode_CountryRegionCode | StateProvinceCode, CountryRegionCode | YES | _Unique nonclustered index._ |
|  | AK_StateProvince_rowguid | rowguid | YES | _Unique nonclustered index. Used to support replication samples._ |


---

## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_StateProvince_CountryRegion_CountryRegionCode | CountryRegionCode->[[Person].[CountryRegion].[CountryRegionCode]](CountryRegion.md) | _Foreign key constraint referencing CountryRegion.CountryRegionCode._ |
| FK_StateProvince_SalesTerritory_TerritoryID | TerritoryID->[[Sales].[SalesTerritory].[TerritoryID]](SalesTerritory.md) | _Foreign key constraint referencing SalesTerritory.TerritoryID._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Person].[StateProvince]
(
[StateProvinceID] [int] NOT NULL IDENTITY(1, 1),
[StateProvinceCode] [nchar] (3) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[CountryRegionCode] [nvarchar] (3) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[IsOnlyStateProvinceFlag] [dbo].[Flag] NOT NULL CONSTRAINT [DF_StateProvince_IsOnlyStateProvinceFlag] DEFAULT ((1)),
[Name] [dbo].[Name] NOT NULL,
[TerritoryID] [int] NOT NULL,
[rowguid] [uniqueidentifier] NOT NULL ROWGUIDCOL CONSTRAINT [DF_StateProvince_rowguid] DEFAULT (newid()),
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_StateProvince_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Person].[StateProvince] ADD CONSTRAINT [PK_StateProvince_StateProvinceID] PRIMARY KEY CLUSTERED  ([StateProvinceID]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_StateProvince_Name] ON [Person].[StateProvince] ([Name]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_StateProvince_rowguid] ON [Person].[StateProvince] ([rowguid]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_StateProvince_StateProvinceCode_CountryRegionCode] ON [Person].[StateProvince] ([StateProvinceCode], [CountryRegionCode]) ON [PRIMARY]
GO
ALTER TABLE [Person].[StateProvince] ADD CONSTRAINT [FK_StateProvince_CountryRegion_CountryRegionCode] FOREIGN KEY ([CountryRegionCode]) REFERENCES [Person].[CountryRegion] ([CountryRegionCode])
GO
ALTER TABLE [Person].[StateProvince] ADD CONSTRAINT [FK_StateProvince_SalesTerritory_TerritoryID] FOREIGN KEY ([TerritoryID]) REFERENCES [Sales].[SalesTerritory] ([TerritoryID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'State and province lookup table.', 'SCHEMA', N'Person', 'TABLE', N'StateProvince', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'ISO standard country or region code. Foreign key to CountryRegion.CountryRegionCode. ', 'SCHEMA', N'Person', 'TABLE', N'StateProvince', 'COLUMN', N'CountryRegionCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'0 = StateProvinceCode exists. 1 = StateProvinceCode unavailable, using CountryRegionCode.', 'SCHEMA', N'Person', 'TABLE', N'StateProvince', 'COLUMN', N'IsOnlyStateProvinceFlag'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Person', 'TABLE', N'StateProvince', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'State or province description.', 'SCHEMA', N'Person', 'TABLE', N'StateProvince', 'COLUMN', N'Name'
GO
EXEC sp_addextendedproperty N'MS_Description', N'ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample.', 'SCHEMA', N'Person', 'TABLE', N'StateProvince', 'COLUMN', N'rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'ISO standard state or province code.', 'SCHEMA', N'Person', 'TABLE', N'StateProvince', 'COLUMN', N'StateProvinceCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key for StateProvince records.', 'SCHEMA', N'Person', 'TABLE', N'StateProvince', 'COLUMN', N'StateProvinceID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'ID of the territory in which the state or province is located. Foreign key to SalesTerritory.SalesTerritoryID.', 'SCHEMA', N'Person', 'TABLE', N'StateProvince', 'COLUMN', N'TerritoryID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 1 (TRUE)', 'SCHEMA', N'Person', 'TABLE', N'StateProvince', 'CONSTRAINT', N'DF_StateProvince_IsOnlyStateProvinceFlag'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Person', 'TABLE', N'StateProvince', 'CONSTRAINT', N'DF_StateProvince_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of NEWID()', 'SCHEMA', N'Person', 'TABLE', N'StateProvince', 'CONSTRAINT', N'DF_StateProvince_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing CountryRegion.CountryRegionCode.', 'SCHEMA', N'Person', 'TABLE', N'StateProvince', 'CONSTRAINT', N'FK_StateProvince_CountryRegion_CountryRegionCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing SalesTerritory.TerritoryID.', 'SCHEMA', N'Person', 'TABLE', N'StateProvince', 'CONSTRAINT', N'FK_StateProvince_SalesTerritory_TerritoryID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Person', 'TABLE', N'StateProvince', 'CONSTRAINT', N'PK_StateProvince_StateProvinceID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index.', 'SCHEMA', N'Person', 'TABLE', N'StateProvince', 'INDEX', N'AK_StateProvince_Name'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index. Used to support replication samples.', 'SCHEMA', N'Person', 'TABLE', N'StateProvince', 'INDEX', N'AK_StateProvince_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index.', 'SCHEMA', N'Person', 'TABLE', N'StateProvince', 'INDEX', N'AK_StateProvince_StateProvinceCode_CountryRegionCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Person', 'TABLE', N'StateProvince', 'INDEX', N'PK_StateProvince_StateProvinceID'
GO

```


---

## <a name="#uses"></a>Uses

* [[Person].[CountryRegion]](CountryRegion.md)
* [[Sales].[SalesTerritory]](SalesTerritory.md)
* [[dbo].[Flag]](../Programmability/Types/User-Defined_Data_Types/Flag.md)
* [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md)
* [Person](../Security/Schemas/Person.md)


---

## <a name="#usedby"></a>Used By

* [[Person].[Address]](Address.md)
* [[Sales].[SalesTaxRate]](SalesTaxRate.md)
* [[HumanResources].[vEmployee]](../Views/vEmployee.md)
* [[Person].[vStateProvinceCountryRegion]](../Views/vStateProvinceCountryRegion.md)
* [[Purchasing].[vVendorWithAddresses]](../Views/vVendorWithAddresses.md)
* [[Sales].[vIndividualCustomer]](../Views/vIndividualCustomer.md)
* [[Sales].[vSalesPerson]](../Views/vSalesPerson.md)
* [[Sales].[vStoreWithAddresses]](../Views/vStoreWithAddresses.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 12:25

