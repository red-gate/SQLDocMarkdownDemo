#### 

[Project](../../../../../index.md) > [(local)\\SQL2012](../../../../index.md) > [User databases](../../../index.md) > [AdventureWorks](../../index.md) > [Programmability](../index.md) > [Database Triggers](Database_Triggers.md) > ddlDatabaseTriggerLog

# ![Database Triggers](../../../../../Images/DdlTrigger32.png) ddlDatabaseTriggerLog

---

## <a name="#description"></a>MS_Description

Database trigger to audit all of the DDL changes made to the AdventureWorks 2012 database.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| ANSI Nulls On | YES |
| Quoted Identifier On | YES |
| Disabled | YES |


---

## <a name="#sqlscript"></a>SQL Script

```sql

CREATE TRIGGER [ddlDatabaseTriggerLog] ON DATABASE 
FOR DDL_DATABASE_LEVEL_EVENTS AS 
BEGIN
    SET NOCOUNT ON;

    DECLARE @data XML;
    DECLARE @schema sysname;
    DECLARE @object sysname;
    DECLARE @eventType sysname;

    SET @data = EVENTDATA();
    SET @eventType = @data.value('(/EVENT_INSTANCE/EventType)[1]', 'sysname');
    SET @schema = @data.value('(/EVENT_INSTANCE/SchemaName)[1]', 'sysname');
    SET @object = @data.value('(/EVENT_INSTANCE/ObjectName)[1]', 'sysname') 

    IF @object IS NOT NULL
        PRINT '  ' + @eventType + ' - ' + @schema + '.' + @object;
    ELSE
        PRINT '  ' + @eventType + ' - ' + @schema;

    IF @eventType IS NULL
        PRINT CONVERT(nvarchar(max), @data);

    INSERT [dbo].[DatabaseLog] 
        (
        [PostTime], 
        [DatabaseUser], 
        [Event], 
        [Schema], 
        [Object], 
        [TSQL], 
        [XmlEvent]
        ) 
    VALUES 
        (
        GETDATE(), 
        CONVERT(sysname, CURRENT_USER), 
        @eventType, 
        CONVERT(sysname, @schema), 
        CONVERT(sysname, @object), 
        @data.value('(/EVENT_INSTANCE/TSQLCommand)[1]', 'nvarchar(max)'), 
        @data
        );
END;
GO
DISABLE TRIGGER ddlDatabaseTriggerLog ON DATABASE
GO
EXEC sp_addextendedproperty N'MS_Description', N'Database trigger to audit all of the DDL changes made to the AdventureWorks 2012 database.', 'TRIGGER', N'ddlDatabaseTriggerLog', NULL, NULL, NULL, NULL
GO

```


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

