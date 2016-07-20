#### 

[Project](../../../../../index.md) > [(local)\\SQL2012](../../../../index.md) > [User databases](../../../index.md) > [AdventureWorks](../../index.md) > [Security](../index.md) > [Schemas](Schemas.md) > Sales

# ![Schemas](../../../../../Images/Schema32.png) Sales

---

## <a name="#description"></a>MS_Description

Contains objects related to customers, sales orders, and sales territories.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Owner | dbo |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE SCHEMA [Sales]
AUTHORIZATION [dbo]
GO
EXEC sp_addextendedproperty N'MS_Description', N'Contains objects related to customers, sales orders, and sales territories.', 'SCHEMA', N'Sales', NULL, NULL, NULL, NULL
GO

```


---

## <a name="#usedby"></a>Used By

DEPENDENCYLIST* [[Sales].[CountryRegionCurrency]](../../Tables/CountryRegionCurrency.md)
* [[Sales].[CreditCard]](../../Tables/CreditCard.md)
* [[Sales].[Currency]](../../Tables/Currency.md)
* [[Sales].[CurrencyRate]](../../Tables/CurrencyRate.md)
* [[Sales].[Customer]](../../Tables/Customer.md)
* [[Sales].[PersonCreditCard]](../../Tables/PersonCreditCard.md)
* [[Sales].[SalesOrderDetail]](../../Tables/SalesOrderDetail.md)
* [[Sales].[SalesOrderHeader]](../../Tables/SalesOrderHeader.md)
* [[Sales].[SalesOrderHeaderSalesReason]](../../Tables/SalesOrderHeaderSalesReason.md)
* [[Sales].[SalesPerson]](../../Tables/SalesPerson.md)
* [[Sales].[SalesPersonQuotaHistory]](../../Tables/SalesPersonQuotaHistory.md)
* [[Sales].[SalesReason]](../../Tables/SalesReason.md)
* [[Sales].[SalesTaxRate]](../../Tables/SalesTaxRate.md)
* [[Sales].[SalesTerritory]](../../Tables/SalesTerritory.md)
* [[Sales].[SalesTerritoryHistory]](../../Tables/SalesTerritoryHistory.md)
* [[Sales].[ShoppingCartItem]](../../Tables/ShoppingCartItem.md)
* [[Sales].[SpecialOffer]](../../Tables/SpecialOffer.md)
* [[Sales].[SpecialOfferProduct]](../../Tables/SpecialOfferProduct.md)
* [[Sales].[Store]](../../Tables/Store.md)
* [[Sales].[vIndividualCustomer]](../../Views/vIndividualCustomer.md)
* [[Sales].[vPersonDemographics]](../../Views/vPersonDemographics.md)
* [[Sales].[vSalesPerson]](../../Views/vSalesPerson.md)
* [[Sales].[vSalesPersonSalesByFiscalYears]](../../Views/vSalesPersonSalesByFiscalYears.md)
* [[Sales].[vStoreWithAddresses]](../../Views/vStoreWithAddresses.md)
* [[Sales].[vStoreWithContacts]](../../Views/vStoreWithContacts.md)
* [[Sales].[vStoreWithDemographics]](../../Views/vStoreWithDemographics.md)
* [[Sales].[StoreSurveySchemaCollection]](../../Programmability/Types/XML_Schema_Collections/StoreSurveySchemaCollection.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

