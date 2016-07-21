#### asdasdasd

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Purchasing.Vendor

# ![Tables](../../../../Images/Table32.png) [Purchasing].[Vendor]

---

## <a name="#description"></a>MS_Description

Companies from whom Adventure Works Cycles purchases parts or other goods.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 104 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:55 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Default | Description |
|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_Vendor_BusinessEntityID: BusinessEntityID](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_Vendor_BusinessEntity_BusinessEntityID: [Person].[BusinessEntity].BusinessEntityID](../../../../Images/fk.png)](#foreignkeys) | BusinessEntityID | int | 4 | NO |  | _Primary key for Vendor records.  Foreign key to BusinessEntity.BusinessEntityID_ |
| [![Indexes AK_Vendor_AccountNumber](../../../../Images/Index.png)](#indexes) | AccountNumber | [[dbo].[AccountNumber]](../Programmability/Types/User-Defined_Data_Types/AccountNumber.md) | 30 | NO |  | _Vendor account (identification) number._ |
|  | Name | [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md) | 100 | NO |  | _Company name._ |
| [![Check Constraints CK_Vendor_CreditRating : ([CreditRating]>=(1) AND [CreditRating]<=(5))](../../../../Images/c-constraint.png)](#checkconstraints) | CreditRating | tinyint | 1 | NO |  | _1 = Superior, 2 = Excellent, 3 = Above average, 4 = Average, 5 = Below average_ |
|  | PreferredVendorStatus | [[dbo].[Flag]](../Programmability/Types/User-Defined_Data_Types/Flag.md) | 1 | NO | ((1)) | _0 = Do not use if another vendor is available. 1 = Preferred over other vendors supplying the same product._ |
|  | ActiveFlag | [[dbo].[Flag]](../Programmability/Types/User-Defined_Data_Types/Flag.md) | 1 | NO | ((1)) | _0 = Vendor no longer used. 1 = Vendor is actively used._ |
|  | PurchasingWebServiceURL | nvarchar(1024) | 2048 | YES |  | _Vendor URL._ |
|  | ModifiedDate | datetime | 8 | NO | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_Vendor_BusinessEntityID: BusinessEntityID](../../../../Images/pkcluster.png)](#indexes) | PK_Vendor_BusinessEntityID | BusinessEntityID | YES | _Primary key (clustered) constraint_ |
|  | AK_Vendor_AccountNumber | AccountNumber | YES | _Unique nonclustered index._ |


---

## <a name="#triggers"></a>Triggers

| Name | ANSI Nulls On | Quoted Identifier On | On | Not For Replication | Description |
|---|---|---|---|---|---|
| dVendor | YES | YES | Instead Of Delete | YES | _INSTEAD OF DELETE trigger which keeps Vendors from being deleted._ |


---

## <a name="#checkconstraints"></a>Check Constraints

| Name | On Column | Constraint | Description |
|---|---|---|---|
| CK_Vendor_CreditRating | CreditRating | ([CreditRating]>=(1) AND [CreditRating]<=(5)) | _Check constraint [CreditRating] BETWEEN (1) AND (5)_ |


---

## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_Vendor_BusinessEntity_BusinessEntityID | BusinessEntityID->[[Person].[BusinessEntity].[BusinessEntityID]](BusinessEntity.md) | _Foreign key constraint referencing BusinessEntity.BusinessEntityID_ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Purchasing].[Vendor]
(
[BusinessEntityID] [int] NOT NULL,
[AccountNumber] [dbo].[AccountNumber] NOT NULL,
[Name] [dbo].[Name] NOT NULL,
[CreditRating] [tinyint] NOT NULL,
[PreferredVendorStatus] [dbo].[Flag] NOT NULL CONSTRAINT [DF_Vendor_PreferredVendorStatus] DEFAULT ((1)),
[ActiveFlag] [dbo].[Flag] NOT NULL CONSTRAINT [DF_Vendor_ActiveFlag] DEFAULT ((1)),
[PurchasingWebServiceURL] [nvarchar] (1024) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_Vendor_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO

CREATE TRIGGER [Purchasing].[dVendor] ON [Purchasing].[Vendor] 
INSTEAD OF DELETE NOT FOR REPLICATION AS 
BEGIN
    DECLARE @Count int;

    SET @Count = @@ROWCOUNT;
    IF @Count = 0 
        RETURN;

    SET NOCOUNT ON;

    BEGIN TRY
        DECLARE @DeleteCount int;

        SELECT @DeleteCount = COUNT(*) FROM deleted;
        IF @DeleteCount > 0 
        BEGIN
            RAISERROR
                (N'Vendors cannot be deleted. They can only be marked as not active.', -- Message
                10, -- Severity.
                1); -- State.

        -- Rollback any active or uncommittable transactions
            IF @@TRANCOUNT > 0
            BEGIN
                ROLLBACK TRANSACTION;
            END
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
ALTER TABLE [Purchasing].[Vendor] ADD CONSTRAINT [CK_Vendor_CreditRating] CHECK (([CreditRating]>=(1) AND [CreditRating]<=(5)))
GO
ALTER TABLE [Purchasing].[Vendor] ADD CONSTRAINT [PK_Vendor_BusinessEntityID] PRIMARY KEY CLUSTERED  ([BusinessEntityID]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_Vendor_AccountNumber] ON [Purchasing].[Vendor] ([AccountNumber]) ON [PRIMARY]
GO
ALTER TABLE [Purchasing].[Vendor] ADD CONSTRAINT [FK_Vendor_BusinessEntity_BusinessEntityID] FOREIGN KEY ([BusinessEntityID]) REFERENCES [Person].[BusinessEntity] ([BusinessEntityID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Companies from whom Adventure Works Cycles purchases parts or other goods.', 'SCHEMA', N'Purchasing', 'TABLE', N'Vendor', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Vendor account (identification) number.', 'SCHEMA', N'Purchasing', 'TABLE', N'Vendor', 'COLUMN', N'AccountNumber'
GO
EXEC sp_addextendedproperty N'MS_Description', N'0 = Vendor no longer used. 1 = Vendor is actively used.', 'SCHEMA', N'Purchasing', 'TABLE', N'Vendor', 'COLUMN', N'ActiveFlag'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key for Vendor records.  Foreign key to BusinessEntity.BusinessEntityID', 'SCHEMA', N'Purchasing', 'TABLE', N'Vendor', 'COLUMN', N'BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'1 = Superior, 2 = Excellent, 3 = Above average, 4 = Average, 5 = Below average', 'SCHEMA', N'Purchasing', 'TABLE', N'Vendor', 'COLUMN', N'CreditRating'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Purchasing', 'TABLE', N'Vendor', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Company name.', 'SCHEMA', N'Purchasing', 'TABLE', N'Vendor', 'COLUMN', N'Name'
GO
EXEC sp_addextendedproperty N'MS_Description', N'0 = Do not use if another vendor is available. 1 = Preferred over other vendors supplying the same product.', 'SCHEMA', N'Purchasing', 'TABLE', N'Vendor', 'COLUMN', N'PreferredVendorStatus'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Vendor URL.', 'SCHEMA', N'Purchasing', 'TABLE', N'Vendor', 'COLUMN', N'PurchasingWebServiceURL'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [CreditRating] BETWEEN (1) AND (5)', 'SCHEMA', N'Purchasing', 'TABLE', N'Vendor', 'CONSTRAINT', N'CK_Vendor_CreditRating'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 1 (TRUE)', 'SCHEMA', N'Purchasing', 'TABLE', N'Vendor', 'CONSTRAINT', N'DF_Vendor_ActiveFlag'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Purchasing', 'TABLE', N'Vendor', 'CONSTRAINT', N'DF_Vendor_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 1 (TRUE)', 'SCHEMA', N'Purchasing', 'TABLE', N'Vendor', 'CONSTRAINT', N'DF_Vendor_PreferredVendorStatus'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing BusinessEntity.BusinessEntityID', 'SCHEMA', N'Purchasing', 'TABLE', N'Vendor', 'CONSTRAINT', N'FK_Vendor_BusinessEntity_BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Purchasing', 'TABLE', N'Vendor', 'CONSTRAINT', N'PK_Vendor_BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index.', 'SCHEMA', N'Purchasing', 'TABLE', N'Vendor', 'INDEX', N'AK_Vendor_AccountNumber'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Purchasing', 'TABLE', N'Vendor', 'INDEX', N'PK_Vendor_BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'INSTEAD OF DELETE trigger which keeps Vendors from being deleted.', 'SCHEMA', N'Purchasing', 'TABLE', N'Vendor', 'TRIGGER', N'dVendor'
GO

```


---

## <a name="#uses"></a>Uses

* [[Person].[BusinessEntity]](BusinessEntity.md)
* [[dbo].[AccountNumber]](../Programmability/Types/User-Defined_Data_Types/AccountNumber.md)
* [[dbo].[Flag]](../Programmability/Types/User-Defined_Data_Types/Flag.md)
* [[dbo].[Name]](../Programmability/Types/User-Defined_Data_Types/Name.md)
* [Purchasing](../Security/Schemas/Purchasing.md)


---

## <a name="#usedby"></a>Used By

* [[Purchasing].[ProductVendor]](ProductVendor.md)
* [[Purchasing].[PurchaseOrderHeader]](PurchaseOrderHeader.md)
* [[Purchasing].[vVendorWithAddresses]](../Views/vVendorWithAddresses.md)
* [[Purchasing].[vVendorWithContacts]](../Views/vVendorWithContacts.md)
* [[dbo].[ufnGetContactInformation]](../Programmability/Functions/Table-valued_Functions/ufnGetContactInformation.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 14:15

