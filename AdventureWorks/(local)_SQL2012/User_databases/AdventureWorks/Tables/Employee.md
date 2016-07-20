#### 

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > HumanResources.Employee

# ![Tables](../../../../Images/Table32.png) [HumanResources].[Employee]

---

## <a name="#description"></a>MS_Description

Employee information such as salary, department, and title.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 290 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:55 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Computed | Max Length (Bytes) | Allow Nulls | Default | Description |
|---|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_Employee_BusinessEntityID: BusinessEntityID](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_Employee_Person_BusinessEntityID: [Person].[Person].BusinessEntityID](../../../../Images/fk.png)](#foreignkeys) | BusinessEntityID | int |  | 4 | NO |  | _Primary key for Employee records.  Foreign key to BusinessEntity.BusinessEntityID._ |
| [![Indexes AK_Employee_NationalIDNumber](../../../../Images/Index.png)](#indexes) | NationalIDNumber | nvarchar(15) |  | 30 | NO |  | _Unique national identification number such as a social security number._ |
| [![Indexes AK_Employee_LoginID](../../../../Images/Index.png)](#indexes) | LoginID | nvarchar(256) |  | 512 | NO |  | _Network login._ |
| [![Indexes IX_Employee_OrganizationLevel_OrganizationNode
IX_Employee_OrganizationNode](../../../../Images/Index.png)](#indexes)(2) | OrganizationNode | hierarchyid |  | 892 | YES |  | _Where the employee is located in corporate hierarchy._ |
| [![Indexes IX_Employee_OrganizationLevel_OrganizationNode](../../../../Images/Index.png)](#indexes) | OrganizationLevel | smallint | YES | 2 | YES |  | _The depth of the employee in the corporate hierarchy._ |
|  | JobTitle | nvarchar(50) |  | 100 | NO |  | _Work title such as Buyer or Sales Representative._ |
| [![Check Constraints CK_Employee_BirthDate : ([BirthDate]>='1930-01-01' AND [BirthDate]<=dateadd(year,(-18),getdate()))](../../../../Images/c-constraint.png)](#checkconstraints) | BirthDate | date |  | 3 | NO |  | _Date of birth._ |
| [![Check Constraints CK_Employee_MaritalStatus : (upper([MaritalStatus])='S' OR upper([MaritalStatus])='M')](../../../../Images/c-constraint.png)](#checkconstraints) | MaritalStatus | nchar(1) |  | 2 | NO |  | _M = Married, S = Single_ |
| [![Check Constraints CK_Employee_Gender : (upper([Gender])='F' OR upper([Gender])='M')](../../../../Images/c-constraint.png)](#checkconstraints) | Gender | nchar(1) |  | 2 | NO |  | _M = Male, F = Female_ |
| [![Check Constraints CK_Employee_HireDate : ([HireDate]>='1996-07-01' AND [HireDate]<=dateadd(day,(1),getdate()))](../../../../Images/c-constraint.png)](#checkconstraints) | HireDate | date |  | 3 | NO |  | _Employee hired on this date._ |
|  | SalariedFlag | [[dbo].[Flag]](../Programmability/Types/User-Defined_Data_Types/Flag.md) |  | 1 | NO | ((1)) | _Job classification. 0 = Hourly, not exempt from collective bargaining. 1 = Salaried, exempt from collective bargaining._ |
| [![Check Constraints CK_Employee_VacationHours : ([VacationHours]>=((-40)) AND [VacationHours]<=(240))](../../../../Images/c-constraint.png)](#checkconstraints) | VacationHours | smallint |  | 2 | NO | ((0)) | _Number of available vacation hours._ |
| [![Check Constraints CK_Employee_SickLeaveHours : ([SickLeaveHours]>=(0) AND [SickLeaveHours]<=(120))](../../../../Images/c-constraint.png)](#checkconstraints) | SickLeaveHours | smallint |  | 2 | NO | ((0)) | _Number of available sick leave hours._ |
|  | CurrentFlag | [[dbo].[Flag]](../Programmability/Types/User-Defined_Data_Types/Flag.md) |  | 1 | NO | ((1)) | _0 = Inactive, 1 = Active_ |
| [![Indexes AK_Employee_rowguid](../../../../Images/Index.png)](#indexes) | rowguid | uniqueidentifier |  | 16 | NO | (newid()) | _ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample._ |
|  | ModifiedDate | datetime |  | 8 | NO | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#computedcolumns"></a>Computed columns

| Name | Column definition |
|---|---|
| OrganizationLevel | ([OrganizationNode].[GetLevel]()) |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_Employee_BusinessEntityID: BusinessEntityID](../../../../Images/pkcluster.png)](#indexes) | PK_Employee_BusinessEntityID | BusinessEntityID | YES | _Primary key (clustered) constraint_ |
|  | AK_Employee_LoginID | LoginID | YES | _Unique nonclustered index._ |
|  | AK_Employee_NationalIDNumber | NationalIDNumber | YES | _Unique nonclustered index._ |
|  | AK_Employee_rowguid | rowguid | YES | _Unique nonclustered index. Used to support replication samples._ |
|  | IX_Employee_OrganizationLevel_OrganizationNode | OrganizationLevel, OrganizationNode |  | _Unique nonclustered index._ |
|  | IX_Employee_OrganizationNode | OrganizationNode |  | _Unique nonclustered index._ |


---

## <a name="#triggers"></a>Triggers

| Name | ANSI Nulls On | Quoted Identifier On | On | Not For Replication | Description |
|---|---|---|---|---|---|
| dEmployee | YES | YES | Instead Of Delete | YES | _INSTEAD OF DELETE trigger which keeps Employees from being deleted._ |


---

## <a name="#checkconstraints"></a>Check Constraints

| Name | On Column | Constraint | Description |
|---|---|---|---|
| CK_Employee_BirthDate | BirthDate | ([BirthDate]>='1930-01-01' AND [BirthDate]<=dateadd(year,(-18),getdate())) | _Check constraint [BirthDate] >= '1930-01-01' AND [BirthDate] <= dateadd(year,(-18),GETDATE())_ |
| CK_Employee_HireDate | HireDate | ([HireDate]>='1996-07-01' AND [HireDate]<=dateadd(day,(1),getdate())) | _Check constraint [HireDate] >= '1996-07-01' AND [HireDate] <= dateadd(day,(1),GETDATE())_ |
| CK_Employee_SickLeaveHours | SickLeaveHours | ([SickLeaveHours]>=(0) AND [SickLeaveHours]<=(120)) | _Check constraint [SickLeaveHours] >= (0) AND [SickLeaveHours] <= (120)_ |
| CK_Employee_VacationHours | VacationHours | ([VacationHours]>=((-40)) AND [VacationHours]<=(240)) | _Check constraint [VacationHours] >= (-40) AND [VacationHours] <= (240)_ |
| CK_Employee_Gender | Gender | (upper([Gender])='F' OR upper([Gender])='M') | _Check constraint [Gender]='f' OR [Gender]='m' OR [Gender]='F' OR [Gender]='M'_ |
| CK_Employee_MaritalStatus | MaritalStatus | (upper([MaritalStatus])='S' OR upper([MaritalStatus])='M') | _Check constraint [MaritalStatus]='s' OR [MaritalStatus]='m' OR [MaritalStatus]='S' OR [MaritalStatus]='M'_ |


---

## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_Employee_Person_BusinessEntityID | BusinessEntityID->[[Person].[Person].[BusinessEntityID]](Person.md) | _Foreign key constraint referencing Person.BusinessEntityID._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [HumanResources].[Employee]
(
[BusinessEntityID] [int] NOT NULL,
[NationalIDNumber] [nvarchar] (15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[LoginID] [nvarchar] (256) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[OrganizationNode] [sys].[hierarchyid] NULL,
[OrganizationLevel] AS ([OrganizationNode].[GetLevel]()),
[JobTitle] [nvarchar] (50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[BirthDate] [date] NOT NULL,
[MaritalStatus] [nchar] (1) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[Gender] [nchar] (1) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[HireDate] [date] NOT NULL,
[SalariedFlag] [dbo].[Flag] NOT NULL CONSTRAINT [DF_Employee_SalariedFlag] DEFAULT ((1)),
[VacationHours] [smallint] NOT NULL CONSTRAINT [DF_Employee_VacationHours] DEFAULT ((0)),
[SickLeaveHours] [smallint] NOT NULL CONSTRAINT [DF_Employee_SickLeaveHours] DEFAULT ((0)),
[CurrentFlag] [dbo].[Flag] NOT NULL CONSTRAINT [DF_Employee_CurrentFlag] DEFAULT ((1)),
[rowguid] [uniqueidentifier] NOT NULL ROWGUIDCOL CONSTRAINT [DF_Employee_rowguid] DEFAULT (newid()),
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_Employee_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO

CREATE TRIGGER [HumanResources].[dEmployee] ON [HumanResources].[Employee] 
INSTEAD OF DELETE NOT FOR REPLICATION AS 
BEGIN
    DECLARE @Count int;

    SET @Count = @@ROWCOUNT;
    IF @Count = 0 
        RETURN;

    SET NOCOUNT ON;

    BEGIN
        RAISERROR
            (N'Employees cannot be deleted. They can only be marked as not current.', -- Message
            10, -- Severity.
            1); -- State.

        -- Rollback any active or uncommittable transactions
        IF @@TRANCOUNT > 0
        BEGIN
            ROLLBACK TRANSACTION;
        END
    END;
END;
GO
ALTER TABLE [HumanResources].[Employee] ADD CONSTRAINT [CK_Employee_BirthDate] CHECK (([BirthDate]>='1930-01-01' AND [BirthDate]<=dateadd(year,(-18),getdate())))
GO
ALTER TABLE [HumanResources].[Employee] ADD CONSTRAINT [CK_Employee_HireDate] CHECK (([HireDate]>='1996-07-01' AND [HireDate]<=dateadd(day,(1),getdate())))
GO
ALTER TABLE [HumanResources].[Employee] ADD CONSTRAINT [CK_Employee_SickLeaveHours] CHECK (([SickLeaveHours]>=(0) AND [SickLeaveHours]<=(120)))
GO
ALTER TABLE [HumanResources].[Employee] ADD CONSTRAINT [CK_Employee_VacationHours] CHECK (([VacationHours]>=((-40)) AND [VacationHours]<=(240)))
GO
ALTER TABLE [HumanResources].[Employee] ADD CONSTRAINT [CK_Employee_Gender] CHECK ((upper([Gender])='F' OR upper([Gender])='M'))
GO
ALTER TABLE [HumanResources].[Employee] ADD CONSTRAINT [CK_Employee_MaritalStatus] CHECK ((upper([MaritalStatus])='S' OR upper([MaritalStatus])='M'))
GO
ALTER TABLE [HumanResources].[Employee] ADD CONSTRAINT [PK_Employee_BusinessEntityID] PRIMARY KEY CLUSTERED  ([BusinessEntityID]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_Employee_LoginID] ON [HumanResources].[Employee] ([LoginID]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_Employee_NationalIDNumber] ON [HumanResources].[Employee] ([NationalIDNumber]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_Employee_OrganizationLevel_OrganizationNode] ON [HumanResources].[Employee] ([OrganizationLevel], [OrganizationNode]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_Employee_OrganizationNode] ON [HumanResources].[Employee] ([OrganizationNode]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_Employee_rowguid] ON [HumanResources].[Employee] ([rowguid]) ON [PRIMARY]
GO
ALTER TABLE [HumanResources].[Employee] ADD CONSTRAINT [FK_Employee_Person_BusinessEntityID] FOREIGN KEY ([BusinessEntityID]) REFERENCES [Person].[Person] ([BusinessEntityID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Employee information such as salary, department, and title.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date of birth.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'COLUMN', N'BirthDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key for Employee records.  Foreign key to BusinessEntity.BusinessEntityID.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'COLUMN', N'BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'0 = Inactive, 1 = Active', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'COLUMN', N'CurrentFlag'
GO
EXEC sp_addextendedproperty N'MS_Description', N'M = Male, F = Female', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'COLUMN', N'Gender'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Employee hired on this date.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'COLUMN', N'HireDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Work title such as Buyer or Sales Representative.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'COLUMN', N'JobTitle'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Network login.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'COLUMN', N'LoginID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'M = Married, S = Single', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'COLUMN', N'MaritalStatus'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique national identification number such as a social security number.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'COLUMN', N'NationalIDNumber'
GO
EXEC sp_addextendedproperty N'MS_Description', N'The depth of the employee in the corporate hierarchy.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'COLUMN', N'OrganizationLevel'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Where the employee is located in corporate hierarchy.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'COLUMN', N'OrganizationNode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'COLUMN', N'rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Job classification. 0 = Hourly, not exempt from collective bargaining. 1 = Salaried, exempt from collective bargaining.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'COLUMN', N'SalariedFlag'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Number of available sick leave hours.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'COLUMN', N'SickLeaveHours'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Number of available vacation hours.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'COLUMN', N'VacationHours'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [BirthDate] >= ''1930-01-01'' AND [BirthDate] <= dateadd(year,(-18),GETDATE())', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'CONSTRAINT', N'CK_Employee_BirthDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [Gender]=''f'' OR [Gender]=''m'' OR [Gender]=''F'' OR [Gender]=''M''', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'CONSTRAINT', N'CK_Employee_Gender'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [HireDate] >= ''1996-07-01'' AND [HireDate] <= dateadd(day,(1),GETDATE())', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'CONSTRAINT', N'CK_Employee_HireDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [MaritalStatus]=''s'' OR [MaritalStatus]=''m'' OR [MaritalStatus]=''S'' OR [MaritalStatus]=''M''', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'CONSTRAINT', N'CK_Employee_MaritalStatus'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [SickLeaveHours] >= (0) AND [SickLeaveHours] <= (120)', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'CONSTRAINT', N'CK_Employee_SickLeaveHours'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [VacationHours] >= (-40) AND [VacationHours] <= (240)', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'CONSTRAINT', N'CK_Employee_VacationHours'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 1', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'CONSTRAINT', N'DF_Employee_CurrentFlag'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'CONSTRAINT', N'DF_Employee_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of NEWID()', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'CONSTRAINT', N'DF_Employee_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 1 (TRUE)', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'CONSTRAINT', N'DF_Employee_SalariedFlag'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 0', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'CONSTRAINT', N'DF_Employee_SickLeaveHours'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 0', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'CONSTRAINT', N'DF_Employee_VacationHours'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Person.BusinessEntityID.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'CONSTRAINT', N'FK_Employee_Person_BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'CONSTRAINT', N'PK_Employee_BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'INDEX', N'AK_Employee_LoginID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'INDEX', N'AK_Employee_NationalIDNumber'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index. Used to support replication samples.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'INDEX', N'AK_Employee_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'INDEX', N'IX_Employee_OrganizationLevel_OrganizationNode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'INDEX', N'IX_Employee_OrganizationNode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'INDEX', N'PK_Employee_BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'INSTEAD OF DELETE trigger which keeps Employees from being deleted.', 'SCHEMA', N'HumanResources', 'TABLE', N'Employee', 'TRIGGER', N'dEmployee'
GO

```


---

## <a name="#uses"></a>Uses

DEPENDENCYLIST* [[Person].[Person]](Person.md)
* [[dbo].[Flag]](../Programmability/Types/User-Defined_Data_Types/Flag.md)
* [HumanResources](../Security/Schemas/HumanResources.md)


---

## <a name="#usedby"></a>Used By

DEPENDENCYLIST* [[HumanResources].[EmployeeDepartmentHistory]](EmployeeDepartmentHistory.md)
* [[HumanResources].[EmployeePayHistory]](EmployeePayHistory.md)
* [[HumanResources].[JobCandidate]](JobCandidate.md)
* [[Production].[Document]](Document.md)
* [[Purchasing].[PurchaseOrderHeader]](PurchaseOrderHeader.md)
* [[Sales].[SalesPerson]](SalesPerson.md)
* [[HumanResources].[vEmployee]](../Views/vEmployee.md)
* [[HumanResources].[vEmployeeDepartment]](../Views/vEmployeeDepartment.md)
* [[HumanResources].[vEmployeeDepartmentHistory]](../Views/vEmployeeDepartmentHistory.md)
* [[Sales].[vSalesPerson]](../Views/vSalesPerson.md)
* [[Sales].[vSalesPersonSalesByFiscalYears]](../Views/vSalesPersonSalesByFiscalYears.md)
* [[dbo].[uspGetEmployeeManagers]](../Programmability/Stored_Procedures/uspGetEmployeeManagers.md)
* [[dbo].[uspGetManagerEmployees]](../Programmability/Stored_Procedures/uspGetManagerEmployees.md)
* [[HumanResources].[uspUpdateEmployeeHireInfo]](../Programmability/Stored_Procedures/uspUpdateEmployeeHireInfo.md)
* [[HumanResources].[uspUpdateEmployeeLogin]](../Programmability/Stored_Procedures/uspUpdateEmployeeLogin.md)
* [[HumanResources].[uspUpdateEmployeePersonalInfo]](../Programmability/Stored_Procedures/uspUpdateEmployeePersonalInfo.md)
* [[dbo].[ufnGetContactInformation]](../Programmability/Functions/Table-valued_Functions/ufnGetContactInformation.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

