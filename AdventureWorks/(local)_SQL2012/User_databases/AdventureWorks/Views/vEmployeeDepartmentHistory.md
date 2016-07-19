
# ![Views](../../../../Images/View32.png) [HumanResources].[vEmployeeDepartmentHistory]

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Views](Views_.md) > HumanResources.vEmployeeDepartmentHistory

## <a name="#description"></a>MS_Description
Returns employee name and current and previous departments.
## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| ANSI Nulls On | YES |
| Quoted Identifier On | YES |
| Created | 13:14:55 14 March 2012 |
| Last Modified | 13:14:55 14 March 2012 |


## <a name="#columns"></a>Columns

| Name |
|---|
| BusinessEntityID |
| Title |
| FirstName |
| MiddleName |
| LastName |
| Suffix |
| Shift |
| Department |
| GroupName |
| StartDate |
| EndDate |


## <a name="#sqlscript"></a>SQL Script
```sql

CREATE VIEW [HumanResources].[vEmployeeDepartmentHistory] 
AS 
SELECT 
    e.[BusinessEntityID] 
    ,p.[Title] 
    ,p.[FirstName] 
    ,p.[MiddleName] 
    ,p.[LastName] 
    ,p.[Suffix] 
    ,s.[Name] AS [Shift]
    ,d.[Name] AS [Department] 
    ,d.[GroupName] 
    ,edh.[StartDate] 
    ,edh.[EndDate]
FROM [HumanResources].[Employee] e
	INNER JOIN [Person].[Person] p
	ON p.[BusinessEntityID] = e.[BusinessEntityID]
    INNER JOIN [HumanResources].[EmployeeDepartmentHistory] edh 
    ON e.[BusinessEntityID] = edh.[BusinessEntityID] 
    INNER JOIN [HumanResources].[Department] d 
    ON edh.[DepartmentID] = d.[DepartmentID] 
    INNER JOIN [HumanResources].[Shift] s
    ON s.[ShiftID] = edh.[ShiftID];
GO
EXEC sp_addextendedproperty N'MS_Description', N'Returns employee name and current and previous departments.', 'SCHEMA', N'HumanResources', 'VIEW', N'vEmployeeDepartmentHistory', NULL, NULL
GO

```

## <a name="#uses"></a>Uses
DEPENDENCYLIST
* [[HumanResources].[Department]](../Tables/Department.md)
* [[HumanResources].[Employee]](../Tables/Employee.md)
* [[HumanResources].[EmployeeDepartmentHistory]](../Tables/EmployeeDepartmentHistory.md)
* [[HumanResources].[Shift]](../Tables/Shift.md)
* [[Person].[Person]](../Tables/Person.md)
* [HumanResources](../Security/Schemas/HumanResources.md)

FOOTER: FOOTER: Author:  Chris Whitworth
FOOTER: Created: 19 July 2016 09:34
FOOTER: Copyright 2016 - All Rights Reserved

