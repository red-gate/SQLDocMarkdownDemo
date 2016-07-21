#### asdasdasd

[Project](../../../../../index.md) > [(local)\\SQL2012](../../../../index.md) > [User databases](../../../index.md) > [AdventureWorks](../../index.md) > [Programmability](../index.md) > Stored Procedures

# ![Stored Procedures](../../../../../Images/StoredProcedure32.png) Stored Procedures

---

## <a name="#objects"></a>Objects

| Name | Description |
|---|---|
| [dbo.uspGetBillOfMaterials](uspGetBillOfMaterials.md) | _Stored procedure using a recursive query to return a multi-level bill of material for the specified ProductID._ |
| [dbo.uspGetEmployeeManagers](uspGetEmployeeManagers.md) | _Stored procedure using a recursive query to return the direct and indirect managers of the specified employee._ |
| [dbo.uspGetManagerEmployees](uspGetManagerEmployees.md) | _Stored procedure using a recursive query to return the direct and indirect employees of the specified manager._ |
| [dbo.uspGetWhereUsedProductID](uspGetWhereUsedProductID.md) | _Stored procedure using a recursive query to return all components or assemblies that directly or indirectly use the specified ProductID._ |
| [dbo.uspLogError](uspLogError.md) | _Logs error information in the ErrorLog table about the error that caused execution to jump to the CATCH block of a TRY...CATCH construct. Should be executed from within the scope of a CATCH block otherwise it will return without inserting error information._ |
| [dbo.uspPrintError](uspPrintError.md) | _Prints error information about the error that caused execution to jump to the CATCH block of a TRY...CATCH construct. Should be executed from within the scope of a CATCH block otherwise it will return without printing any error information._ |
| [dbo.uspSearchCandidateResumes](uspSearchCandidateResumes.md) |  |
| [HumanResources.uspUpdateEmployeeHireInfo](uspUpdateEmployeeHireInfo.md) | _Updates the Employee table and inserts a new row in the EmployeePayHistory table with the values specified in the input parameters._ |
| [HumanResources.uspUpdateEmployeeLogin](uspUpdateEmployeeLogin.md) | _Updates the Employee table with the values specified in the input parameters for the given BusinessEntityID._ |
| [HumanResources.uspUpdateEmployeePersonalInfo](uspUpdateEmployeePersonalInfo.md) | _Updates the Employee table with the values specified in the input parameters for the given EmployeeID._ |


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 12:25

