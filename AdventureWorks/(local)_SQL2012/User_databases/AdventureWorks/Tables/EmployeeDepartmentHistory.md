
# ![Tables](../../../../Images/Table32.png) [HumanResources].[EmployeeDepartmentHistory]

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables_.md) > HumanResources.EmployeeDepartmentHistory

## <a name="#description"></a>MS_Description
Employee department transfers.
## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Row Count (~) | 296 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:54 14 March 2012 |


## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Default | Description |
|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_EmployeeDepartmentHistory_BusinessEntityID_StartDate_DepartmentID: BusinessEntityID\\StartDate\\DepartmentID\\ShiftID](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_EmployeeDepartmentHistory_Employee_BusinessEntityID: [HumanResources].[Employee].BusinessEntityID](../../../../Images/fk.png)](#foreignkeys) | BusinessEntityID | int | 4 | NO |  | _Employee identification number. Foreign key to Employee.BusinessEntityID._ |
| [![Cluster Primary Key PK_EmployeeDepartmentHistory_BusinessEntityID_StartDate_DepartmentID: BusinessEntityID\\StartDate\\DepartmentID\\ShiftID](../../../../Images/pkcluster.png)](#indexes)[![Indexes IX_EmployeeDepartmentHistory_DepartmentID](../../../../Images/Index.png)](#indexes)[![Foreign Keys FK_EmployeeDepartmentHistory_Department_DepartmentID: [HumanResources].[Department].DepartmentID](../../../../Images/fk.png)](#foreignkeys) | DepartmentID | smallint | 2 | NO |  | _Department in which the employee worked including currently. Foreign key to Department.DepartmentID._ |
| [![Cluster Primary Key PK_EmployeeDepartmentHistory_BusinessEntityID_StartDate_DepartmentID: BusinessEntityID\\StartDate\\DepartmentID\\ShiftID](../../../../Images/pkcluster.png)](#indexes)[![Indexes IX_EmployeeDepartmentHistory_ShiftID](../../../../Images/Index.png)](#indexes)[![Foreign Keys FK_EmployeeDepartmentHistory_Shift_ShiftID: [HumanResources].[Shift].ShiftID](../../../../Images/fk.png)](#foreignkeys) | ShiftID | tinyint | 1 | NO |  | _Identifies which 8-hour shift the employee works. Foreign key to Shift.Shift.ID._ |
| [![Cluster Primary Key PK_EmployeeDepartmentHistory_BusinessEntityID_StartDate_DepartmentID: BusinessEntityID\\StartDate\\DepartmentID\\ShiftID](../../../../Images/pkcluster.png)](#indexes) | StartDate | date | 3 | NO |  | _Date the employee started work in the department._ |
|  | EndDate | date | 3 | YES |  | _Date the employee left the department. NULL = Current department._ |
|  | ModifiedDate | datetime | 8 | NO | (getdate()) | _Date and time the record was last updated._ |


## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_EmployeeDepartmentHistory_BusinessEntityID_StartDate_DepartmentID: BusinessEntityID\\StartDate\\DepartmentID\\ShiftID](../../../../Images/pkcluster.png)](#indexes) | PK_EmployeeDepartmentHistory_BusinessEntityID_StartDate_DepartmentID | BusinessEntityID, StartDate, DepartmentID, ShiftID | YES | _Primary key (clustered) constraint_ |
|  | IX_EmployeeDepartmentHistory_DepartmentID | DepartmentID |  | _Nonclustered index._ |
|  | IX_EmployeeDepartmentHistory_ShiftID | ShiftID |  | _Nonclustered index._ |


## <a name="#checkconstraints"></a>Check Constraints

| Name | Constraint | Description |
|---|---|---|
| CK_EmployeeDepartmentHistory_EndDate | ([EndDate]>=[StartDate] OR [EndDate] IS NULL) | _Check constraint [EndDate] >= [StartDate] OR [EndDate] IS NUL_ |


## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_EmployeeDepartmentHistory_Department_DepartmentID | DepartmentID->[[HumanResources].[Department].[DepartmentID]](Department.md) | _Foreign key constraint referencing Department.DepartmentID._ |
| FK_EmployeeDepartmentHistory_Employee_BusinessEntityID | BusinessEntityID->[[HumanResources].[Employee].[BusinessEntityID]](Employee.md) | _Foreign key constraint referencing Employee.EmployeeID._ |
| FK_EmployeeDepartmentHistory_Shift_ShiftID | ShiftID->[[HumanResources].[Shift].[ShiftID]](Shift.md) | _Foreign key constraint referencing Shift.ShiftID_ |


## <a name="#sqlscript"></a>SQL Script
```sql
CREATE TABLE [HumanResources].[EmployeeDepartmentHistory]
(
[BusinessEntityID] [int] NOT NULL,
[DepartmentID] [smallint] NOT NULL,
[ShiftID] [tinyint] NOT NULL,
[StartDate] [date] NOT NULL,
[EndDate] [date] NULL,
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_EmployeeDepartmentHistory_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [HumanResources].[EmployeeDepartmentHistory] ADD CONSTRAINT [CK_EmployeeDepartmentHistory_EndDate] CHECK (([EndDate]>=[StartDate] OR [EndDate] IS NULL))
GO
ALTER TABLE [HumanResources].[EmployeeDepartmentHistory] ADD CONSTRAINT [PK_EmployeeDepartmentHistory_BusinessEntityID_StartDate_DepartmentID] PRIMARY KEY CLUSTERED  ([BusinessEntityID], [StartDate], [DepartmentID], [ShiftID]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_EmployeeDepartmentHistory_DepartmentID] ON [HumanResources].[EmployeeDepartmentHistory] ([DepartmentID]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_EmployeeDepartmentHistory_ShiftID] ON [HumanResources].[EmployeeDepartmentHistory] ([ShiftID]) ON [PRIMARY]
GO
ALTER TABLE [HumanResources].[EmployeeDepartmentHistory] ADD CONSTRAINT [FK_EmployeeDepartmentHistory_Department_DepartmentID] FOREIGN KEY ([DepartmentID]) REFERENCES [HumanResources].[Department] ([DepartmentID])
GO
ALTER TABLE [HumanResources].[EmployeeDepartmentHistory] ADD CONSTRAINT [FK_EmployeeDepartmentHistory_Employee_BusinessEntityID] FOREIGN KEY ([BusinessEntityID]) REFERENCES [HumanResources].[Employee] ([BusinessEntityID])
GO
ALTER TABLE [HumanResources].[EmployeeDepartmentHistory] ADD CONSTRAINT [FK_EmployeeDepartmentHistory_Shift_ShiftID] FOREIGN KEY ([ShiftID]) REFERENCES [HumanResources].[Shift] ([ShiftID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Employee department transfers.', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeeDepartmentHistory', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Employee identification number. Foreign key to Employee.BusinessEntityID.', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeeDepartmentHistory', 'COLUMN', N'BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Department in which the employee worked including currently. Foreign key to Department.DepartmentID.', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeeDepartmentHistory', 'COLUMN', N'DepartmentID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date the employee left the department. NULL = Current department.', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeeDepartmentHistory', 'COLUMN', N'EndDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeeDepartmentHistory', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Identifies which 8-hour shift the employee works. Foreign key to Shift.Shift.ID.', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeeDepartmentHistory', 'COLUMN', N'ShiftID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date the employee started work in the department.', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeeDepartmentHistory', 'COLUMN', N'StartDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [EndDate] >= [StartDate] OR [EndDate] IS NUL', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeeDepartmentHistory', 'CONSTRAINT', N'CK_EmployeeDepartmentHistory_EndDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeeDepartmentHistory', 'CONSTRAINT', N'DF_EmployeeDepartmentHistory_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Department.DepartmentID.', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeeDepartmentHistory', 'CONSTRAINT', N'FK_EmployeeDepartmentHistory_Department_DepartmentID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Employee.EmployeeID.', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeeDepartmentHistory', 'CONSTRAINT', N'FK_EmployeeDepartmentHistory_Employee_BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Shift.ShiftID', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeeDepartmentHistory', 'CONSTRAINT', N'FK_EmployeeDepartmentHistory_Shift_ShiftID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeeDepartmentHistory', 'CONSTRAINT', N'PK_EmployeeDepartmentHistory_BusinessEntityID_StartDate_DepartmentID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Nonclustered index.', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeeDepartmentHistory', 'INDEX', N'IX_EmployeeDepartmentHistory_DepartmentID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Nonclustered index.', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeeDepartmentHistory', 'INDEX', N'IX_EmployeeDepartmentHistory_ShiftID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeeDepartmentHistory', 'INDEX', N'PK_EmployeeDepartmentHistory_BusinessEntityID_StartDate_DepartmentID'
GO

```

## <a name="#uses"></a>Uses
DEPENDENCYLIST
* [[HumanResources].[Department]](Department.md)
* [[HumanResources].[Employee]](Employee.md)
* [[HumanResources].[Shift]](Shift.md)
* [HumanResources](../Security/Schemas/HumanResources.md)


## <a name="#usedby"></a>Used By
DEPENDENCYLIST
* [[HumanResources].[vEmployeeDepartment]](../Views/vEmployeeDepartment.md)
* [[HumanResources].[vEmployeeDepartmentHistory]](../Views/vEmployeeDepartmentHistory.md)

FOOTER: FOOTER: Author:  Chris Whitworth
FOOTER: Created: 19 July 2016 09:34
FOOTER: Copyright 2016 - All Rights Reserved

