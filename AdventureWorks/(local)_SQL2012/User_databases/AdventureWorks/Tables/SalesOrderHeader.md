
# ![Tables](../../../../Images/Table32.png) [Sales].[SalesOrderHeader]

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables_.md) > Sales.SalesOrderHeader

## <a name="#description"></a>MS_Description
General sales order information.
## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 31465 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:55 14 March 2012 |


## <a name="#columns"></a>Columns

| Key | Name | Data Type | Computed | Max Length (Bytes) | Allow Nulls | Identity | Identity Replication | Default | Description |
|---|---|---|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_SalesOrderHeader_SalesOrderID: SalesOrderID](../../../../Images/pkcluster.png)](#indexes) | SalesOrderID | int |  | 4 | NO | 1 - 1 | NO |  | _Primary key._ |
|  | RevisionNumber | tinyint |  | 1 | NO |  |  | ((0)) | _Incremental number to track changes to the sales order over time._ |
|  | OrderDate | datetime |  | 8 | NO |  |  | (getdate()) | _Dates the sales order was created._ |
|  | DueDate | datetime |  | 8 | NO |  |  |  | _Date the order is due to the customer._ |
|  | ShipDate | datetime |  | 8 | YES |  |  |  | _Date the order was shipped to the customer._ |
| [![Check Constraints CK_SalesOrderHeader_Status : ([Status]>=(0) AND [Status]<=(8))](../../../../Images/c-constraint.png)](#checkconstraints) | Status | tinyint |  | 1 | NO |  |  | ((1)) | _Order current status. 1 = In process; 2 = Approved; 3 = Backordered; 4 = Rejected; 5 = Shipped; 6 = Cancelled_ |
|  | OnlineOrderFlag | [[dbo].[Flag]](../Programmability/Types/User-Defined_Data_Types/Flag.md) |  | 1 | NO |  |  | ((1)) | _0 = Order placed by sales person. 1 = Order placed online by customer._ |
| [![Indexes AK_SalesOrderHeader_SalesOrderNumber](../../../../Images/Index.png)](#indexes) | SalesOrderNumber | nvarchar(25) | YES | 50 | NO |  |  |  | _Unique sales order identification number._ |
|  | PurchaseOrderNumber | [[dbo].[OrderNumber]](../Programmability/Types/User-Defined_Data_Types/OrderNumber.md) |  | 50 | YES |  |  |  | _Customer purchase order number reference. _ |
|  | AccountNumber | [[dbo].[AccountNumber]](../Programmability/Types/User-Defined_Data_Types/AccountNumber.md) |  | 30 | YES |  |  |  | _Financial accounting number reference._ |
| [![Indexes IX_SalesOrderHeader_CustomerID](../../../../Images/Index.png)](#indexes)[![Foreign Keys FK_SalesOrderHeader_Customer_CustomerID: [Sales].[Customer].CustomerID](../../../../Images/fk.png)](#foreignkeys) | CustomerID | int |  | 4 | NO |  |  |  | _Customer identification number. Foreign key to Customer.BusinessEntityID._ |
| [![Indexes IX_SalesOrderHeader_SalesPersonID](../../../../Images/Index.png)](#indexes)[![Foreign Keys FK_SalesOrderHeader_SalesPerson_SalesPersonID: [Sales].[SalesPerson].SalesPersonID](../../../../Images/fk.png)](#foreignkeys) | SalesPersonID | int |  | 4 | YES |  |  |  | _Sales person who created the sales order. Foreign key to SalesPerson.BusinessEntityID._ |
| [![Foreign Keys FK_SalesOrderHeader_SalesTerritory_TerritoryID: [Sales].[SalesTerritory].TerritoryID](../../../../Images/fk.png)](#foreignkeys) | TerritoryID | int |  | 4 | YES |  |  |  | _Territory in which the sale was made. Foreign key to SalesTerritory.SalesTerritoryID._ |
| [![Foreign Keys FK_SalesOrderHeader_Address_BillToAddressID: [Person].[Address].BillToAddressID](../../../../Images/fk.png)](#foreignkeys) | BillToAddressID | int |  | 4 | NO |  |  |  | _Customer billing address. Foreign key to Address.AddressID._ |
| [![Foreign Keys FK_SalesOrderHeader_Address_ShipToAddressID: [Person].[Address].ShipToAddressID](../../../../Images/fk.png)](#foreignkeys) | ShipToAddressID | int |  | 4 | NO |  |  |  | _Customer shipping address. Foreign key to Address.AddressID._ |
| [![Foreign Keys FK_SalesOrderHeader_ShipMethod_ShipMethodID: [Purchasing].[ShipMethod].ShipMethodID](../../../../Images/fk.png)](#foreignkeys) | ShipMethodID | int |  | 4 | NO |  |  |  | _Shipping method. Foreign key to ShipMethod.ShipMethodID._ |
| [![Foreign Keys FK_SalesOrderHeader_CreditCard_CreditCardID: [Sales].[CreditCard].CreditCardID](../../../../Images/fk.png)](#foreignkeys) | CreditCardID | int |  | 4 | YES |  |  |  | _Credit card identification number. Foreign key to CreditCard.CreditCardID._ |
|  | CreditCardApprovalCode | varchar(15) |  | 15 | YES |  |  |  | _Approval code provided by the credit card company._ |
| [![Foreign Keys FK_SalesOrderHeader_CurrencyRate_CurrencyRateID: [Sales].[CurrencyRate].CurrencyRateID](../../../../Images/fk.png)](#foreignkeys) | CurrencyRateID | int |  | 4 | YES |  |  |  | _Currency exchange rate used. Foreign key to CurrencyRate.CurrencyRateID._ |
| [![Check Constraints CK_SalesOrderHeader_SubTotal : ([SubTotal]>=(0.00))](../../../../Images/c-constraint.png)](#checkconstraints) | SubTotal | money |  | 8 | NO |  |  | ((0.00)) | _Sales subtotal. Computed as SUM(SalesOrderDetail.LineTotal)for the appropriate SalesOrderID._ |
| [![Check Constraints CK_SalesOrderHeader_TaxAmt : ([TaxAmt]>=(0.00))](../../../../Images/c-constraint.png)](#checkconstraints) | TaxAmt | money |  | 8 | NO |  |  | ((0.00)) | _Tax amount._ |
| [![Check Constraints CK_SalesOrderHeader_Freight : ([Freight]>=(0.00))](../../../../Images/c-constraint.png)](#checkconstraints) | Freight | money |  | 8 | NO |  |  | ((0.00)) | _Shipping cost._ |
|  | TotalDue | money | YES | 8 | NO |  |  |  | _Total due from customer. Computed as Subtotal + TaxAmt + Freight._ |
|  | Comment | nvarchar(128) |  | 256 | YES |  |  |  | _Sales representative comments._ |
| [![Indexes AK_SalesOrderHeader_rowguid](../../../../Images/Index.png)](#indexes) | rowguid | uniqueidentifier |  | 16 | NO |  |  | (newid()) | _ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample._ |
|  | ModifiedDate | datetime |  | 8 | NO |  |  | (getdate()) | _Date and time the record was last updated._ |


## <a name="#computedcolumns"></a>Computed columns

| Name | Column definition |
|---|---|
| SalesOrderNumber | (isnull(N'SO'+CONVERT([nvarchar](23),[SalesOrderID],(0)),N'*** ERROR ***')) |
| TotalDue | (isnull(([SubTotal]+[TaxAmt])+[Freight],(0))) |


## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_SalesOrderHeader_SalesOrderID: SalesOrderID](../../../../Images/pkcluster.png)](#indexes) | PK_SalesOrderHeader_SalesOrderID | SalesOrderID | YES | _Primary key (clustered) constraint_ |
|  | AK_SalesOrderHeader_SalesOrderNumber | SalesOrderNumber | YES | _Unique nonclustered index._ |
|  | AK_SalesOrderHeader_rowguid | rowguid | YES | _Unique nonclustered index. Used to support replication samples._ |
|  | IX_SalesOrderHeader_CustomerID | CustomerID |  | _Nonclustered index._ |
|  | IX_SalesOrderHeader_SalesPersonID | SalesPersonID |  | _Nonclustered index._ |


## <a name="#triggers"></a>Triggers

| Name | ANSI Nulls On | Quoted Identifier On | On | Not For Replication | Description |
|---|---|---|---|---|---|
| uSalesOrderHeader | YES | YES | After Update | YES | _AFTER UPDATE trigger that updates the RevisionNumber and ModifiedDate columns in the SalesOrderHeader table.Updates the SalesYTD column in the SalesPerson and SalesTerritory tables._ |


## <a name="#checkconstraints"></a>Check Constraints

| Name | On Column | Constraint | Description |
|---|---|---|---|
| CK_SalesOrderHeader_DueDate |  | ([DueDate]>=[OrderDate]) | _Check constraint [DueDate] >= [OrderDate]_ |
| CK_SalesOrderHeader_Freight | Freight | ([Freight]>=(0.00)) | _Check constraint [Freight] >= (0.00)_ |
| CK_SalesOrderHeader_ShipDate |  | ([ShipDate]>=[OrderDate] OR [ShipDate] IS NULL) | _Check constraint [ShipDate] >= [OrderDate] OR [ShipDate] IS NULL_ |
| CK_SalesOrderHeader_Status | Status | ([Status]>=(0) AND [Status]<=(8)) | _Check constraint [Status] BETWEEN (0) AND (8)_ |
| CK_SalesOrderHeader_SubTotal | SubTotal | ([SubTotal]>=(0.00)) | _Check constraint [SubTotal] >= (0.00)_ |
| CK_SalesOrderHeader_TaxAmt | TaxAmt | ([TaxAmt]>=(0.00)) | _Check constraint [TaxAmt] >= (0.00)_ |


## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_SalesOrderHeader_Address_BillToAddressID | BillToAddressID->[[Person].[Address].[AddressID]](Address.md) | _Foreign key constraint referencing Address.AddressID._ |
| FK_SalesOrderHeader_Address_ShipToAddressID | ShipToAddressID->[[Person].[Address].[AddressID]](Address.md) | _Foreign key constraint referencing Address.AddressID._ |
| FK_SalesOrderHeader_CreditCard_CreditCardID | CreditCardID->[[Sales].[CreditCard].[CreditCardID]](CreditCard.md) | _Foreign key constraint referencing CreditCard.CreditCardID._ |
| FK_SalesOrderHeader_CurrencyRate_CurrencyRateID | CurrencyRateID->[[Sales].[CurrencyRate].[CurrencyRateID]](CurrencyRate.md) | _Foreign key constraint referencing CurrencyRate.CurrencyRateID._ |
| FK_SalesOrderHeader_Customer_CustomerID | CustomerID->[[Sales].[Customer].[CustomerID]](Customer.md) | _Foreign key constraint referencing Customer.CustomerID._ |
| FK_SalesOrderHeader_SalesPerson_SalesPersonID | SalesPersonID->[[Sales].[SalesPerson].[BusinessEntityID]](SalesPerson.md) | _Foreign key constraint referencing SalesPerson.SalesPersonID._ |
| FK_SalesOrderHeader_SalesTerritory_TerritoryID | TerritoryID->[[Sales].[SalesTerritory].[TerritoryID]](SalesTerritory.md) | _Foreign key constraint referencing SalesTerritory.TerritoryID._ |
| FK_SalesOrderHeader_ShipMethod_ShipMethodID | ShipMethodID->[[Purchasing].[ShipMethod].[ShipMethodID]](ShipMethod.md) | _Foreign key constraint referencing ShipMethod.ShipMethodID._ |


## <a name="#sqlscript"></a>SQL Script
```sql
CREATE TABLE [Sales].[SalesOrderHeader]
(
[SalesOrderID] [int] NOT NULL IDENTITY(1, 1) NOT FOR REPLICATION,
[RevisionNumber] [tinyint] NOT NULL CONSTRAINT [DF_SalesOrderHeader_RevisionNumber] DEFAULT ((0)),
[OrderDate] [datetime] NOT NULL CONSTRAINT [DF_SalesOrderHeader_OrderDate] DEFAULT (getdate()),
[DueDate] [datetime] NOT NULL,
[ShipDate] [datetime] NULL,
[Status] [tinyint] NOT NULL CONSTRAINT [DF_SalesOrderHeader_Status] DEFAULT ((1)),
[OnlineOrderFlag] [dbo].[Flag] NOT NULL CONSTRAINT [DF_SalesOrderHeader_OnlineOrderFlag] DEFAULT ((1)),
[SalesOrderNumber] AS (isnull(N'SO'+CONVERT([nvarchar](23),[SalesOrderID],(0)),N'*** ERROR ***')),
[PurchaseOrderNumber] [dbo].[OrderNumber] NULL,
[AccountNumber] [dbo].[AccountNumber] NULL,
[CustomerID] [int] NOT NULL,
[SalesPersonID] [int] NULL,
[TerritoryID] [int] NULL,
[BillToAddressID] [int] NOT NULL,
[ShipToAddressID] [int] NOT NULL,
[ShipMethodID] [int] NOT NULL,
[CreditCardID] [int] NULL,
[CreditCardApprovalCode] [varchar] (15) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
[CurrencyRateID] [int] NULL,
[SubTotal] [money] NOT NULL CONSTRAINT [DF_SalesOrderHeader_SubTotal] DEFAULT ((0.00)),
[TaxAmt] [money] NOT NULL CONSTRAINT [DF_SalesOrderHeader_TaxAmt] DEFAULT ((0.00)),
[Freight] [money] NOT NULL CONSTRAINT [DF_SalesOrderHeader_Freight] DEFAULT ((0.00)),
[TotalDue] AS (isnull(([SubTotal]+[TaxAmt])+[Freight],(0))),
[Comment] [nvarchar] (128) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
[rowguid] [uniqueidentifier] NOT NULL ROWGUIDCOL CONSTRAINT [DF_SalesOrderHeader_rowguid] DEFAULT (newid()),
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_SalesOrderHeader_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO

CREATE TRIGGER [Sales].[uSalesOrderHeader] ON [Sales].[SalesOrderHeader] 
AFTER UPDATE NOT FOR REPLICATION AS 
BEGIN
    DECLARE @Count int;

    SET @Count = @@ROWCOUNT;
    IF @Count = 0 
        RETURN;

    SET NOCOUNT ON;

    BEGIN TRY
        -- Update RevisionNumber for modification of any field EXCEPT the Status.
        IF NOT UPDATE([Status])
        BEGIN
            UPDATE [Sales].[SalesOrderHeader]
            SET [Sales].[SalesOrderHeader].[RevisionNumber] = 
                [Sales].[SalesOrderHeader].[RevisionNumber] + 1
            WHERE [Sales].[SalesOrderHeader].[SalesOrderID] IN 
                (SELECT inserted.[SalesOrderID] FROM inserted);
        END;

        -- Update the SalesPerson SalesYTD when SubTotal is updated
        IF UPDATE([SubTotal])
        BEGIN
            DECLARE @StartDate datetime,
                    @EndDate datetime

            SET @StartDate = [dbo].[ufnGetAccountingStartDate]();
            SET @EndDate = [dbo].[ufnGetAccountingEndDate]();

            UPDATE [Sales].[SalesPerson]
            SET [Sales].[SalesPerson].[SalesYTD] = 
                (SELECT SUM([Sales].[SalesOrderHeader].[SubTotal])
                FROM [Sales].[SalesOrderHeader] 
                WHERE [Sales].[SalesPerson].[BusinessEntityID] = [Sales].[SalesOrderHeader].[SalesPersonID]
                    AND ([Sales].[SalesOrderHeader].[Status] = 5) -- Shipped
                    AND [Sales].[SalesOrderHeader].[OrderDate] BETWEEN @StartDate AND @EndDate)
            WHERE [Sales].[SalesPerson].[BusinessEntityID] 
                IN (SELECT DISTINCT inserted.[SalesPersonID] FROM inserted 
                    WHERE inserted.[OrderDate] BETWEEN @StartDate AND @EndDate);

            -- Update the SalesTerritory SalesYTD when SubTotal is updated
            UPDATE [Sales].[SalesTerritory]
            SET [Sales].[SalesTerritory].[SalesYTD] = 
                (SELECT SUM([Sales].[SalesOrderHeader].[SubTotal])
                FROM [Sales].[SalesOrderHeader] 
                WHERE [Sales].[SalesTerritory].[TerritoryID] = [Sales].[SalesOrderHeader].[TerritoryID]
                    AND ([Sales].[SalesOrderHeader].[Status] = 5) -- Shipped
                    AND [Sales].[SalesOrderHeader].[OrderDate] BETWEEN @StartDate AND @EndDate)
            WHERE [Sales].[SalesTerritory].[TerritoryID] 
                IN (SELECT DISTINCT inserted.[TerritoryID] FROM inserted 
                    WHERE inserted.[OrderDate] BETWEEN @StartDate AND @EndDate);
        END;
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
ALTER TABLE [Sales].[SalesOrderHeader] ADD CONSTRAINT [CK_SalesOrderHeader_DueDate] CHECK (([DueDate]>=[OrderDate]))
GO
ALTER TABLE [Sales].[SalesOrderHeader] ADD CONSTRAINT [CK_SalesOrderHeader_Freight] CHECK (([Freight]>=(0.00)))
GO
ALTER TABLE [Sales].[SalesOrderHeader] ADD CONSTRAINT [CK_SalesOrderHeader_ShipDate] CHECK (([ShipDate]>=[OrderDate] OR [ShipDate] IS NULL))
GO
ALTER TABLE [Sales].[SalesOrderHeader] ADD CONSTRAINT [CK_SalesOrderHeader_Status] CHECK (([Status]>=(0) AND [Status]<=(8)))
GO
ALTER TABLE [Sales].[SalesOrderHeader] ADD CONSTRAINT [CK_SalesOrderHeader_SubTotal] CHECK (([SubTotal]>=(0.00)))
GO
ALTER TABLE [Sales].[SalesOrderHeader] ADD CONSTRAINT [CK_SalesOrderHeader_TaxAmt] CHECK (([TaxAmt]>=(0.00)))
GO
ALTER TABLE [Sales].[SalesOrderHeader] ADD CONSTRAINT [PK_SalesOrderHeader_SalesOrderID] PRIMARY KEY CLUSTERED  ([SalesOrderID]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_SalesOrderHeader_CustomerID] ON [Sales].[SalesOrderHeader] ([CustomerID]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_SalesOrderHeader_rowguid] ON [Sales].[SalesOrderHeader] ([rowguid]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_SalesOrderHeader_SalesOrderNumber] ON [Sales].[SalesOrderHeader] ([SalesOrderNumber]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_SalesOrderHeader_SalesPersonID] ON [Sales].[SalesOrderHeader] ([SalesPersonID]) ON [PRIMARY]
GO
ALTER TABLE [Sales].[SalesOrderHeader] ADD CONSTRAINT [FK_SalesOrderHeader_Address_BillToAddressID] FOREIGN KEY ([BillToAddressID]) REFERENCES [Person].[Address] ([AddressID])
GO
ALTER TABLE [Sales].[SalesOrderHeader] ADD CONSTRAINT [FK_SalesOrderHeader_Address_ShipToAddressID] FOREIGN KEY ([ShipToAddressID]) REFERENCES [Person].[Address] ([AddressID])
GO
ALTER TABLE [Sales].[SalesOrderHeader] ADD CONSTRAINT [FK_SalesOrderHeader_CreditCard_CreditCardID] FOREIGN KEY ([CreditCardID]) REFERENCES [Sales].[CreditCard] ([CreditCardID])
GO
ALTER TABLE [Sales].[SalesOrderHeader] ADD CONSTRAINT [FK_SalesOrderHeader_CurrencyRate_CurrencyRateID] FOREIGN KEY ([CurrencyRateID]) REFERENCES [Sales].[CurrencyRate] ([CurrencyRateID])
GO
ALTER TABLE [Sales].[SalesOrderHeader] ADD CONSTRAINT [FK_SalesOrderHeader_Customer_CustomerID] FOREIGN KEY ([CustomerID]) REFERENCES [Sales].[Customer] ([CustomerID])
GO
ALTER TABLE [Sales].[SalesOrderHeader] ADD CONSTRAINT [FK_SalesOrderHeader_SalesPerson_SalesPersonID] FOREIGN KEY ([SalesPersonID]) REFERENCES [Sales].[SalesPerson] ([BusinessEntityID])
GO
ALTER TABLE [Sales].[SalesOrderHeader] ADD CONSTRAINT [FK_SalesOrderHeader_SalesTerritory_TerritoryID] FOREIGN KEY ([TerritoryID]) REFERENCES [Sales].[SalesTerritory] ([TerritoryID])
GO
ALTER TABLE [Sales].[SalesOrderHeader] ADD CONSTRAINT [FK_SalesOrderHeader_ShipMethod_ShipMethodID] FOREIGN KEY ([ShipMethodID]) REFERENCES [Purchasing].[ShipMethod] ([ShipMethodID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'General sales order information.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Financial accounting number reference.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'AccountNumber'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Customer billing address. Foreign key to Address.AddressID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'BillToAddressID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Sales representative comments.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'Comment'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Approval code provided by the credit card company.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'CreditCardApprovalCode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Credit card identification number. Foreign key to CreditCard.CreditCardID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'CreditCardID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Currency exchange rate used. Foreign key to CurrencyRate.CurrencyRateID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'CurrencyRateID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Customer identification number. Foreign key to Customer.BusinessEntityID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'CustomerID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date the order is due to the customer.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'DueDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Shipping cost.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'Freight'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'0 = Order placed by sales person. 1 = Order placed online by customer.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'OnlineOrderFlag'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Dates the sales order was created.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'OrderDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Customer purchase order number reference. ', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'PurchaseOrderNumber'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Incremental number to track changes to the sales order over time.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'RevisionNumber'
GO
EXEC sp_addextendedproperty N'MS_Description', N'ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'SalesOrderID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique sales order identification number.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'SalesOrderNumber'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Sales person who created the sales order. Foreign key to SalesPerson.BusinessEntityID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'SalesPersonID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date the order was shipped to the customer.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'ShipDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Shipping method. Foreign key to ShipMethod.ShipMethodID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'ShipMethodID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Customer shipping address. Foreign key to Address.AddressID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'ShipToAddressID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Order current status. 1 = In process; 2 = Approved; 3 = Backordered; 4 = Rejected; 5 = Shipped; 6 = Cancelled', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'Status'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Sales subtotal. Computed as SUM(SalesOrderDetail.LineTotal)for the appropriate SalesOrderID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'SubTotal'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Tax amount.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'TaxAmt'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Territory in which the sale was made. Foreign key to SalesTerritory.SalesTerritoryID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'TerritoryID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Total due from customer. Computed as Subtotal + TaxAmt + Freight.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'COLUMN', N'TotalDue'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [DueDate] >= [OrderDate]', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'CK_SalesOrderHeader_DueDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [Freight] >= (0.00)', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'CK_SalesOrderHeader_Freight'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [ShipDate] >= [OrderDate] OR [ShipDate] IS NULL', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'CK_SalesOrderHeader_ShipDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [Status] BETWEEN (0) AND (8)', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'CK_SalesOrderHeader_Status'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [SubTotal] >= (0.00)', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'CK_SalesOrderHeader_SubTotal'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [TaxAmt] >= (0.00)', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'CK_SalesOrderHeader_TaxAmt'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 0.0', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'DF_SalesOrderHeader_Freight'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'DF_SalesOrderHeader_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 1 (TRUE)', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'DF_SalesOrderHeader_OnlineOrderFlag'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'DF_SalesOrderHeader_OrderDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 0', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'DF_SalesOrderHeader_RevisionNumber'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of NEWID()', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'DF_SalesOrderHeader_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 1', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'DF_SalesOrderHeader_Status'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 0.0', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'DF_SalesOrderHeader_SubTotal'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 0.0', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'DF_SalesOrderHeader_TaxAmt'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Address.AddressID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'FK_SalesOrderHeader_Address_BillToAddressID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Address.AddressID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'FK_SalesOrderHeader_Address_ShipToAddressID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing CreditCard.CreditCardID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'FK_SalesOrderHeader_CreditCard_CreditCardID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing CurrencyRate.CurrencyRateID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'FK_SalesOrderHeader_CurrencyRate_CurrencyRateID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Customer.CustomerID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'FK_SalesOrderHeader_Customer_CustomerID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing SalesPerson.SalesPersonID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'FK_SalesOrderHeader_SalesPerson_SalesPersonID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing SalesTerritory.TerritoryID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'FK_SalesOrderHeader_SalesTerritory_TerritoryID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing ShipMethod.ShipMethodID.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'FK_SalesOrderHeader_ShipMethod_ShipMethodID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'CONSTRAINT', N'PK_SalesOrderHeader_SalesOrderID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index. Used to support replication samples.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'INDEX', N'AK_SalesOrderHeader_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'INDEX', N'AK_SalesOrderHeader_SalesOrderNumber'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Nonclustered index.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'INDEX', N'IX_SalesOrderHeader_CustomerID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Nonclustered index.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'INDEX', N'IX_SalesOrderHeader_SalesPersonID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'INDEX', N'PK_SalesOrderHeader_SalesOrderID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'AFTER UPDATE trigger that updates the RevisionNumber and ModifiedDate columns in the SalesOrderHeader table.Updates the SalesYTD column in the SalesPerson and SalesTerritory tables.', 'SCHEMA', N'Sales', 'TABLE', N'SalesOrderHeader', 'TRIGGER', N'uSalesOrderHeader'
GO

```

## <a name="#uses"></a>Uses
DEPENDENCYLIST
* [[Person].[Address]](Address.md)
* [[Purchasing].[ShipMethod]](ShipMethod.md)
* [[Sales].[CreditCard]](CreditCard.md)
* [[Sales].[CurrencyRate]](CurrencyRate.md)
* [[Sales].[Customer]](Customer.md)
* [[Sales].[SalesPerson]](SalesPerson.md)
* [[Sales].[SalesTerritory]](SalesTerritory.md)
* [[dbo].[AccountNumber]](../Programmability/Types/User-Defined_Data_Types/AccountNumber.md)
* [[dbo].[Flag]](../Programmability/Types/User-Defined_Data_Types/Flag.md)
* [[dbo].[OrderNumber]](../Programmability/Types/User-Defined_Data_Types/OrderNumber.md)
* [Sales](../Security/Schemas/Sales.md)


## <a name="#usedby"></a>Used By
DEPENDENCYLIST
* [[Sales].[SalesOrderDetail]](SalesOrderDetail.md)
* [[Sales].[SalesOrderHeaderSalesReason]](SalesOrderHeaderSalesReason.md)
* [[Sales].[vSalesPersonSalesByFiscalYears]](../Views/vSalesPersonSalesByFiscalYears.md)

FOOTER: FOOTER: Author:  Chris Whitworth
FOOTER: Created: 19 July 2016 09:34
FOOTER: Copyright 2016 - All Rights Reserved

