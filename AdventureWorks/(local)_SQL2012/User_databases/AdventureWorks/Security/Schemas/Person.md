#### 

[Project](../../../../../index.md) > [(local)\\SQL2012](../../../../index.md) > [User databases](../../../index.md) > [AdventureWorks](../../index.md) > [Security](../index.md) > [Schemas](Schemas.md) > Person

# ![Schemas](../../../../../Images/Schema32.png) Person

---

## <a name="#description"></a>MS_Description

Contains objects related to names and addresses of customers, vendors, and employees

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Owner | dbo |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE SCHEMA [Person]
AUTHORIZATION [dbo]
GO
EXEC sp_addextendedproperty N'MS_Description', N'Contains objects related to names and addresses of customers, vendors, and employees', 'SCHEMA', N'Person', NULL, NULL, NULL, NULL
GO

```


---

## <a name="#usedby"></a>Used By

DEPENDENCYLIST* [[Person].[Address]](../../Tables/Address.md)
* [[Person].[AddressType]](../../Tables/AddressType.md)
* [[Person].[BusinessEntity]](../../Tables/BusinessEntity.md)
* [[Person].[BusinessEntityAddress]](../../Tables/BusinessEntityAddress.md)
* [[Person].[BusinessEntityContact]](../../Tables/BusinessEntityContact.md)
* [[Person].[ContactType]](../../Tables/ContactType.md)
* [[Person].[CountryRegion]](../../Tables/CountryRegion.md)
* [[Person].[EmailAddress]](../../Tables/EmailAddress.md)
* [[Person].[Password]](../../Tables/Password.md)
* [[Person].[Person]](../../Tables/Person.md)
* [[Person].[PersonPhone]](../../Tables/PersonPhone.md)
* [[Person].[PhoneNumberType]](../../Tables/PhoneNumberType.md)
* [[Person].[StateProvince]](../../Tables/StateProvince.md)
* [[Person].[vAdditionalContactInfo]](../../Views/vAdditionalContactInfo.md)
* [[Person].[vStateProvinceCountryRegion]](../../Views/vStateProvinceCountryRegion.md)
* [[Person].[AdditionalContactInfoSchemaCollection]](../../Programmability/Types/XML_Schema_Collections/AdditionalContactInfoSchemaCollection.md)
* [[Person].[IndividualSurveySchemaCollection]](../../Programmability/Types/XML_Schema_Collections/IndividualSurveySchemaCollection.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

