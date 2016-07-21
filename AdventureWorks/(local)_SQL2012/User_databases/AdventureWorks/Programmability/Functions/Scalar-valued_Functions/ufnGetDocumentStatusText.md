#### asdasdasd

[Project](../../../../../../index.md) > [(local)\\SQL2012](../../../../../index.md) > [User databases](../../../../index.md) > [AdventureWorks](../../../index.md) > [Programmability](../../index.md) > [Functions](../index.md) > [Scalar-valued Functions](Scalar-valued_Functions.md) > dbo.ufnGetDocumentStatusText

# ![Scalar-valued Functions](../../../../../../Images/Function_Scalar32.png) [dbo].[ufnGetDocumentStatusText]

---

## <a name="#description"></a>MS_Description

Scalar function returning the text representation of the Status column in the Document table.

## <a name="#properties"></a>Properties

| Property | Value |
|---|---|
| ANSI Nulls On | YES |
| Quoted Identifier On | YES |


---

## <a name="#parameters"></a>Parameters

| Name | Data Type | Max Length (Bytes) | Description |
|---|---|---|---|
| @Status | tinyint | 1 | _Input parameter for the scalar function ufnGetDocumentStatusText. Enter a valid integer._ |


---

## <a name="#sqlscript"></a>SQL Script

```sql

CREATE FUNCTION [dbo].[ufnGetDocumentStatusText](@Status [tinyint])
RETURNS [nvarchar](16) 
AS 
-- Returns the sales order status text representation for the status value.
BEGIN
    DECLARE @ret [nvarchar](16);

    SET @ret = 
        CASE @Status
            WHEN 1 THEN N'Pending approval'
            WHEN 2 THEN N'Approved'
            WHEN 3 THEN N'Obsolete'
            ELSE N'** Invalid **'
        END;
    
    RETURN @ret
END;
GO
EXEC sp_addextendedproperty N'MS_Description', N'Scalar function returning the text representation of the Status column in the Document table.', 'SCHEMA', N'dbo', 'FUNCTION', N'ufnGetDocumentStatusText', NULL, NULL
GO
EXEC sp_addextendedproperty N'MS_Description', N'Input parameter for the scalar function ufnGetDocumentStatusText. Enter a valid integer.', 'SCHEMA', N'dbo', 'FUNCTION', N'ufnGetDocumentStatusText', 'PARAMETER', N'@Status'
GO

```


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 14:15

