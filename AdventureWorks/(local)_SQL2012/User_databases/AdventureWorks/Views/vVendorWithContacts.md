#### asdasdasd

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Views](Views.md) > Purchasing.vVendorWithContacts

# ![Views](../../../../Images/View32.png) [Purchasing].[vVendorWithContacts]

---

## <a name="#description"></a>MS_Description

Vendor (company) names  and the names of vendor employees to contact.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| ANSI Nulls On | YES |
| Quoted Identifier On | YES |
| Created | 13:14:55 14 March 2012 |
| Last Modified | 13:14:55 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Name |
|---|
| BusinessEntityID |
| Name |
| ContactType |
| Title |
| FirstName |
| MiddleName |
| LastName |
| Suffix |
| PhoneNumber |
| PhoneNumberType |
| EmailAddress |
| EmailPromotion |


---

## <a name="#sqlscript"></a>SQL Script

```sql

CREATE VIEW [Purchasing].[vVendorWithContacts] AS 
SELECT 
    v.[BusinessEntityID]
    ,v.[Name]
    ,ct.[Name] AS [ContactType] 
    ,p.[Title] 
    ,p.[FirstName] 
    ,p.[MiddleName] 
    ,p.[LastName] 
    ,p.[Suffix] 
    ,pp.[PhoneNumber] 
	,pnt.[Name] AS [PhoneNumberType]
    ,ea.[EmailAddress] 
    ,p.[EmailPromotion] 
FROM [Purchasing].[Vendor] v
    INNER JOIN [Person].[BusinessEntityContact] bec 
    ON bec.[BusinessEntityID] = v.[BusinessEntityID]
	INNER JOIN [Person].ContactType ct
	ON ct.[ContactTypeID] = bec.[ContactTypeID]
	INNER JOIN [Person].[Person] p
	ON p.[BusinessEntityID] = bec.[PersonID]
	LEFT OUTER JOIN [Person].[EmailAddress] ea
	ON ea.[BusinessEntityID] = p.[BusinessEntityID]
	LEFT OUTER JOIN [Person].[PersonPhone] pp
	ON pp.[BusinessEntityID] = p.[BusinessEntityID]
	LEFT OUTER JOIN [Person].[PhoneNumberType] pnt
	ON pnt.[PhoneNumberTypeID] = pp.[PhoneNumberTypeID];
GO
EXEC sp_addextendedproperty N'MS_Description', N'Vendor (company) names  and the names of vendor employees to contact.', 'SCHEMA', N'Purchasing', 'VIEW', N'vVendorWithContacts', NULL, NULL
GO

```


---

## <a name="#uses"></a>Uses

* [[Person].[BusinessEntityContact]](../Tables/BusinessEntityContact.md)
* [[Person].[ContactType]](../Tables/ContactType.md)
* [[Person].[EmailAddress]](../Tables/EmailAddress.md)
* [[Person].[Person]](../Tables/Person.md)
* [[Person].[PersonPhone]](../Tables/PersonPhone.md)
* [[Person].[PhoneNumberType]](../Tables/PhoneNumberType.md)
* [[Purchasing].[Vendor]](../Tables/Vendor.md)
* [Purchasing](../Security/Schemas/Purchasing.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 14:15

