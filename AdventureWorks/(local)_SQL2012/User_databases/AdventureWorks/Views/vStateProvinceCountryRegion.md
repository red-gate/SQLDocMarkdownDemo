#### asdasdasd

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Views](Views.md) > Person.vStateProvinceCountryRegion

# ![Views](../../../../Images/View32.png) [Person].[vStateProvinceCountryRegion]

---

## <a name="#description"></a>MS_Description

Joins StateProvince table with CountryRegion table.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| ANSI Nulls On | YES |
| Quoted Identifier On | YES |
| Schema Bound | YES |
| Created | 13:14:55 14 March 2012 |
| Last Modified | 13:14:55 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name |
|---|---|
| [![Cluster Key IX_vStateProvinceCountryRegion: StateProvinceID\CountryRegionCode](../../../../Images/cluster.png)](#indexes) | StateProvinceID |
|  | StateProvinceCode |
|  | IsOnlyStateProvinceFlag |
|  | StateProvinceName |
|  | TerritoryID |
| [![Cluster Key IX_vStateProvinceCountryRegion: StateProvinceID\CountryRegionCode](../../../../Images/cluster.png)](#indexes) | CountryRegionCode |
|  | CountryRegionName |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Key IX_vStateProvinceCountryRegion: StateProvinceID\CountryRegionCode](../../../../Images/cluster.png)](#indexes) | IX_vStateProvinceCountryRegion | StateProvinceID, CountryRegionCode | YES | _Clustered index on the view vStateProvinceCountryRegion._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql

CREATE VIEW [Person].[vStateProvinceCountryRegion] 
WITH SCHEMABINDING 
AS 
SELECT 
    sp.[StateProvinceID] 
    ,sp.[StateProvinceCode] 
    ,sp.[IsOnlyStateProvinceFlag] 
    ,sp.[Name] AS [StateProvinceName] 
    ,sp.[TerritoryID] 
    ,cr.[CountryRegionCode] 
    ,cr.[Name] AS [CountryRegionName]
FROM [Person].[StateProvince] sp 
    INNER JOIN [Person].[CountryRegion] cr 
    ON sp.[CountryRegionCode] = cr.[CountryRegionCode];
GO
CREATE UNIQUE CLUSTERED INDEX [IX_vStateProvinceCountryRegion] ON [Person].[vStateProvinceCountryRegion] ([StateProvinceID], [CountryRegionCode]) ON [PRIMARY]
GO
EXEC sp_addextendedproperty N'MS_Description', N'Joins StateProvince table with CountryRegion table.', 'SCHEMA', N'Person', 'VIEW', N'vStateProvinceCountryRegion', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index on the view vStateProvinceCountryRegion.', 'SCHEMA', N'Person', 'VIEW', N'vStateProvinceCountryRegion', 'INDEX', N'IX_vStateProvinceCountryRegion'
GO

```


---

## <a name="#uses"></a>Uses

* [[Person].[CountryRegion]](../Tables/CountryRegion.md)
* [[Person].[StateProvince]](../Tables/StateProvince.md)
* [Person](../Security/Schemas/Person.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 12:25

