#### 

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Production.Document

# ![Tables](../../../../Images/Table32.png) [Production].[Document]

---

## <a name="#description"></a>MS_Description

Product maintenance documents.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Collation | SQL_Latin1_General_CP1_CI_AS |
| Full Text Catalog | [AW2008FullTextCatalog](../Storage/Full_Text_Catalogs/AW2008FullTextCatalog.md) |
| Full Text | PK_Document_DocumentNode |
| Row Count (~) | 13 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:54 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Computed | Max Length (Bytes) | Allow Nulls | Full Text Indexed | Language | Default | Description |
|---|---|---|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_Document_DocumentNode: DocumentNode](../../../../Images/pkcluster.png)](#indexes)[![Indexes AK_Document_DocumentLevel_DocumentNode](../../../../Images/Index.png)](#indexes) | DocumentNode | hierarchyid |  | 892 | NO |  |  |  | _Primary key for Document records._ |
| [![Indexes AK_Document_DocumentLevel_DocumentNode](../../../../Images/Index.png)](#indexes) | DocumentLevel | smallint | YES | 2 | YES |  |  |  | _Depth in the document hierarchy._ |
|  | Title | nvarchar(50) |  | 100 | NO |  |  |  | _Title of the document._ |
| [![Foreign Keys FK_Document_Employee_Owner: [HumanResources].[Employee].Owner](../../../../Images/fk.png)](#foreignkeys) | Owner | int |  | 4 | NO |  |  |  | _Employee who controls the document.  Foreign key to Employee.BusinessEntityID_ |
|  | FolderFlag | bit |  | 1 | NO |  |  | ((0)) | _0 = This is a folder, 1 = This is a document._ |
| [![Indexes IX_Document_FileName_Revision](../../../../Images/Index.png)](#indexes) | FileName | nvarchar(400) |  | 800 | NO |  |  |  | _File name of the document_ |
|  | FileExtension | nvarchar(8) |  | 16 | NO |  |  |  | _File extension indicating the document type. For example, .doc or .txt._ |
| [![Indexes IX_Document_FileName_Revision](../../../../Images/Index.png)](#indexes) | Revision | nchar(5) |  | 10 | NO |  |  |  | _Revision number of the document. _ |
|  | ChangeNumber | int |  | 4 | NO |  |  | ((0)) | _Engineering change approval number._ |
| [![Check Constraints CK_Document_Status : ([Status]>=(1) AND [Status]<=(3))](../../../../Images/c-constraint.png)](#checkconstraints) | Status | tinyint |  | 1 | NO |  |  |  | _1 = Pending approval, 2 = Approved, 3 = Obsolete_ |
|  | DocumentSummary | nvarchar(max) |  | max | YES | YES | 1033 |  | _Document abstract._ |
|  | Document | varbinary(max) |  | max | YES | YES | 1033 |  | _Complete document._ |
| [![Indexes AK_Document_rowguid
UQ__Document__F73921F793071A63](../../../../Images/Index.png)](#indexes)(2) | rowguid | uniqueidentifier |  | 16 | NO |  |  | (newid()) | _ROWGUIDCOL number uniquely identifying the record. Required for FileStream._ |
|  | ModifiedDate | datetime |  | 8 | NO |  |  | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#computedcolumns"></a>Computed columns

| Name | Column definition |
|---|---|
| DocumentLevel | ([DocumentNode].[GetLevel]()) |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_Document_DocumentNode: DocumentNode](../../../../Images/pkcluster.png)](#indexes) | PK_Document_DocumentNode | DocumentNode | YES | _Primary key (clustered) constraint_ |
|  | AK_Document_DocumentLevel_DocumentNode | DocumentLevel, DocumentNode | YES | _Unique nonclustered index._ |
|  | AK_Document_rowguid | rowguid | YES | _Unique nonclustered index. Used to support FileStream._ |
|  | UQ__Document__F73921F793071A63 | rowguid | YES |  |
|  | IX_Document_FileName_Revision | FileName, Revision |  | _Unique nonclustered index._ |


---

## <a name="#checkconstraints"></a>Check Constraints

| Name | On Column | Constraint | Description |
|---|---|---|---|
| CK_Document_Status | Status | ([Status]>=(1) AND [Status]<=(3)) | _Check constraint [Status] BETWEEN (1) AND (3)_ |


---

## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_Document_Employee_Owner | Owner->[[HumanResources].[Employee].[BusinessEntityID]](Employee.md) | _Foreign key constraint referencing Employee.BusinessEntityID._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Production].[Document]
(
[DocumentNode] [sys].[hierarchyid] NOT NULL,
[DocumentLevel] AS ([DocumentNode].[GetLevel]()),
[Title] [nvarchar] (50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[Owner] [int] NOT NULL,
[FolderFlag] [bit] NOT NULL CONSTRAINT [DF_Document_FolderFlag] DEFAULT ((0)),
[FileName] [nvarchar] (400) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[FileExtension] [nvarchar] (8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[Revision] [nchar] (5) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[ChangeNumber] [int] NOT NULL CONSTRAINT [DF_Document_ChangeNumber] DEFAULT ((0)),
[Status] [tinyint] NOT NULL,
[DocumentSummary] [nvarchar] (max) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
[Document] [varbinary] (max) NULL,
[rowguid] [uniqueidentifier] NOT NULL ROWGUIDCOL CONSTRAINT [DF_Document_rowguid] DEFAULT (newid()),
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_Document_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
ALTER TABLE [Production].[Document] ADD CONSTRAINT [CK_Document_Status] CHECK (([Status]>=(1) AND [Status]<=(3)))
GO
ALTER TABLE [Production].[Document] ADD CONSTRAINT [PK_Document_DocumentNode] PRIMARY KEY CLUSTERED  ([DocumentNode]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_Document_DocumentLevel_DocumentNode] ON [Production].[Document] ([DocumentLevel], [DocumentNode]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_Document_FileName_Revision] ON [Production].[Document] ([FileName], [Revision]) ON [PRIMARY]
GO
CREATE UNIQUE NONCLUSTERED INDEX [AK_Document_rowguid] ON [Production].[Document] ([rowguid]) ON [PRIMARY]
GO
ALTER TABLE [Production].[Document] ADD CONSTRAINT [UQ__Document__F73921F793071A63] UNIQUE NONCLUSTERED  ([rowguid]) ON [PRIMARY]
GO
ALTER TABLE [Production].[Document] ADD CONSTRAINT [FK_Document_Employee_Owner] FOREIGN KEY ([Owner]) REFERENCES [HumanResources].[Employee] ([BusinessEntityID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Product maintenance documents.', 'SCHEMA', N'Production', 'TABLE', N'Document', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Engineering change approval number.', 'SCHEMA', N'Production', 'TABLE', N'Document', 'COLUMN', N'ChangeNumber'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Complete document.', 'SCHEMA', N'Production', 'TABLE', N'Document', 'COLUMN', N'Document'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Depth in the document hierarchy.', 'SCHEMA', N'Production', 'TABLE', N'Document', 'COLUMN', N'DocumentLevel'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key for Document records.', 'SCHEMA', N'Production', 'TABLE', N'Document', 'COLUMN', N'DocumentNode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Document abstract.', 'SCHEMA', N'Production', 'TABLE', N'Document', 'COLUMN', N'DocumentSummary'
GO
EXEC sp_addextendedproperty N'MS_Description', N'File extension indicating the document type. For example, .doc or .txt.', 'SCHEMA', N'Production', 'TABLE', N'Document', 'COLUMN', N'FileExtension'
GO
EXEC sp_addextendedproperty N'MS_Description', N'File name of the document', 'SCHEMA', N'Production', 'TABLE', N'Document', 'COLUMN', N'FileName'
GO
EXEC sp_addextendedproperty N'MS_Description', N'0 = This is a folder, 1 = This is a document.', 'SCHEMA', N'Production', 'TABLE', N'Document', 'COLUMN', N'FolderFlag'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Production', 'TABLE', N'Document', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Employee who controls the document.  Foreign key to Employee.BusinessEntityID', 'SCHEMA', N'Production', 'TABLE', N'Document', 'COLUMN', N'Owner'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Revision number of the document. ', 'SCHEMA', N'Production', 'TABLE', N'Document', 'COLUMN', N'Revision'
GO
EXEC sp_addextendedproperty N'MS_Description', N'ROWGUIDCOL number uniquely identifying the record. Required for FileStream.', 'SCHEMA', N'Production', 'TABLE', N'Document', 'COLUMN', N'rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'1 = Pending approval, 2 = Approved, 3 = Obsolete', 'SCHEMA', N'Production', 'TABLE', N'Document', 'COLUMN', N'Status'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Title of the document.', 'SCHEMA', N'Production', 'TABLE', N'Document', 'COLUMN', N'Title'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [Status] BETWEEN (1) AND (3)', 'SCHEMA', N'Production', 'TABLE', N'Document', 'CONSTRAINT', N'CK_Document_Status'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of 0', 'SCHEMA', N'Production', 'TABLE', N'Document', 'CONSTRAINT', N'DF_Document_ChangeNumber'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Production', 'TABLE', N'Document', 'CONSTRAINT', N'DF_Document_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of NEWID()', 'SCHEMA', N'Production', 'TABLE', N'Document', 'CONSTRAINT', N'DF_Document_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Employee.BusinessEntityID.', 'SCHEMA', N'Production', 'TABLE', N'Document', 'CONSTRAINT', N'FK_Document_Employee_Owner'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Production', 'TABLE', N'Document', 'CONSTRAINT', N'PK_Document_DocumentNode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index.', 'SCHEMA', N'Production', 'TABLE', N'Document', 'INDEX', N'AK_Document_DocumentLevel_DocumentNode'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index. Used to support FileStream.', 'SCHEMA', N'Production', 'TABLE', N'Document', 'INDEX', N'AK_Document_rowguid'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Unique nonclustered index.', 'SCHEMA', N'Production', 'TABLE', N'Document', 'INDEX', N'IX_Document_FileName_Revision'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Production', 'TABLE', N'Document', 'INDEX', N'PK_Document_DocumentNode'
GO
CREATE FULLTEXT INDEX ON [Production].[Document] KEY INDEX [PK_Document_DocumentNode] ON [AW2008FullTextCatalog]
GO
ALTER FULLTEXT INDEX ON [Production].[Document] ADD ([DocumentSummary] LANGUAGE 1033)
GO
ALTER FULLTEXT INDEX ON [Production].[Document] ADD ([Document] TYPE COLUMN [FileExtension] LANGUAGE 1033)
GO

```


---

## <a name="#uses"></a>Uses

DEPENDENCYLIST* [[HumanResources].[Employee]](Employee.md)
* [Production](../Security/Schemas/Production.md)


---

## <a name="#usedby"></a>Used By

DEPENDENCYLIST* [[Production].[ProductDocument]](ProductDocument.md)
* [AW2008FullTextCatalog](../Storage/Full_Text_Catalogs/AW2008FullTextCatalog.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

