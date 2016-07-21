#### asdasdasd

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > HumanResources.EmployeePayHistory

# ![Tables](../../../../Images/Table32.png) [HumanResources].[EmployeePayHistory]

---

## <a name="#description"></a>MS_Description

Employee pay history.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Row Count (~) | 316 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:54 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Default | Description |
|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_EmployeePayHistory_BusinessEntityID_RateChangeDate: BusinessEntityID\RateChangeDate](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_EmployeePayHistory_Employee_BusinessEntityID: [HumanResources].[Employee].BusinessEntityID](../../../../Images/fk.png)](#foreignkeys) | BusinessEntityID | int | 4 | NO |  | _Employee identification number. Foreign key to Employee.BusinessEntityID._ |
| [![Cluster Primary Key PK_EmployeePayHistory_BusinessEntityID_RateChangeDate: BusinessEntityID\RateChangeDate](../../../../Images/pkcluster.png)](#indexes) | RateChangeDate | datetime | 8 | NO |  | _Date the change in pay is effective_ |
| [![Check Constraints CK_EmployeePayHistory_Rate : ([Rate]>=(6.50) AND [Rate]<=(200.00))](../../../../Images/c-constraint.png)](#checkconstraints) | Rate | money | 8 | NO |  | _Salary hourly rate._ |
| [![Check Constraints CK_EmployeePayHistory_PayFrequency : ([PayFrequency]=(2) OR [PayFrequency]=(1))](../../../../Images/c-constraint.png)](#checkconstraints) | PayFrequency | tinyint | 1 | NO |  | _1 = Salary received monthly, 2 = Salary received biweekly_ |
|  | ModifiedDate | datetime | 8 | NO | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_EmployeePayHistory_BusinessEntityID_RateChangeDate: BusinessEntityID\RateChangeDate](../../../../Images/pkcluster.png)](#indexes) | PK_EmployeePayHistory_BusinessEntityID_RateChangeDate | BusinessEntityID, RateChangeDate | YES | _Primary key (clustered) constraint_ |


---

## <a name="#checkconstraints"></a>Check Constraints

| Name | On Column | Constraint | Description |
|---|---|---|---|
| CK_EmployeePayHistory_PayFrequency | PayFrequency | ([PayFrequency]=(2) OR [PayFrequency]=(1)) | _Check constraint [PayFrequency]=(3) OR [PayFrequency]=(2) OR [PayFrequency]=(1)_ |
| CK_EmployeePayHistory_Rate | Rate | ([Rate]>=(6.50) AND [Rate]<=(200.00)) | _Check constraint [Rate] >= (6.50) AND [Rate] <= (200.00)_ |


---

## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_EmployeePayHistory_Employee_BusinessEntityID | BusinessEntityID->[[HumanResources].[Employee].[BusinessEntityID]](Employee.md) | _Foreign key constraint referencing Employee.EmployeeID._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [HumanResources].[EmployeePayHistory]
(
[BusinessEntityID] [int] NOT NULL,
[RateChangeDate] [datetime] NOT NULL,
[Rate] [money] NOT NULL,
[PayFrequency] [tinyint] NOT NULL,
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_EmployeePayHistory_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [HumanResources].[EmployeePayHistory] ADD CONSTRAINT [CK_EmployeePayHistory_PayFrequency] CHECK (([PayFrequency]=(2) OR [PayFrequency]=(1)))
GO
ALTER TABLE [HumanResources].[EmployeePayHistory] ADD CONSTRAINT [CK_EmployeePayHistory_Rate] CHECK (([Rate]>=(6.50) AND [Rate]<=(200.00)))
GO
ALTER TABLE [HumanResources].[EmployeePayHistory] ADD CONSTRAINT [PK_EmployeePayHistory_BusinessEntityID_RateChangeDate] PRIMARY KEY CLUSTERED  ([BusinessEntityID], [RateChangeDate]) ON [PRIMARY]
GO
ALTER TABLE [HumanResources].[EmployeePayHistory] ADD CONSTRAINT [FK_EmployeePayHistory_Employee_BusinessEntityID] FOREIGN KEY ([BusinessEntityID]) REFERENCES [HumanResources].[Employee] ([BusinessEntityID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Employee pay history.', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeePayHistory', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Employee identification number. Foreign key to Employee.BusinessEntityID.', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeePayHistory', 'COLUMN', N'BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeePayHistory', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'1 = Salary received monthly, 2 = Salary received biweekly', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeePayHistory', 'COLUMN', N'PayFrequency'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Salary hourly rate.', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeePayHistory', 'COLUMN', N'Rate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date the change in pay is effective', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeePayHistory', 'COLUMN', N'RateChangeDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [PayFrequency]=(3) OR [PayFrequency]=(2) OR [PayFrequency]=(1)', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeePayHistory', 'CONSTRAINT', N'CK_EmployeePayHistory_PayFrequency'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [Rate] >= (6.50) AND [Rate] <= (200.00)', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeePayHistory', 'CONSTRAINT', N'CK_EmployeePayHistory_Rate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeePayHistory', 'CONSTRAINT', N'DF_EmployeePayHistory_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Employee.EmployeeID.', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeePayHistory', 'CONSTRAINT', N'FK_EmployeePayHistory_Employee_BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeePayHistory', 'CONSTRAINT', N'PK_EmployeePayHistory_BusinessEntityID_RateChangeDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'HumanResources', 'TABLE', N'EmployeePayHistory', 'INDEX', N'PK_EmployeePayHistory_BusinessEntityID_RateChangeDate'
GO

```


---

## <a name="#uses"></a>Uses

* [[HumanResources].[Employee]](Employee.md)
* [HumanResources](../Security/Schemas/HumanResources.md)


---

## <a name="#usedby"></a>Used By

* [[HumanResources].[uspUpdateEmployeeHireInfo]](../Programmability/Stored_Procedures/uspUpdateEmployeeHireInfo.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 14:15

