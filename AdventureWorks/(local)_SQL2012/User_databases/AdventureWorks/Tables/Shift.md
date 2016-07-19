
# ![Tables](../../../../Images/Table32.png) [HumanResources].[Shift]

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables_.md) > HumanResources.Shift

## <a name="#description"></a>MS_Description
Work shift lookup table.
## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 3 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:54 14 March 2012 |


## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Identity | Default | Description |
|---|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_Shift_ShiftID: ShiftID](../../../../Images/pkcluster.png)](#indexes) | ShiftID | tinyint | 1 | NO | 1 - 1 |  | _Primary key for Shift records._ |
| [![Indexes AK_Shift_Name](../../../../Images/Index.png)](#indexes) | Name | [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md) | 100 | NO |  |  | _Shift description._ |
| [![Indexes AK_Shift_StartTime_EndTime](../../../../Images/Index.png)](#indexes) | StartTime | time | 5 | NO |  |  | _Shift start time._ |
| [![Indexes AK_Shift_StartTime_EndTime](../../../../Images/Index.png)](#indexes) | EndTime | time | 5 | NO |  |  | _Shift end time._ |
|  | ModifiedDate | datetime | 8 | NO |  | (getdate()) | _Date and time the record was last updated._ |


## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_Shift_ShiftID: ShiftID](../../../../Images/pkcluster.png)](#indexes) | PK_Shift_ShiftID | ShiftID | YES | _Primary key (clustered) constraint_ |
|  | AK_Shift_Name | Name | YES | _Unique nonclustered index._ |
|  | AK_Shift_StartTime_EndTime | StartTime, EndTime | YES | _Unique nonclustered index._ |


## <a name="#sqlscript"></a>SQL Script
```sql
CREATE TABLE [HumanResources].[Shift]
(
[ShiftID] [tinyint] NOT NULL IDENTITY(1, 1),
[Name] [dbo].[Name] NOT NULL,
[StartTime] [time] NOT NULL,
[EndTime] [time] NOT NULL,
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_Shift_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [HumanResources].[Shift] ADD CONSTRAINT [PK_Shift_ShiftID] PRIMARY KEY CLUSTERED  ([ShiftID]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_Shift_Name] ON [HumanResources].[Shift] ([Name]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_Shift_StartTime_EndTime] ON [HumanResources].[Shift] ([StartTime], [EndTime]) ON [PRIMARY]
GO
EXEC sp_addextendedproperty N'MS_Description', N'Work shift lookup table.', 'SCHEMA', N'HumanResources', 'TABLE', N'Shift', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Shift end time.', 'SCHEMA', N'HumanResources', 'TABLE', N'Shift', 'COLUMN', N'EndTime'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'HumanResources', 'TABLE', N'Shift', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Shift description.', 'SCHEMA', N'HumanResources', 'TABLE', N'Shift', 'COLUMN', N'Name'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key for Shift records.', 'SCHEMA', N'HumanResources', 'TABLE', N'Shift', 'COLUMN', N'ShiftID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Shift start time.', 'SCHEMA', N'HumanResources', 'TABLE', N'Shift', 'COLUMN', N'StartTime'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'HumanResources', 'TABLE', N'Shift', 'CONSTRAINT', N'DF_Shift_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'HumanResources', 'TABLE', N'Shift', 'CONSTRAINT', N'PK_Shift_ShiftID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index.', 'SCHEMA', N'HumanResources', 'TABLE', N'Shift', 'INDEX', N'AK_Shift_Name'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index.', 'SCHEMA', N'HumanResources', 'TABLE', N'Shift', 'INDEX', N'AK_Shift_StartTime_EndTime'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'HumanResources', 'TABLE', N'Shift', 'INDEX', N'PK_Shift_ShiftID'
GO

```

## <a name="#uses"></a>Uses
DEPENDENCYLIST
* [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md)
* [HumanResources](../Security/Schemas/HumanResources.md)


## <a name="#usedby"></a>Used By
DEPENDENCYLIST
* [[HumanResources].[EmployeeDepartmentHistory]](EmployeeDepartmentHistory.md)
* [[HumanResources].[vEmployeeDepartmentHistory]](../Views/vEmployeeDepartmentHistory.md)

FOOTER: FOOTER: Author:  Chris Whitworth
FOOTER: Created: 19 July 2016 09:34
FOOTER: Copyright 2016 - All Rights Reserved

