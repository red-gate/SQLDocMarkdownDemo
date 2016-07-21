#### asdasdasd

[Project](../../../../../index.md) > [(local)\\SQL2012](../../../../index.md) > [User databases](../../../index.md) > [AdventureWorks](../../index.md) > [Programmability](../index.md) > [Stored Procedures](Stored_Procedures.md) > HumanResources.uspUpdateEmployeePersonalInfo

# ![Stored Procedures](../../../../../Images/StoredProcedure32.png) [HumanResources].[uspUpdateEmployeePersonalInfo]

---

## <a name="#description"></a>MS_Description

Updates the Employee table with the values specified in the input parameters for the given EmployeeID.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| ANSI Nulls On | YES |
| Quoted Identifier On | YES |


---

## <a name="#parameters"></a>Parameters

| Name | Data Type | Max Length (Bytes) | Description |
|---|---|---|---|
| @BusinessEntityID | int | 4 | _Input parameter for the stored procedure uspUpdateEmployeePersonalInfo. Enter a valid BusinessEntityID from the HumanResources.Employee table._ |
| @NationalIDNumber | nvarchar(15) | 30 | _Input parameter for the stored procedure uspUpdateEmployeeHireInfo. Enter a national ID for the employee._ |
| @BirthDate | datetime | 8 | _Input parameter for the stored procedure uspUpdateEmployeeHireInfo. Enter a birth date for the employee._ |
| @MaritalStatus | nchar | 1 | _Input parameter for the stored procedure uspUpdateEmployeeHireInfo. Enter a marital status for the employee._ |
| @Gender | nchar | 1 | _Input parameter for the stored procedure uspUpdateEmployeeHireInfo. Enter a gender for the employee._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql

CREATE PROCEDURE [HumanResources].[uspUpdateEmployeePersonalInfo]
    @BusinessEntityID [int], 
    @NationalIDNumber [nvarchar](15), 
    @BirthDate [datetime], 
    @MaritalStatus [nchar](1), 
    @Gender [nchar](1)
WITH EXECUTE AS CALLER
AS
BEGIN
    SET NOCOUNT ON;

    BEGIN TRY
        UPDATE [HumanResources].[Employee] 
        SET [NationalIDNumber] = @NationalIDNumber 
            ,[BirthDate] = @BirthDate 
            ,[MaritalStatus] = @MaritalStatus 
            ,[Gender] = @Gender 
        WHERE [BusinessEntityID] = @BusinessEntityID;
    END TRY
    BEGIN CATCH
        EXECUTE [dbo].[uspLogError];
    END CATCH;
END;
GO
EXEC sp_addextendedproperty N'MS_Description', N'Updates the Employee table with the values specified in the input parameters for the given EmployeeID.', 'SCHEMA', N'HumanResources', 'PROCEDURE', N'uspUpdateEmployeePersonalInfo', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Input parameter for the stored procedure uspUpdateEmployeeHireInfo. Enter a birth date for the employee.', 'SCHEMA', N'HumanResources', 'PROCEDURE', N'uspUpdateEmployeePersonalInfo', 'PARAMETER', N'@BirthDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Input parameter for the stored procedure uspUpdateEmployeePersonalInfo. Enter a valid BusinessEntityID from the HumanResources.Employee table.', 'SCHEMA', N'HumanResources', 'PROCEDURE', N'uspUpdateEmployeePersonalInfo', 'PARAMETER', N'@BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Input parameter for the stored procedure uspUpdateEmployeeHireInfo. Enter a gender for the employee.', 'SCHEMA', N'HumanResources', 'PROCEDURE', N'uspUpdateEmployeePersonalInfo', 'PARAMETER', N'@Gender'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Input parameter for the stored procedure uspUpdateEmployeeHireInfo. Enter a marital status for the employee.', 'SCHEMA', N'HumanResources', 'PROCEDURE', N'uspUpdateEmployeePersonalInfo', 'PARAMETER', N'@MaritalStatus'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Input parameter for the stored procedure uspUpdateEmployeeHireInfo. Enter a national ID for the employee.', 'SCHEMA', N'HumanResources', 'PROCEDURE', N'uspUpdateEmployeePersonalInfo', 'PARAMETER', N'@NationalIDNumber'
GO

```


---

## <a name="#uses"></a>Uses

* [[HumanResources].[Employee]](../../Tables/Employee.md)
* [[dbo].[uspLogError]](uspLogError.md)
* [HumanResources](../../Security/Schemas/HumanResources.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 14:15

