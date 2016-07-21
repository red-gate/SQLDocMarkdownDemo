#### asdasdasd

[Project](../../../../index.md) > [(local)\\SQL2012](../../../index.md) > [User databases](../../index.md) > [AdventureWorks](../index.md) > [Tables](Tables.md) > Production.WorkOrderRouting

# ![Tables](../../../../Images/Table32.png) [Production].[WorkOrderRouting]

---

## <a name="#description"></a>MS_Description

Work order details.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| Row Count (~) | 67131 |
| Created | 13:14:19 14 March 2012 |
| Last Modified | 13:14:55 14 March 2012 |


---

## <a name="#columns"></a>Columns

| Key | Name | Data Type | Max Length (Bytes) | Allow Nulls | Default | Description |
|---|---|---|---|---|---|---|
| [![Cluster Primary Key PK_WorkOrderRouting_WorkOrderID_ProductID_OperationSequence: WorkOrderID\ProductID\OperationSequence](../../../../Images/pkcluster.png)](#indexes)[![Foreign Keys FK_WorkOrderRouting_WorkOrder_WorkOrderID: [Production].[WorkOrder].WorkOrderID](../../../../Images/fk.png)](#foreignkeys) | WorkOrderID | int | 4 | NO |  | _Primary key. Foreign key to WorkOrder.WorkOrderID._ |
| [![Cluster Primary Key PK_WorkOrderRouting_WorkOrderID_ProductID_OperationSequence: WorkOrderID\ProductID\OperationSequence](../../../../Images/pkcluster.png)](#indexes)[![Indexes IX_WorkOrderRouting_ProductID](../../../../Images/Index.png)](#indexes) | ProductID | int | 4 | NO |  | _Primary key. Foreign key to Product.ProductID._ |
| [![Cluster Primary Key PK_WorkOrderRouting_WorkOrderID_ProductID_OperationSequence: WorkOrderID\ProductID\OperationSequence](../../../../Images/pkcluster.png)](#indexes) | OperationSequence | smallint | 2 | NO |  | _Primary key. Indicates the manufacturing process sequence._ |
| [![Foreign Keys FK_WorkOrderRouting_Location_LocationID: [Production].[Location].LocationID](../../../../Images/fk.png)](#foreignkeys) | LocationID | smallint | 2 | NO |  | _Manufacturing location where the part is processed. Foreign key to Location.LocationID._ |
|  | ScheduledStartDate | datetime | 8 | NO |  | _Planned manufacturing start date._ |
|  | ScheduledEndDate | datetime | 8 | NO |  | _Planned manufacturing end date._ |
|  | ActualStartDate | datetime | 8 | YES |  | _Actual start date._ |
|  | ActualEndDate | datetime | 8 | YES |  | _Actual end date._ |
| [![Check Constraints CK_WorkOrderRouting_ActualResourceHrs : ([ActualResourceHrs]>=(0.0000))](../../../../Images/c-constraint.png)](#checkconstraints) | ActualResourceHrs | decimal(9,4) | 5 | YES |  | _Number of manufacturing hours used._ |
| [![Check Constraints CK_WorkOrderRouting_PlannedCost : ([PlannedCost]>(0.00))](../../../../Images/c-constraint.png)](#checkconstraints) | PlannedCost | money | 8 | NO |  | _Estimated manufacturing cost._ |
| [![Check Constraints CK_WorkOrderRouting_ActualCost : ([ActualCost]>(0.00))](../../../../Images/c-constraint.png)](#checkconstraints) | ActualCost | money | 8 | YES |  | _Actual manufacturing cost._ |
|  | ModifiedDate | datetime | 8 | NO | (getdate()) | _Date and time the record was last updated._ |


---

## <a name="#indexes"></a>Indexes

| Key | Name | Key Columns | Unique | Description |
|---|---|---|---|---|
| [![Cluster Primary Key PK_WorkOrderRouting_WorkOrderID_ProductID_OperationSequence: WorkOrderID\ProductID\OperationSequence](../../../../Images/pkcluster.png)](#indexes) | PK_WorkOrderRouting_WorkOrderID_ProductID_OperationSequence | WorkOrderID, ProductID, OperationSequence | YES | _Primary key (clustered) constraint_ |
|  | IX_WorkOrderRouting_ProductID | ProductID |  | _Nonclustered index._ |


---

## <a name="#checkconstraints"></a>Check Constraints

| Name | On Column | Constraint | Description |
|---|---|---|---|
| CK_WorkOrderRouting_ActualCost | ActualCost | ([ActualCost]>(0.00)) | _Check constraint [ActualCost] > (0.00)_ |
| CK_WorkOrderRouting_ActualEndDate |  | ([ActualEndDate]>=[ActualStartDate] OR [ActualEndDate] IS NULL OR [ActualStartDate] IS NULL) | _Check constraint [ActualEndDate] >= [ActualStartDate] OR [ActualEndDate] IS NULL OR [ActualStartDate] IS NULL_ |
| CK_WorkOrderRouting_ActualResourceHrs | ActualResourceHrs | ([ActualResourceHrs]>=(0.0000)) | _Check constraint [ActualResourceHrs] >= (0.0000)_ |
| CK_WorkOrderRouting_PlannedCost | PlannedCost | ([PlannedCost]>(0.00)) | _Check constraint [PlannedCost] > (0.00)_ |
| CK_WorkOrderRouting_ScheduledEndDate |  | ([ScheduledEndDate]>=[ScheduledStartDate]) | _Check constraint [ScheduledEndDate] >= [ScheduledStartDate]_ |


---

## <a name="#foreignkeys"></a>Foreign Keys

| Name | Columns | Description |
|---|---|---|
| FK_WorkOrderRouting_Location_LocationID | LocationID->[[Production].[Location].[LocationID]](Location.md) | _Foreign key constraint referencing Location.LocationID._ |
| FK_WorkOrderRouting_WorkOrder_WorkOrderID | WorkOrderID->[[Production].[WorkOrder].[WorkOrderID]](WorkOrder.md) | _Foreign key constraint referencing WorkOrder.WorkOrderID._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE TABLE [Production].[WorkOrderRouting]
(
[WorkOrderID] [int] NOT NULL,
[ProductID] [int] NOT NULL,
[OperationSequence] [smallint] NOT NULL,
[LocationID] [smallint] NOT NULL,
[ScheduledStartDate] [datetime] NOT NULL,
[ScheduledEndDate] [datetime] NOT NULL,
[ActualStartDate] [datetime] NULL,
[ActualEndDate] [datetime] NULL,
[ActualResourceHrs] [decimal] (9, 4) NULL,
[PlannedCost] [money] NOT NULL,
[ActualCost] [money] NULL,
[ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_WorkOrderRouting_ModifiedDate] DEFAULT (getdate())
) ON [PRIMARY]
GO
ALTER TABLE [Production].[WorkOrderRouting] ADD CONSTRAINT [CK_WorkOrderRouting_ActualCost] CHECK (([ActualCost]>(0.00)))
GO
ALTER TABLE [Production].[WorkOrderRouting] ADD CONSTRAINT [CK_WorkOrderRouting_ActualEndDate] CHECK (([ActualEndDate]>=[ActualStartDate] OR [ActualEndDate] IS NULL OR [ActualStartDate] IS NULL))
GO
ALTER TABLE [Production].[WorkOrderRouting] ADD CONSTRAINT [CK_WorkOrderRouting_ActualResourceHrs] CHECK (([ActualResourceHrs]>=(0.0000)))
GO
ALTER TABLE [Production].[WorkOrderRouting] ADD CONSTRAINT [CK_WorkOrderRouting_PlannedCost] CHECK (([PlannedCost]>(0.00)))
GO
ALTER TABLE [Production].[WorkOrderRouting] ADD CONSTRAINT [CK_WorkOrderRouting_ScheduledEndDate] CHECK (([ScheduledEndDate]>=[ScheduledStartDate]))
GO
ALTER TABLE [Production].[WorkOrderRouting] ADD CONSTRAINT [PK_WorkOrderRouting_WorkOrderID_ProductID_OperationSequence] PRIMARY KEY CLUSTERED  ([WorkOrderID], [ProductID], [OperationSequence]) ON [PRIMARY]
GO
CREATE NONCLUSTERED INDEX [IX_WorkOrderRouting_ProductID] ON [Production].[WorkOrderRouting] ([ProductID]) ON [PRIMARY]
GO
ALTER TABLE [Production].[WorkOrderRouting] ADD CONSTRAINT [FK_WorkOrderRouting_Location_LocationID] FOREIGN KEY ([LocationID]) REFERENCES [Production].[Location] ([LocationID])
GO
ALTER TABLE [Production].[WorkOrderRouting] ADD CONSTRAINT [FK_WorkOrderRouting_WorkOrder_WorkOrderID] FOREIGN KEY ([WorkOrderID]) REFERENCES [Production].[WorkOrder] ([WorkOrderID])
GO
EXEC sp_addextendedproperty N'MS_Description', N'Work order details.', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Actual manufacturing cost.', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'COLUMN', N'ActualCost'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Actual end date.', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'COLUMN', N'ActualEndDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Number of manufacturing hours used.', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'COLUMN', N'ActualResourceHrs'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Actual start date.', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'COLUMN', N'ActualStartDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Manufacturing location where the part is processed. Foreign key to Location.LocationID.', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'COLUMN', N'LocationID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Date and time the record was last updated.', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'COLUMN', N'ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key. Indicates the manufacturing process sequence.', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'COLUMN', N'OperationSequence'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Estimated manufacturing cost.', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'COLUMN', N'PlannedCost'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key. Foreign key to Product.ProductID.', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'COLUMN', N'ProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Planned manufacturing end date.', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'COLUMN', N'ScheduledEndDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Planned manufacturing start date.', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'COLUMN', N'ScheduledStartDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key. Foreign key to WorkOrder.WorkOrderID.', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'COLUMN', N'WorkOrderID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [ActualCost] > (0.00)', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'CONSTRAINT', N'CK_WorkOrderRouting_ActualCost'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [ActualEndDate] >= [ActualStartDate] OR [ActualEndDate] IS NULL OR [ActualStartDate] IS NULL', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'CONSTRAINT', N'CK_WorkOrderRouting_ActualEndDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [ActualResourceHrs] >= (0.0000)', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'CONSTRAINT', N'CK_WorkOrderRouting_ActualResourceHrs'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [PlannedCost] > (0.00)', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'CONSTRAINT', N'CK_WorkOrderRouting_PlannedCost'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Check constraint [ScheduledEndDate] >= [ScheduledStartDate]', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'CONSTRAINT', N'CK_WorkOrderRouting_ScheduledEndDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Default constraint value of GETDATE()', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'CONSTRAINT', N'DF_WorkOrderRouting_ModifiedDate'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing Location.LocationID.', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'CONSTRAINT', N'FK_WorkOrderRouting_Location_LocationID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Foreign key constraint referencing WorkOrder.WorkOrderID.', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'CONSTRAINT', N'FK_WorkOrderRouting_WorkOrder_WorkOrderID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Primary key (clustered) constraint', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'CONSTRAINT', N'PK_WorkOrderRouting_WorkOrderID_ProductID_OperationSequence'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Nonclustered index.', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'INDEX', N'IX_WorkOrderRouting_ProductID'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Clustered index created by a primary key constraint.', 'SCHEMA', N'Production', 'TABLE', N'WorkOrderRouting', 'INDEX', N'PK_WorkOrderRouting_WorkOrderID_ProductID_OperationSequence'
GO

```


---

## <a name="#uses"></a>Uses

* [[Production].[Location]](Location.md)
* [[Production].[WorkOrder]](WorkOrder.md)
* [Production](../Security/Schemas/Production.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 12:25

