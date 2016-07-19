
# ![Schemas](../../../../../Images/Schema32.png) Purchasing

[Project](../../../../../index.md) > [(local)\\SQL2012](../../../../index.md) > [User databases](../../../index.md) > [AdventureWorks](../../index.md) > [Security](../index.md) > [Schemas](Schemas_.md) > Purchasing

## <a name="#description"></a>MS_Description
Contains objects related to vendors and purchase orders.
## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Owner | dbo |


## <a name="#sqlscript"></a>SQL Script
```sql
CREATE SCHEMA [Purchasing]
AUTHORIZATION [dbo]
GO
EXEC sp_addextendedproperty N'MS_Description', N'Contains objects related to vendors and purchase orders.', 'SCHEMA', N'Purchasing', NULL, NULL, NULL, NULL
GO

```

## <a name="#usedby"></a>Used By
DEPENDENCYLIST
* [[Purchasing].[ProductVendor]](../../Tables/ProductVendor.md)
* [[Purchasing].[PurchaseOrderDetail]](../../Tables/PurchaseOrderDetail.md)
* [[Purchasing].[PurchaseOrderHeader]](../../Tables/PurchaseOrderHeader.md)
* [[Purchasing].[ShipMethod]](../../Tables/ShipMethod.md)
* [[Purchasing].[Vendor]](../../Tables/Vendor.md)
* [[Purchasing].[vVendorWithAddresses]](../../Views/vVendorWithAddresses.md)
* [[Purchasing].[vVendorWithContacts]](../../Views/vVendorWithContacts.md)

FOOTER: FOOTER: Author:  Chris Whitworth
FOOTER: Created: 19 July 2016 09:34
FOOTER: Copyright 2016 - All Rights Reserved

