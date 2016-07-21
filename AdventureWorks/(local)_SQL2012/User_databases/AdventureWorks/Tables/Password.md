#### asdasdasd

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Person.Password

# ![Tables](../../../../Images/Table32.png) [Person].[Password]

---

## <a name="#description"></a>MS_Description

One way hashed authentication information

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Row Count (~) | 19972 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:54 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Default | Description |
|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_Password_BusinessEntityID: BusinessEntityID](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_Password_Person_BusinessEntityID: [Person].[Person].BusinessEntityID](../../../../Images/fk.png)](#foreignkeys) | BusinessEntityID | int | 4 | NO |  |  |
|  | PasswordHash | varchar(128) | 128 | NO |  | _Password for the e-mail account._ |
|  | PasswordSalt | varchar(10) | 10 | NO |  | _Random value concatenated with the password string before the password is hashed._ |
|  | rowguid | uniqueidentifier | 16 | NO | (newid()) | _ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample._ |
|  | ModifiedDate | datetime | 8 | NO | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_Password_BusinessEntityID: BusinessEntityID](../../../../Images/pkcluster.png)](#indexes) | PK_Password_BusinessEntityID | BusinessEntityID | YES | _Primary key (clustered) constraint_ |


---

## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_Password_Person_BusinessEntityID | BusinessEntityID->[[Person].[Person].[BusinessEntityID]](Person.md) | _Foreign key constraint referencing Person.BusinessEntityID._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Person].[Password]
(
[BusinessEntityID] [int] NOT NULL,
[PasswordHash] [varchar] (128) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[PasswordSalt] [varchar] (10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[rowguid] [uniqueidentifier] NOT NULL ROWGUIDCOL CONSTRAINT [DF_Password_rowguid] DEFAULT (newid()),
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_Password_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Person].[Password] ADD CONSTRAINT [PK_Password_BusinessEntityID] PRIMARY KEY CLUSTERED  ([BusinessEntityID]) ON [PRIMARY]
GO
ALTER TABLE [Person].[Password] ADD CONSTRAINT [FK_Password_Person_BusinessEntityID] FOREIGN KEY ([BusinessEntityID]) REFERENCES [Person].[Person] ([BusinessEntityID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'One way hashed authentication information', 'SCHEMA', N'Person', 'TABLE', N'Password', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Person', 'TABLE', N'Password', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Password for the e-mail account.', 'SCHEMA', N'Person', 'TABLE', N'Password', 'COLUMN', N'PasswordHash'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Random value concatenated with the password string before the password is hashed.', 'SCHEMA', N'Person', 'TABLE', N'Password', 'COLUMN', N'PasswordSalt'
GO
EXEC sp_addextendedproperty N'MS_Description', N'ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample.', 'SCHEMA', N'Person', 'TABLE', N'Password', 'COLUMN', N'rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Person', 'TABLE', N'Password', 'CONSTRAINT', N'DF_Password_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of NEWID()', 'SCHEMA', N'Person', 'TABLE', N'Password', 'CONSTRAINT', N'DF_Password_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Person.BusinessEntityID.', 'SCHEMA', N'Person', 'TABLE', N'Password', 'CONSTRAINT', N'FK_Password_Person_BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Person', 'TABLE', N'Password', 'CONSTRAINT', N'PK_Password_BusinessEntityID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Person', 'TABLE', N'Password', 'INDEX', N'PK_Password_BusinessEntityID'
GO

```


---

## <a name="#uses"></a>Uses

* [[Person].[Person]](Person.md)
* [Person](../Security/Schemas/Person.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 14:15

