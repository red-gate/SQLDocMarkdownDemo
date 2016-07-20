#### 

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Purchasing.PurchaseOrderHeader

# ![Tables](../../../../Images/Table32.png) [Purchasing].[PurchaseOrderHeader]

---

## <a name="#description"></a>MS_Description

General purchase order information. See PurchaseOrderDetail.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Row Count (~) | 4012 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:55 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Persisted | Computed | Max Length (Bytes) | Allow Nulls | Identity | Default | Description |
|---|---|---|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_PurchaseOrderHeader_PurchaseOrderID: PurchaseOrderID](../../../../Images/pkcluster.png)](#indexes) | PurchaseOrderID | int |  |  | 4 | NO | 1 - 1 |  | _Primary key._ |
|  | RevisionNumber | tinyint |  |  | 1 | NO |  | ((0)) | _Incremental number to track changes to the purchase order over time._ |
| [![Check Constraints CK_PurchaseOrderHeader_Status : ([Status]>=(1) AND [Status]<=(4))](../../../../Images/c-constraint.png)](#checkconstraints) | Status | tinyint |  |  | 1 | NO |  | ((1)) | _Order current status. 1 = Pending; 2 = Approved; 3 = Rejected; 4 = Complete_ |
| [![Indexes IX_PurchaseOrderHeader_EmployeeID](../../../../Images/Index.png)](#indexes)[![Foreign Keys FK_PurchaseOrderHeader_Employee_EmployeeID: [HumanResources].[Employee].EmployeeID](../../../../Images/fk.png)](#foreignkeys) | EmployeeID | int |  |  | 4 | NO |  |  | _Employee who created the purchase order. Foreign key to Employee.BusinessEntityID._ |
| [![Indexes IX_PurchaseOrderHeader_VendorID](../../../../Images/Index.png)](#indexes)[![Foreign Keys FK_PurchaseOrderHeader_Vendor_VendorID: [Purchasing].[Vendor].VendorID](../../../../Images/fk.png)](#foreignkeys) | VendorID | int |  |  | 4 | NO |  |  | _Vendor with whom the purchase order is placed. Foreign key to Vendor.BusinessEntityID._ |
| [![Foreign Keys FK_PurchaseOrderHeader_ShipMethod_ShipMethodID: [Purchasing].[ShipMethod].ShipMethodID](../../../../Images/fk.png)](#foreignkeys) | ShipMethodID | int |  |  | 4 | NO |  |  | _Shipping method. Foreign key to ShipMethod.ShipMethodID._ |
|  | OrderDate | datetime |  |  | 8 | NO |  | (getdate()) | _Purchase order creation date._ |
|  | ShipDate | datetime |  |  | 8 | YES |  |  | _Estimated shipment date from the vendor._ |
| [![Check Constraints CK_PurchaseOrderHeader_SubTotal : ([SubTotal]>=(0.00))](../../../../Images/c-constraint.png)](#checkconstraints) | SubTotal | money |  |  | 8 | NO |  | ((0.00)) | _Purchase order subtotal. Computed as SUM(PurchaseOrderDetail.LineTotal)for the appropriate PurchaseOrderID._ |
| [![Check Constraints CK_PurchaseOrderHeader_TaxAmt : ([TaxAmt]>=(0.00))](../../../../Images/c-constraint.png)](#checkconstraints) | TaxAmt | money |  |  | 8 | NO |  | ((0.00)) | _Tax amount._ |
| [![Check Constraints CK_PurchaseOrderHeader_Freight : ([Freight]>=(0.00))](../../../../Images/c-constraint.png)](#checkconstraints) | Freight | money |  |  | 8 | NO |  | ((0.00)) | _Shipping cost._ |
|  | TotalDue | money | YES | YES | 8 | NO |  |  | _Total due to vendor. Computed as Subtotal + TaxAmt + Freight._ |
|  | ModifiedDate | datetime |  |  | 8 | NO |  | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#computedcolumns"></a>Computed columns

| Name | Column definition |
|---|---|
| TotalDue | (isnull(([SubTotal]+[TaxAmt])+[Freight],(0))) |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_PurchaseOrderHeader_PurchaseOrderID: PurchaseOrderID](../../../../Images/pkcluster.png)](#indexes) | PK_PurchaseOrderHeader_PurchaseOrderID | PurchaseOrderID | YES | _Primary key (clustered) constraint_ |
|  | IX_PurchaseOrderHeader_EmployeeID | EmployeeID |  | _Nonclustered index._ |
|  | IX_PurchaseOrderHeader_VendorID | VendorID |  | _Nonclustered index._ |


---

## <a name="#triggers"></a>Triggers

| Name | ANSI Nulls On | Quoted Identifier On | On | Description |
|---|---|---|---|---|
| uPurchaseOrderHeader | YES | YES | After Update | _AFTER UPDATE trigger that updates the RevisionNumber and ModifiedDate columns in the PurchaseOrderHeader table._ |


---

## <a name="#checkconstraints"></a>Check Constraints

| Name | On Column | Constraint | Description |
|---|---|---|---|
| CK_PurchaseOrderHeader_Freight | Freight | ([Freight]>=(0.00)) | _Check constraint [Freight] >= (0.00)_ |
| CK_PurchaseOrderHeader_ShipDate |  | ([ShipDate]>=[OrderDate] OR [ShipDate] IS NULL) | _Check constraint [ShipDate] >= [OrderDate] OR [ShipDate] IS NULL_ |
| CK_PurchaseOrderHeader_Status | Status | ([Status]>=(1) AND [Status]<=(4)) | _Check constraint [Status] BETWEEN (1) AND (4)_ |
| CK_PurchaseOrderHeader_SubTotal | SubTotal | ([SubTotal]>=(0.00)) | _Check constraint [SubTotal] >= (0.00)_ |
| CK_PurchaseOrderHeader_TaxAmt | TaxAmt | ([TaxAmt]>=(0.00)) | _Check constraint [TaxAmt] >= (0.00)_ |


---

## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_PurchaseOrderHeader_Employee_EmployeeID | EmployeeID->[[HumanResources].[Employee].[BusinessEntityID]](Employee.md) | _Foreign key constraint referencing Employee.EmployeeID._ |
| FK_PurchaseOrderHeader_ShipMethod_ShipMethodID | ShipMethodID->[[Purchasing].[ShipMethod].[ShipMethodID]](ShipMethod.md) | _Foreign key constraint referencing ShipMethod.ShipMethodID._ |
| FK_PurchaseOrderHeader_Vendor_VendorID | VendorID->[[Purchasing].[Vendor].[BusinessEntityID]](Vendor.md) | _Foreign key constraint referencing Vendor.VendorID._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Purchasing].[PurchaseOrderHeader]
(
[PurchaseOrderID] [int] NOT NULL IDENTITY(1, 1),
[RevisionNumber] [tinyint] NOT NULL CONSTRAINT [DF_PurchaseOrderHeader_RevisionNumber] DEFAULT ((0)),
[Status] [tinyint] NOT NULL CONSTRAINT [DF_PurchaseOrderHeader_Status] DEFAULT ((1)),
[EmployeeID] [int] NOT NULL,
[VendorID] [int] NOT NULL,
[ShipMethodID] [int] NOT NULL,
[OrderDate] [datetime] NOT NULL CONSTRAINT [DF_PurchaseOrderHeader_OrderDate] DEFAULT (getdate()),
[ShipDate] [datetime] NULL,
[SubTotal] [money] NOT NULL CONSTRAINT [DF_PurchaseOrderHeader_SubTotal] DEFAULT ((0.00)),
[TaxAmt] [money] NOT NULL CONSTRAINT [DF_PurchaseOrderHeader_TaxAmt] DEFAULT ((0.00)),
[Freight] [money] NOT NULL CONSTRAINT [DF_PurchaseOrderHeader_Freight] DEFAULT ((0.00)),
[TotalDue] AS (isnull(([SubTotal]+[TaxAmt])+[Freight],(0))) PERSISTED NOT NULL,
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_PurchaseOrderHeader_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO

CREATE TRIGGER [Purchasing].[uPurchaseOrderHeader] ON [Purchasing].[PurchaseOrderHeader] 
AFTER UPDATE AS 
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
            UPDATE [Purchasing].[PurchaseOrderHeader]
            SET [Purchasing].[PurchaseOrderHeader].[RevisionNumber] = 
                [Purchasing].[PurchaseOrderHeader].[RevisionNumber] + 1
            WHERE [Purchasing].[PurchaseOrderHeader].[PurchaseOrderID] IN 
                (SELECT inserted.[PurchaseOrderID] FROM inserted);
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
ALTER TABLE [Purchasing].[PurchaseOrderHeader] ADD CONSTRAINT [CK_PurchaseOrderHeader_Freight] CHECK (([Freight]>=(0.00)))
GO
ALTER TABLE [Purchasing].[PurchaseOrderHeader] ADD CONSTRAINT [CK_PurchaseOrderHeader_ShipDate] CHECK (([ShipDate]>=[OrderDate] OR [ShipDate] IS NULL))
GO
ALTER TABLE [Purchasing].[PurchaseOrderHeader] ADD CONSTRAINT [CK_PurchaseOrderHeader_Status] CHECK (([Status]>=(1) AND [Status]<=(4)))
GO
ALTER TABLE [Purchasing].[PurchaseOrderHeader] ADD CONSTRAINT [CK_PurchaseOrderHeader_SubTotal] CHECK (([SubTotal]>=(0.00)))
GO
ALTER TABLE [Purchasing].[PurchaseOrderHeader] ADD CONSTRAINT [CK_PurchaseOrderHeader_TaxAmt] CHECK (([TaxAmt]>=(0.00)))
GO
ALTER TABLE [Purchasing].[PurchaseOrderHeader] ADD CONSTRAINT [PK_PurchaseOrderHeader_PurchaseOrderID] PRIMARY KEY CLUSTERED  ([PurchaseOrderID]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_PurchaseOrderHeader_EmployeeID] ON [Purchasing].[PurchaseOrderHeader] ([EmployeeID]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_PurchaseOrderHeader_VendorID] ON [Purchasing].[PurchaseOrderHeader] ([VendorID]) ON [PRIMARY]
GO
ALTER TABLE [Purchasing].[PurchaseOrderHeader] ADD CONSTRAINT [FK_PurchaseOrderHeader_Employee_EmployeeID] FOREIGN KEY ([EmployeeID]) REFERENCES [HumanResources].[Employee] ([BusinessEntityID])
GO
ALTER TABLE [Purchasing].[PurchaseOrderHeader] ADD CONSTRAINT [FK_PurchaseOrderHeader_ShipMethod_ShipMethodID] FOREIGN KEY ([ShipMethodID]) REFERENCES [Purchasing].[ShipMethod] ([ShipMethodID])
GO
ALTER TABLE [Purchasing].[PurchaseOrderHeader] ADD CONSTRAINT [FK_PurchaseOrderHeader_Vendor_VendorID] FOREIGN KEY ([VendorID]) REFERENCES [Purchasing].[Vendor] ([BusinessEntityID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'General purchase order information. See PurchaseOrderDetail.', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Employee who created the purchase order. Foreign key to Employee.BusinessEntityID.', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'COLUMN', N'EmployeeID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Shipping cost.', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'COLUMN', N'Freight'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Purchase order creation date.', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'COLUMN', N'OrderDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key.', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'COLUMN', N'PurchaseOrderID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Incremental number to track changes to the purchase order over time.', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'COLUMN', N'RevisionNumber'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Estimated shipment date from the vendor.', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'COLUMN', N'ShipDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Shipping method. Foreign key to ShipMethod.ShipMethodID.', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'COLUMN', N'ShipMethodID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Order current status. 1 = Pending; 2 = Approved; 3 = Rejected; 4 = Complete', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'COLUMN', N'Status'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Purchase order subtotal. Computed as SUM(PurchaseOrderDetail.LineTotal)for the appropriate PurchaseOrderID.', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'COLUMN', N'SubTotal'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Tax amount.', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'COLUMN', N'TaxAmt'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Total due to vendor. Computed as Subtotal + TaxAmt + Freight.', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'COLUMN', N'TotalDue'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Vendor with whom the purchase order is placed. Foreign key to Vendor.BusinessEntityID.', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'COLUMN', N'VendorID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [Freight] >= (0.00)', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'CONSTRAINT', N'CK_PurchaseOrderHeader_Freight'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [ShipDate] >= [OrderDate] OR [ShipDate] IS NULL', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'CONSTRAINT', N'CK_PurchaseOrderHeader_ShipDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [Status] BETWEEN (1) AND (4)', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'CONSTRAINT', N'CK_PurchaseOrderHeader_Status'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [SubTotal] >= (0.00)', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'CONSTRAINT', N'CK_PurchaseOrderHeader_SubTotal'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [TaxAmt] >= (0.00)', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'CONSTRAINT', N'CK_PurchaseOrderHeader_TaxAmt'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 0.0', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'CONSTRAINT', N'DF_PurchaseOrderHeader_Freight'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'CONSTRAINT', N'DF_PurchaseOrderHeader_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'CONSTRAINT', N'DF_PurchaseOrderHeader_OrderDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 0', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'CONSTRAINT', N'DF_PurchaseOrderHeader_RevisionNumber'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 1', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'CONSTRAINT', N'DF_PurchaseOrderHeader_Status'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 0.0', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'CONSTRAINT', N'DF_PurchaseOrderHeader_SubTotal'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 0.0', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'CONSTRAINT', N'DF_PurchaseOrderHeader_TaxAmt'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Employee.EmployeeID.', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'CONSTRAINT', N'FK_PurchaseOrderHeader_Employee_EmployeeID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing ShipMethod.ShipMethodID.', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'CONSTRAINT', N'FK_PurchaseOrderHeader_ShipMethod_ShipMethodID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Vendor.VendorID.', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'CONSTRAINT', N'FK_PurchaseOrderHeader_Vendor_VendorID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'CONSTRAINT', N'PK_PurchaseOrderHeader_PurchaseOrderID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Nonclustered index.', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'INDEX', N'IX_PurchaseOrderHeader_EmployeeID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Nonclustered index.', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'INDEX', N'IX_PurchaseOrderHeader_VendorID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'INDEX', N'PK_PurchaseOrderHeader_PurchaseOrderID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'AFTER UPDATE trigger that updates the RevisionNumber and ModifiedDate columns in the PurchaseOrderHeader table.', 'SCHEMA', N'Purchasing', 'TABLE', N'PurchaseOrderHeader', 'TRIGGER', N'uPurchaseOrderHeader'
GO

```


---

## <a name="#uses"></a>Uses

DEPENDENCYLIST* [[HumanResources].[Employee]](Employee.md)
* [[Purchasing].[ShipMethod]](ShipMethod.md)
* [[Purchasing].[Vendor]](Vendor.md)
* [Purchasing](../Security/Schemas/Purchasing.md)


---

## <a name="#usedby"></a>Used By

DEPENDENCYLIST* [[Purchasing].[PurchaseOrderDetail]](PurchaseOrderDetail.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

