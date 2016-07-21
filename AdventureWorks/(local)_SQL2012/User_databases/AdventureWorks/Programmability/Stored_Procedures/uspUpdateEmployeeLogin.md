#### asdasdasd

[Project](../../../../../index.md) > [(local)\\SQL2012](../../../../index.md) > [User databases](../../../index.md) > [AdventureWorks](../../index.md) > [Programmability](../index.md) > [Stored Procedures](Stored_Procedures.md) > HumanResources.uspUpdateEmployeeLogin

# ![Stored Procedures](../../../../../Images/StoredProcedure32.png) [HumanResources].[uspUpdateEmployeeLogin]

---

## <a name="#description"></a>MS_Description

Updates the Employee table with the values specified in the input parameters for the given BusinessEntityID.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| ANSI Nulls On | YES |
| Quoted Identifier On | YES |


---

## <a name="#parameters"></a>Parameters

| Name | Data Type | Max Length (Bytes) | Description |
|---|---|---|---|
| @BusinessEntityID | int | 4 | _Input parameter for the stored procedure uspUpdateEmployeeLogin. Enter a valid EmployeeID from the Employee table._ |
| @OrganizationNode | hierarchyid | 892 | _Input parameter for the stored procedure uspUpdateEmployeeHireInfo. Enter a valid ManagerID for the employee._ |
| @LoginID | nvarchar(256) | 512 | _Input parameter for the stored procedure uspUpdateEmployeeHireInfo. Enter a valid login for the employee._ |
| @JobTitle | nvarchar(50) | 100 | _Input parameter for the stored procedure uspUpdateEmployeeHireInfo. Enter a title for the employee._ |
| @HireDate | datetime | 8 | _Input parameter for the stored procedure uspUpdateEmployeeHireInfo. Enter a hire date for the employee._ |
| @CurrentFlag | Flag | 1 | _Input parameter for the stored procedure uspUpdateEmployeeHireInfo. Enter the current flag for the employee._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql

CREATE PROCEDURE [HumanResources].[uspUpdateEmployeeLogin]
    @BusinessEntityID [int], 
    @OrganizationNode [hierarchyid],
    @LoginID [nvarchar](256),
    @JobTitle [nvarchar](50),
    @HireDate [datetime],
    @CurrentFlag [dbo].[Flag]
WITH EXECUTE AS CALLER
AS
BEGIN
    SET NOCOUNT ON;

    BEGIN TRY
        UPDATE [HumanResources].[Employee] 
        SET [OrganizationNode] = @OrganizationNode 
            ,[LoginID] = @LoginID 
            ,[JobTitle] = @JobTitle 
            ,[HireDate] = @HireDate 
            ,[CurrentFlag] = @CurrentFlag 
        WHERE [BusinessEntityID] = @BusinessEntityID;
    END TRY
    BEGIN CATCH
        EXECUTE [dbo].[uspLogError];
    END CATCH;
END;
GO
EXEC sp_addextendedproperty N'MS_Description', N'Updates the Employee table with the values specified in the input parameters for the given BusinessEntityID.', 'SCHEMA', N'HumanResources', 'PROCEDURE', N'uspUpdateEmployeeLogin', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Input parameter for the stored procedure uspUpdateEmployeeLogin. Enter a valid EmployeeID from the Employee table.', 'SCHEMA', N'HumanResources', 'PROCEDURE', N'uspUpdateEmployeeLogin', 'PARAMETER', N'@BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Input parameter for the stored procedure uspUpdateEmployeeHireInfo. Enter the current flag for the employee.', 'SCHEMA', N'HumanResources', 'PROCEDURE', N'uspUpdateEmployeeLogin', 'PARAMETER', N'@CurrentFlag'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Input parameter for the stored procedure uspUpdateEmployeeHireInfo. Enter a hire date for the employee.', 'SCHEMA', N'HumanResources', 'PROCEDURE', N'uspUpdateEmployeeLogin', 'PARAMETER', N'@HireDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Input parameter for the stored procedure uspUpdateEmployeeHireInfo. Enter a title for the employee.', 'SCHEMA', N'HumanResources', 'PROCEDURE', N'uspUpdateEmployeeLogin', 'PARAMETER', N'@JobTitle'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Input parameter for the stored procedure uspUpdateEmployeeHireInfo. Enter a valid login for the employee.', 'SCHEMA', N'HumanResources', 'PROCEDURE', N'uspUpdateEmployeeLogin', 'PARAMETER', N'@LoginID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Input parameter for the stored procedure uspUpdateEmployeeHireInfo. Enter a valid ManagerID for the employee.', 'SCHEMA', N'HumanResources', 'PROCEDURE', N'uspUpdateEmployeeLogin', 'PARAMETER', N'@OrganizationNode'
GO

```


---

## <a name="#uses"></a>Uses

* [[HumanResources].[Employee]](../../Tables/Employee.md)
* [[dbo].[uspLogError]](uspLogError.md)
* [[dbo].[Flag]](../Types/User-Defined_Data_Types/Flag.md)
* [HumanResources](../../Security/Schemas/HumanResources.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 14:15

