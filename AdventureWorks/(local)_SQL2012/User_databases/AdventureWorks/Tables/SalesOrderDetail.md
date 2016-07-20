#### 

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Sales.SalesOrderDetail

# ![Tables](../../../../Images/Table32.png) [Sales].[SalesOrderDetail]

---

## <a name="#description"></a>MS_Description

Individual products associated with a specific sales order. See SalesOrderHeader.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 121317 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:55 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Computed | Max Length (Bytes) | Allow Nulls | Identity | Default | Description |
|---|---|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_SalesOrderDetail_SalesOrderID_SalesOrderDetailID: SalesOrderID\SalesOrderDetailID](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_SalesOrderDetail_SalesOrderHeader_SalesOrderID: [Sales].[SalesOrderHeader].SalesOrderID](../../../../Images/fk.png)](#foreignkeys) | SalesOrderID | int |  | 4 | NO |  |  | _Primary key. Foreign key to SalesOrderHeader.SalesOrderID._ |
| [![Cluster Primary Key PK_SalesOrderDetail_SalesOrderID_SalesOrderDetailID: SalesOrderID\SalesOrderDetailID](../../../../Images/pkcluster.png)](#indexes) | SalesOrderDetailID | int |  | 4 | NO | 1 - 1 |  | _Primary key. One incremental unique number per product sold._ |
|  | CarrierTrackingNumber | nvarchar(25) |  | 50 | YES |  |  | _Shipment tracking number supplied by the shipper._ |
| [![Check Constraints CK_SalesOrderDetail_OrderQty : ([OrderQty]>(0))](../../../../Images/c-constraint.png)](#checkconstraints) | OrderQty | smallint |  | 2 | NO |  |  | _Quantity ordered per product._ |
| [![Indexes IX_SalesOrderDetail_ProductID](../../../../Images/Index.png)](#indexes)[![Foreign Keys FK_SalesOrderDetail_SpecialOfferProduct_SpecialOfferIDProductID: [Sales].[SpecialOfferProduct].SpecialOfferID\ProductID](../../../../Images/fk.png)](#foreignkeys) | ProductID | int |  | 4 | NO |  |  | _Product sold to customer. Foreign key to Product.ProductID._ |
| [![Foreign Keys FK_SalesOrderDetail_SpecialOfferProduct_SpecialOfferIDProductID: [Sales].[SpecialOfferProduct].SpecialOfferID\ProductID](../../../../Images/fk.png)](#foreignkeys) | SpecialOfferID | int |  | 4 | NO |  |  | _Promotional code. Foreign key to SpecialOffer.SpecialOfferID._ |
| [![Check Constraints CK_SalesOrderDetail_UnitPrice : ([UnitPrice]>=(0.00))](../../../../Images/c-constraint.png)](#checkconstraints) | UnitPrice | money |  | 8 | NO |  |  | _Selling price of a single product._ |
| [![Check Constraints CK_SalesOrderDetail_UnitPriceDiscount : ([UnitPriceDiscount]>=(0.00))](../../../../Images/c-constraint.png)](#checkconstraints) | UnitPriceDiscount | money |  | 8 | NO |  | ((0.0)) | _Discount amount._ |
|  | LineTotal | numeric(38,6) | YES | 17 | NO |  |  | _Per product subtotal. Computed as UnitPrice * (1 - UnitPriceDiscount) * OrderQty._ |
| [![Indexes AK_SalesOrderDetail_rowguid](../../../../Images/Index.png)](#indexes) | rowguid | uniqueidentifier |  | 16 | NO |  | (newid()) | _ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample._ |
|  | ModifiedDate | datetime |  | 8 | NO |  | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#computedcolumns"></a>Computed columns

| Name | Column definition |
|---|---|
| LineTotal | (isnull(([UnitPrice]*((1.0)-[UnitPriceDiscount]))*[OrderQty],(0.0))) |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_SalesOrderDetail_SalesOrderID_SalesOrderDetailID: SalesOrderID\SalesOrderDetailID](../../../../Images/pkcluster.png)](#indexes) | PK_SalesOrderDetail_SalesOrderID_SalesOrderDetailID | SalesOrderID, SalesOrderDetailID | YES | _Primary key (clustered) constraint_ |
|  | AK_SalesOrderDetail_rowguid | rowguid | YES | _Unique nonclustered index. Used to support replication samples._ |
|  | IX_SalesOrderDetail_ProductID | ProductID |  | _Nonclustered index._ |


---

## <a name="#triggers"></a>Triggers

| Name | ANSI Nulls On | Quoted Identifier On | On | Description |
|---|---|---|---|---|
| iduSalesOrderDetail | YES | YES | After Delete Insert Update | _AFTER INSERT, DELETE, UPDATE trigger that inserts a row in the TransactionHistory table, updates ModifiedDate in SalesOrderDetail and updates the SalesOrderHeader.SubTotal column._ |


---

## <a name="#checkconstraints"></a>Check Constraints

| Name | On Column | Constraint | Description |
|---|---|---|---|
| CK_SalesOrderDetail_OrderQty | OrderQty | ([OrderQty]>(0)) | _Check constraint [OrderQty] > (0)_ |
| CK_SalesOrderDetail_UnitPrice | UnitPrice | ([UnitPrice]>=(0.00)) | _Check constraint [UnitPrice] >= (0.00)_ |
| CK_SalesOrderDetail_UnitPriceDiscount | UnitPriceDiscount | ([UnitPriceDiscount]>=(0.00)) | _Check constraint [UnitPriceDiscount] >= (0.00)_ |


---

## <a name="#foreignkeys"></a>Foreign Keys

| Name | Delete | Columns | Description |
|---|---|---|---|
| FK_SalesOrderDetail_SalesOrderHeader_SalesOrderID | Cascade | SalesOrderID->[[Sales].[SalesOrderHeader].[SalesOrderID]](SalesOrderHeader.md) | _Foreign key constraint referencing SalesOrderHeader.PurchaseOrderID._ |
| FK_SalesOrderDetail_SpecialOfferProduct_SpecialOfferIDProductID |  | SpecialOfferID->[[Sales].[SpecialOfferProduct].[SpecialOfferID]](SpecialOfferProduct.md)
ProductID->[[Sales].[SpecialOfferProduct].[ProductID]](SpecialOfferProduct.md) | _Foreign key constraint referencing SpecialOfferProduct.SpecialOfferIDProductID._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Sales].[SalesOrderDetail]
(
[SalesOrderID] [int] NOT NULL,
[SalesOrderDetailID] [int] NOT NULL IDENTITY(1, 1),
[CarrierTrackingNumber] [nvarchar] (25) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
[OrderQty] [smallint] NOT NULL,
[ProductID] [int] NOT NULL,
[SpecialOfferID] [int] NOT NULL,
[UnitPrice] [money] NOT NULL,
[UnitPriceDiscount] [money] NOT NULL CONSTRAINT [DF_SalesOrderDetail_UnitPriceDiscount] DEFAULT ((0.0)),
[LineTotal] AS (isnull(([UnitPrice]*((1.0)-[UnitPriceDiscount]))*[OrderQty],(0.0))),
[rowguid] [uniqueidentifier] NOT NULL ROWGUIDCOL CONSTRAINT [DF_SalesOrderDetail_rowguid] DEFAULT (newid()),
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_SalesOrderDetail_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO

CREATE TRIGGER [Sales].[iduSalesOrderDetail] ON [Sales].[SalesOrderDetail] 
AFTER INSERT, DELETE, UPDATE AS 
BEGIN
    DECLARE @Count int;

    SET @Count = @@ROWCOUNT;
    IF @Count = 0 
        RETURN;

    SET NOCOUNT ON;

    BEGIN TRY
        -- If inserting or updating these columns
        IF UPDATE([ProductID]) OR UPDATE([OrderQty]) OR UPDATE([UnitPrice]) OR UPDATE([UnitPriceDiscount]) 
        -- Insert record into TransactionHistory
        BEGIN
            INSERT INTO [Production].[TransactionHistory]
                ([ProductID]
                ,[ReferenceOrderID]
                ,[ReferenceOrderLineID]
                ,[TransactionType]
                ,[TransactionDate]
                ,[Quantity]
                ,[ActualCost])
            SELECT 
                inserted.[ProductID]
                ,inserted.[SalesOrderID]
                ,inserted.[SalesOrderDetailID]
                ,'S'
                ,GETDATE()
                ,inserted.[OrderQty]
                ,inserted.[UnitPrice]
            FROM inserted 
                INNER JOIN [Sales].[SalesOrderHeader] 
                ON inserted.[SalesOrderID] = [Sales].[SalesOrderHeader].[SalesOrderID];

            UPDATE [Person].[Person] 
            SET [Demographics].modify('declare default element namespace 
                "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/IndividualSurvey"; 
                replace value of (/IndividualSurvey/TotalPurchaseYTD)[1] 
                with data(/IndividualSurvey/TotalPurchaseYTD)[1] + sql:column ("inserted.LineTotal")') 
            FROM inserted 
                INNER JOIN [Sales].[SalesOrderHeader] AS SOH
                ON inserted.[SalesOrderID] = SOH.[SalesOrderID] 
                INNER JOIN [Sales].[Customer] AS C
                ON SOH.[CustomerID] = C.[CustomerID]
            WHERE C.[PersonID] = [Person].[Person].[BusinessEntityID];
        END;

        -- Update SubTotal in SalesOrderHeader record. Note that this causes the 
        -- SalesOrderHeader trigger to fire which will update the RevisionNumber.
        UPDATE [Sales].[SalesOrderHeader]
        SET [Sales].[SalesOrderHeader].[SubTotal] = 
            (SELECT SUM([Sales].[SalesOrderDetail].[LineTotal])
                FROM [Sales].[SalesOrderDetail]
                WHERE [Sales].[SalesOrderHeader].[SalesOrderID] = [Sales].[SalesOrderDetail].[SalesOrderID])
        WHERE [Sales].[SalesOrderHeader].[SalesOrderID] IN (SELECT inserted.[SalesOrderID] FROM inserted);

        UPDATE [Person].[Person] 
        SET [Demographics].modify('declare default element namespace 
            "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/IndividualSurvey"; 
            replace value of (/IndividualSurvey/TotalPurchaseYTD)[1] 
            with data(/IndividualSurvey/TotalPurchaseYTD)[1] - sql:column("deleted.LineTotal")') 
        FROM deleted 
            INNER JOIN [Sales].[SalesOrderHeader] 
            ON deleted.[SalesOrderID] = [Sales].[SalesOrderHeader].[SalesOrderID] 
            INNER JOIN [Sales].[Customer]
            ON [Sales].[Customer].[CustomerID] = [Sales].[SalesOrderHeader].[CustomerID]
        WHERE [Sales].[Customer].[PersonID] = [Person].[Person].[BusinessEntityID];
    END TRY
    BEGIN CATCH
        EXECUTE [dbo].[uspPrintError];

        -- Rollback any active or uncommittable transactions before
        -- inserting information in the ErrorLog
        IF @@TRANCOUNT > 0
        BEGIN
            ROLLBACK TRANSACTION;
        END

        EXECUTE [dbo].[uspLogError];
    END CATCH;
END;
GO
ALTER TABLE [Sales].[SalesOrderDetail] ADD CONSTRAINT [CK_SalesOrderDetail_OrderQty] CHECK (([OrderQty]>(0)))
GO
ALTER TABLE [Sales].[SalesOrderDetail] ADD CONSTRAINT [CK_SalesOrderDetail_UnitPrice] CHECK (([UnitPrice]>=(0.00)))
GO
ALTER TABLE [Sales].[SalesOrderDetail] ADD CONSTRAINT [CK_SalesOrderDetail_UnitPriceDiscount] CHECK (([UnitPriceDiscount]>=(0.00)))
GO
ALTER TABLE [Sales].[SalesOrderDetail] ADD CONSTRAINT [PK_SalesOrderDetail_SalesOrderID_SalesOrderDetailID] PRIMARY KEY CLUSTERED  ([SalesOrderID], [SalesOrderDetailID]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_SalesOrderDetail_ProductID] ON [Sales].[SalesOrderDetail] ([ProductID]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_SalesOrderDetail_rowguid] ON [Sales].[SalesOrderDetail] ([rowguid]) ON [PRIMARY]
GO
ALTER TABLE [Sales].[SalesOrderDetail] ADD CONSTRAINT [FK_SalesOrderDetail_SalesOrderHeader_SalesOrderID] FOREIGN KEY ([SalesOrderID]) REFERENCES [Sales].[SalesOrderHeader] ([SalesOrderID]) ON DELETE CASCADE
GO
ALTER TABLE [Sales].[SalesOrderDetail] ADD CONSTRAINT [FK_SalesOrderDetail_SpecialOfferProduct_SpecialOfferIDProductID] FOREIGN KEY ([SpecialOfferID], [ProductID]) REFERENCES [Sales].[SpecialOfferProduct] ([SpecialOfferID], [ProductID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Individual products associated with a specific sales order. See SalesOrderHeader.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Shipment tracking number supplied by the shipper.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'COLUMN', N'CarrierTrackingNumber'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Per product subtotal. Computed as UnitPrice * (1 - UnitPriceDiscount) * OrderQty.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'COLUMN', N'LineTotal'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Quantity ordered per product.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'COLUMN', N'OrderQty'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Product sold to customer. Foreign key to Product.ProductID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'COLUMN', N'ProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'COLUMN', N'rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key. One incremental unique number per product sold.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'COLUMN', N'SalesOrderDetailID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key. Foreign key to SalesOrderHeader.SalesOrderID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'COLUMN', N'SalesOrderID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Promotional code. Foreign key to SpecialOffer.SpecialOfferID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'COLUMN', N'SpecialOfferID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Selling price of a single product.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'COLUMN', N'UnitPrice'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Discount amount.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'COLUMN', N'UnitPriceDiscount'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [OrderQty] > (0)', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'CONSTRAINT', N'CK_SalesOrderDetail_OrderQty'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [UnitPrice] >= (0.00)', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'CONSTRAINT', N'CK_SalesOrderDetail_UnitPrice'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [UnitPriceDiscount] >= (0.00)', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'CONSTRAINT', N'CK_SalesOrderDetail_UnitPriceDiscount'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'CONSTRAINT', N'DF_SalesOrderDetail_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of NEWID()', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'CONSTRAINT', N'DF_SalesOrderDetail_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 0.0', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'CONSTRAINT', N'DF_SalesOrderDetail_UnitPriceDiscount'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing SalesOrderHeader.PurchaseOrderID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'CONSTRAINT', N'FK_SalesOrderDetail_SalesOrderHeader_SalesOrderID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing SpecialOfferProduct.SpecialOfferIDProductID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'CONSTRAINT', N'FK_SalesOrderDetail_SpecialOfferProduct_SpecialOfferIDProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'CONSTRAINT', N'PK_SalesOrderDetail_SalesOrderID_SalesOrderDetailID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index. Used to support replication samples.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'INDEX', N'AK_SalesOrderDetail_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Nonclustered index.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'INDEX', N'IX_SalesOrderDetail_ProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'INDEX', N'PK_SalesOrderDetail_SalesOrderID_SalesOrderDetailID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'AFTER INSERT, DELETE, UPDATE trigger that inserts a row in the TransactionHistory table, updates ModifiedDate in SalesOrderDetail and updates the SalesOrderHeader.SubTotal column.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderDetail', 'TRIGGER', N'iduSalesOrderDetail'
GO

```


---

## <a name="#uses"></a>Uses

DEPENDENCYLIST* [[Sales].[SalesOrderHeader]](SalesOrderHeader.md)
* [[Sales].[SpecialOfferProduct]](SpecialOfferProduct.md)
* [Sales](../Security/Schemas/Sales.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

