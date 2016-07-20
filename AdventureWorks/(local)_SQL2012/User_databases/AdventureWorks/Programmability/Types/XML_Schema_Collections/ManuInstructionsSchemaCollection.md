#### 

[Project](../../../../../../index.md) > [(local)\\SQL2012](../../../../../index.md) > [User databases](../../../../index.md) > [AdventureWorks](../../../index.md) > [Programmability](../../index.md) > [Types](../index.md) > [XML Schema Collections](XML_Schema_Collections.md) > Production.ManuInstructionsSchemaCollection

# ![XML Schema Collections](../../../../../../Images/XmlSchemaCollection32.png) [Production].[ManuInstructionsSchemaCollection]

---

## <a name="#description"></a>MS_Description

Collection of XML schemas for the Instructions column in the Production.ProductModel table.

## <a name="#dependentcolumns"></a>Dependent Columns

* [[Production].[ProductModel].[Instructions]](../../../Tables/ProductModel.md)


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE XML SCHEMA COLLECTION [Production].[ManuInstructionsSchemaCollection] 
AS N'<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:t="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" targetNamespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" elementFormDefault="qualified">
  <xsd:element name="root">
    <xsd:complexType mixed="true">
      <xsd:complexContent mixed="true">
        <xsd:restriction base="xsd:anyType">
          <xsd:sequence>
            <xsd:element name="Location" maxOccurs="unbounded">
              <xsd:complexType mixed="true">
                <xsd:complexContent mixed="true">
                  <xsd:restriction base="xsd:anyType">
                    <xsd:sequence>
                      <xsd:element name="step" type="t:StepType" maxOccurs="unbounded" />
                    </xsd:sequence>
                    <xsd:attribute name="LocationID" type="xsd:integer" use="required" />
                    <xsd:attribute name="SetupHours" type="xsd:decimal" />
                    <xsd:attribute name="MachineHours" type="xsd:decimal" />
                    <xsd:attribute name="LaborHours" type="xsd:decimal" />
                    <xsd:attribute name="LotSize" type="xsd:decimal" />
                  </xsd:restriction>
                </xsd:complexContent>
              </xsd:complexType>
            </xsd:element>
          </xsd:sequence>
        </xsd:restriction>
      </xsd:complexContent>
    </xsd:complexType>
  </xsd:element>
  <xsd:complexType name="StepType" mixed="true">
    <xsd:complexContent mixed="true">
      <xsd:restriction base="xsd:anyType">
        <xsd:choice minOccurs="0" maxOccurs="unbounded">
          <xsd:element name="tool" type="xsd:string" />
          <xsd:element name="material" type="xsd:string" />
          <xsd:element name="blueprint" type="xsd:string" />
          <xsd:element name="specs" type="xsd:string" />
          <xsd:element name="diag" type="xsd:string" />
        </xsd:choice>
      </xsd:restriction>
    </xsd:complexContent>
  </xsd:complexType>
</xsd:schema>'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Collection of XML schemas for the Instructions column in the Production.ProductModel table.', 'SCHEMA', N'Production', 'XML SCHEMA COLLECTION', N'ManuInstructionsSchemaCollection', NULL, NULL
GO

```


---

## <a name="#uses"></a>Uses

DEPENDENCYLIST* [Production](../../../Security/Schemas/Production.md)


---

## <a name="#usedby"></a>Used By

DEPENDENCYLIST* [[Production].[ProductModel]](../../../Tables/ProductModel.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 20 July 2016 10:31

