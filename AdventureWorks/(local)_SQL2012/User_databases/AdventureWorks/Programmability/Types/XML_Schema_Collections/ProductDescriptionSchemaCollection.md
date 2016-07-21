#### asdasdasd

[Project](../../../../../../index.md) > [(local)\\SQL2012](../../../../../index.md) > [User databases](../../../../index.md) > [AdventureWorks](../../../index.md) > [Programmability](../../index.md) > [Types](../index.md) > [XML Schema Collections](XML_Schema_Collections.md) > Production.ProductDescriptionSchemaCollection

# ![XML Schema Collections](../../../../../../Images/XmlSchemaCollection32.png) [Production].[ProductDescriptionSchemaCollection]

---

## <a name="#description"></a>MS_Description

Collection of XML schemas for the CatalogDescription column in the Production.ProductModel table.

## <a name="#dependentcolumns"></a>Dependent Columns

* [[Production].[ProductModel].[CatalogDescription]](../../../Tables/ProductModel.md)


---

## <a name="#sqlscript"></a>SQL Script

```sql
CREATE XML SCHEMA COLLECTION [Production].[ProductDescriptionSchemaCollection] 
AS N'<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:t="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain" targetNamespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain" elementFormDefault="qualified">
  <xsd:element name="Maintenance">
    <xsd:complexType>
      <xsd:complexContent>
        <xsd:restriction base="xsd:anyType">
          <xsd:sequence>
            <xsd:element name="NoOfYears" type="xsd:string" />
            <xsd:element name="Description" type="xsd:string" />
          </xsd:sequence>
        </xsd:restriction>
      </xsd:complexContent>
    </xsd:complexType>
  </xsd:element>
  <xsd:element name="Warranty">
    <xsd:complexType>
      <xsd:complexContent>
        <xsd:restriction base="xsd:anyType">
          <xsd:sequence>
            <xsd:element name="WarrantyPeriod" type="xsd:string" />
            <xsd:element name="Description" type="xsd:string" />
          </xsd:sequence>
        </xsd:restriction>
      </xsd:complexContent>
    </xsd:complexType>
  </xsd:element>
</xsd:schema>
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:ns1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain" xmlns:t="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription" targetNamespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription" elementFormDefault="qualified">
  <xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain" />
  <xsd:element name="Code" type="xsd:string" />
  <xsd:element name="Description" type="xsd:string" />
  <xsd:element name="ProductDescription" type="t:ProductDescription" />
  <xsd:element name="Taxonomy" type="xsd:string" />
  <xsd:complexType name="Category">
    <xsd:complexContent>
      <xsd:restriction base="xsd:anyType">
        <xsd:sequence>
          <xsd:element ref="t:Taxonomy" />
          <xsd:element ref="t:Code" />
          <xsd:element ref="t:Description" minOccurs="0" />
        </xsd:sequence>
      </xsd:restriction>
    </xsd:complexContent>
  </xsd:complexType>
  <xsd:complexType name="Features" mixed="true">
    <xsd:complexContent mixed="true">
      <xsd:restriction base="xsd:anyType">
        <xsd:sequence>
          <xsd:element ref="ns1:Warranty" />
          <xsd:element ref="ns1:Maintenance" />
          <xsd:any namespace="##other" processContents="skip" minOccurs="0" maxOccurs="unbounded" />
        </xsd:sequence>
      </xsd:restriction>
    </xsd:complexContent>
  </xsd:complexType>
  <xsd:complexType name="Manufacturer">
    <xsd:complexContent>
      <xsd:restriction base="xsd:anyType">
        <xsd:sequence>
          <xsd:element name="Name" type="xsd:string" minOccurs="0" />
          <xsd:element name="CopyrightURL" type="xsd:string" minOccurs="0" />
          <xsd:element name="Copyright" type="xsd:string" minOccurs="0" />
          <xsd:element name="ProductURL" type="xsd:string" minOccurs="0" />
        </xsd:sequence>
      </xsd:restriction>
    </xsd:complexContent>
  </xsd:complexType>
  <xsd:complexType name="Picture">
    <xsd:complexContent>
      <xsd:restriction base="xsd:anyType">
        <xsd:sequence>
          <xsd:element name="Name" type="xsd:string" minOccurs="0" />
          <xsd:element name="Angle" type="xsd:string" minOccurs="0" />
          <xsd:element name="Size" type="xsd:string" minOccurs="0" />
          <xsd:element name="ProductPhotoID" type="xsd:integer" minOccurs="0" />
        </xsd:sequence>
      </xsd:restriction>
    </xsd:complexContent>
  </xsd:complexType>
  <xsd:complexType name="ProductDescription">
    <xsd:complexContent>
      <xsd:restriction base="xsd:anyType">
        <xsd:sequence>
          <xsd:element name="Summary" type="t:Summary" minOccurs="0" />
          <xsd:element name="Manufacturer" type="t:Manufacturer" minOccurs="0" />
          <xsd:element name="Features" type="t:Features" minOccurs="0" maxOccurs="unbounded" />
          <xsd:element name="Picture" type="t:Picture" minOccurs="0" maxOccurs="unbounded" />
          <xsd:element name="Category" type="t:Category" minOccurs="0" maxOccurs="unbounded" />
          <xsd:element name="Specifications" type="t:Specifications" minOccurs="0" maxOccurs="unbounded" />
        </xsd:sequence>
        <xsd:attribute name="ProductModelID" type="xsd:string" />
        <xsd:attribute name="ProductModelName" type="xsd:string" />
      </xsd:restriction>
    </xsd:complexContent>
  </xsd:complexType>
  <xsd:complexType name="Specifications" mixed="true">
    <xsd:complexContent mixed="true">
      <xsd:restriction base="xsd:anyType">
        <xsd:sequence>
          <xsd:any processContents="skip" minOccurs="0" maxOccurs="unbounded" />
        </xsd:sequence>
      </xsd:restriction>
    </xsd:complexContent>
  </xsd:complexType>
  <xsd:complexType name="Summary" mixed="true">
    <xsd:complexContent mixed="true">
      <xsd:restriction base="xsd:anyType">
        <xsd:sequence>
          <xsd:any namespace="http://www.w3.org/1999/xhtml" processContents="skip" minOccurs="0" maxOccurs="unbounded" />
        </xsd:sequence>
      </xsd:restriction>
    </xsd:complexContent>
  </xsd:complexType>
</xsd:schema>'
GO
EXEC sp_addextendedproperty N'MS_Description', N'Collection of XML schemas for the CatalogDescription column in the Production.ProductModel table.', 'SCHEMA', N'Production', 'XML SCHEMA COLLECTION', N'ProductDescriptionSchemaCollection', NULL, NULL
GO

```


---

## <a name="#uses"></a>Uses

* [Production](../../../Security/Schemas/Production.md)


---

## <a name="#usedby"></a>Used By

* [[Production].[ProductModel]](../../../Tables/ProductModel.md)


---

###### Author:  Chris Whitworth

###### Copyright 2016 - All Rights Reserved

###### Created: 21 July 2016 14:15

