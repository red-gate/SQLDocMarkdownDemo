#### 

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > Tables

# ![Tables](../../../../Images/Table32.png) Tables

---

## <a name="#objects"></a>Objects

| Name | Description |
|---|---|
| [dbo.AWBuildVersion](AWBuildVersion.md) | _Current version number of the AdventureWorks 2012 sample database. _ |
| [dbo.DatabaseLog](DatabaseLog.md) | _Audit table tracking all DDL changes made to the AdventureWorks database. Data is captured by the database trigger ddlDatabaseTriggerLog._ |
| [dbo.ErrorLog](ErrorLog.md) | _Audit table tracking errors in the the AdventureWorks database that are caught by the CATCH block of a TRY...CATCH construct. Data is inserted by stored procedure dbo.uspLogError when it is executed from inside the CATCH block of a TRY...CATCH construct._ |
| [HumanResources.Department](Department.md) | _Lookup table containing the departments within the Adventure Works Cycles company._ |
| [HumanResources.Employee](Employee.md) | _Employee information such as salary, department, and title._ |
| [HumanResources.EmployeeDepartmentHistory](EmployeeDepartmentHistory.md) | _Employee department transfers._ |
| [HumanResources.EmployeePayHistory](EmployeePayHistory.md) | _Employee pay history._ |
| [HumanResources.JobCandidate](JobCandidate.md) | _Résumés submitted to Human Resources by job applicants._ |
| [HumanResources.Shift](Shift.md) | _Work shift lookup table._ |
| [Person.Address](Address.md) | _Street address information for customers, employees, and vendors._ |
| [Person.AddressType](AddressType.md) | _Types of addresses stored in the Address table. _ |
| [Person.BusinessEntity](BusinessEntity.md) | _Source of the ID that connects vendors, customers, and employees with address and contact information._ |
| [Person.BusinessEntityAddress](BusinessEntityAddress.md) | _Cross-reference table mapping customers, vendors, and employees to their addresses._ |
| [Person.BusinessEntityContact](BusinessEntityContact.md) | _Cross-reference table mapping stores, vendors, and employees to people_ |
| [Person.ContactType](ContactType.md) | _Lookup table containing the types of business entity contacts._ |
| [Person.CountryRegion](CountryRegion.md) | _Lookup table containing the ISO standard codes for countries and regions._ |
| [Person.EmailAddress](EmailAddress.md) | _Where to send a person email._ |
| [Person.Password](Password.md) | _One way hashed authentication information_ |
| [Person.Person](Person.md) | _Human beings involved with AdventureWorks: employees, customer contacts, and vendor contacts._ |
| [Person.PersonPhone](PersonPhone.md) | _Telephone number and type of a person._ |
| [Person.PhoneNumberType](PhoneNumberType.md) | _Type of phone number of a person._ |
| [Person.StateProvince](StateProvince.md) | _State and province lookup table._ |
| [Production.BillOfMaterials](BillOfMaterials.md) | _Items required to make bicycles and bicycle subassemblies. It identifies the heirarchical relationship between a parent product and its components._ |
| [Production.Culture](Culture.md) | _Lookup table containing the languages in which some AdventureWorks data is stored._ |
| [Production.Document](Document.md) | _Product maintenance documents._ |
| [Production.Illustration](Illustration.md) | _Bicycle assembly diagrams._ |
| [Production.Location](Location.md) | _Product inventory and manufacturing locations._ |
| [Production.Product](Product.md) | _Products sold or used in the manfacturing of sold products._ |
| [Production.ProductCategory](ProductCategory.md) | _High-level product categorization._ |
| [Production.ProductCostHistory](ProductCostHistory.md) | _Changes in the cost of a product over time._ |
| [Production.ProductDescription](ProductDescription.md) | _Product descriptions in several languages._ |
| [Production.ProductDocument](ProductDocument.md) | _Cross-reference table mapping products to related product documents._ |
| [Production.ProductInventory](ProductInventory.md) | _Product inventory information._ |
| [Production.ProductListPriceHistory](ProductListPriceHistory.md) | _Changes in the list price of a product over time._ |
| [Production.ProductModel](ProductModel.md) | _Product model classification._ |
| [Production.ProductModelIllustration](ProductModelIllustration.md) | _Cross-reference table mapping product models and illustrations._ |
| [Production.ProductModelProductDescriptionCulture](ProductModelProductDescriptionCulture.md) | _Cross-reference table mapping product descriptions and the language the description is written in._ |
| [Production.ProductPhoto](ProductPhoto.md) | _Product images._ |
| [Production.ProductProductPhoto](ProductProductPhoto.md) | _Cross-reference table mapping products and product photos._ |
| [Production.ProductReview](ProductReview.md) | _Customer reviews of products they have purchased._ |
| [Production.ProductSubcategory](ProductSubcategory.md) | _Product subcategories. See ProductCategory table._ |
| [Production.ScrapReason](ScrapReason.md) | _Manufacturing failure reasons lookup table._ |
| [Production.TransactionHistory](TransactionHistory.md) | _Record of each purchase order, sales order, or work order transaction year to date._ |
| [Production.TransactionHistoryArchive](TransactionHistoryArchive.md) | _Transactions for previous years._ |
| [Production.UnitMeasure](UnitMeasure.md) | _Unit of measure lookup table._ |
| [Production.WorkOrder](WorkOrder.md) | _Manufacturing work orders._ |
| [Production.WorkOrderRouting](WorkOrderRouting.md) | _Work order details._ |
| [Purchasing.ProductVendor](ProductVendor.md) | _Cross-reference table mapping vendors with the products they supply._ |
| [Purchasing.PurchaseOrderDetail](PurchaseOrderDetail.md) | _Individual products associated with a specific purchase order. See PurchaseOrderHeader._ |
| [Purchasing.PurchaseOrderHeader](PurchaseOrderHeader.md) | _General purchase order information. See PurchaseOrderDetail._ |
| [Purchasing.ShipMethod](ShipMethod.md) | _Shipping company lookup table._ |
| [Purchasing.Vendor](Vendor.md) | _Companies from whom Adventure Works Cycles purchases parts or other goods._ |
| [Sales.CountryRegionCurrency](CountryRegionCurrency.md) | _Cross-reference table mapping ISO currency codes to a country or region._ |
| [Sales.CreditCard](CreditCard.md) | _Customer credit card information._ |
| [Sales.Currency](Currency.md) | _Lookup table containing standard ISO currencies._ |
| [Sales.CurrencyRate](CurrencyRate.md) | _Currency exchange rates._ |
| [Sales.Customer](Customer.md) | _Current customer information. Also see the Person and Store tables._ |
| [Sales.PersonCreditCard](PersonCreditCard.md) | _Cross-reference table mapping people to their credit card information in the CreditCard table. _ |
| [Sales.SalesOrderDetail](SalesOrderDetail.md) | _Individual products associated with a specific sales order. See SalesOrderHeader._ |
| [Sales.SalesOrderHeader](SalesOrderHeader.md) | _General sales order information._ |
| [Sales.SalesOrderHeaderSalesReason](SalesOrderHeaderSalesReason.md) | _Cross-reference table mapping sales orders to sales reason codes._ |
| [Sales.SalesPerson](SalesPerson.md) | _Sales representative current information._ |
| [Sales.SalesPersonQuotaHistory](SalesPersonQuotaHistory.md) | _Sales performance tracking._ |
| [Sales.SalesReason](SalesReason.md) | _Lookup table of customer purchase reasons._ |
| [Sales.SalesTaxRate](SalesTaxRate.md) | _Tax rate lookup table._ |
| [Sales.SalesTerritory](SalesTerritory.md) | _Sales territory lookup table._ |
| [Sales.SalesTerritoryHistory](SalesTerritoryHistory.md) | _Sales representative transfers to other sales territories._ |
| [Sales.ShoppingCartItem](ShoppingCartItem.md) | _Contains online customer orders until the order is submitted or cancelled._ |
| [Sales.SpecialOffer](SpecialOffer.md) | _Sale discounts lookup table._ |
| [Sales.SpecialOfferProduct](SpecialOfferProduct.md) | _Cross-reference table mapping products to special offer discounts._ |
| [Sales.Store](Store.md) | _Customers (resellers) of Adventure Works products._ |


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

