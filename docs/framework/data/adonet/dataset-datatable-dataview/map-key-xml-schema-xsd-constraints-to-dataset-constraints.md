---
title: Asignar restricciones KEY de un esquema XML (XSD) a restricciones de conjuntos de datos
ms.date: 03/30/2017
ms.assetid: 22664196-f270-4ebc-a169-70e16a83dfa1
ms.openlocfilehash: 8543f5b34ee2a80ff0154897cf7678b244a8d357
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786107"
---
# <a name="map-key-xml-schema-xsd-constraints-to-dataset-constraints"></a>Asignar restricciones KEY de un esquema XML (XSD) a restricciones de conjuntos de datos
En un esquema, puede especificar una restricción de clave en un elemento o atributo mediante el elemento **key** . El elemento o el atributo para el que se especifica una restricción de clave debe tener valores únicos en cualquier instancia del esquema y no puede tener valores nulos.  
  
 La restricción de clave es similar a la restricción única, excepto en que la columna sobre la que se define una restricción de clave no puede tener valores nulos.  
  
 En la tabla siguiente se describen los atributos **msdata** que puede especificar en el elemento **key** .  
  
|Nombre del atributo|DESCRIPCIÓN|  
|--------------------|-----------------|  
|**msdata:ConstraintName**|Si se especifica este atributo, su valor se utiliza como nombre de la restricción. De lo contrario, el atributo **Name** proporciona el valor del nombre de la restricción.|  
|**msdata:PrimaryKey**|Si `PrimaryKey="true"` está presente, la propiedad de restricción **IsPrimaryKey** está establecida en **true**, por lo que se convierte en una clave principal. La propiedad de columna **AllowDBNull** está establecida en **false**, ya que las claves principales no pueden tener valores NULL.|  
  
 En la conversión del esquema en el que se especifica una restricción de clave, el proceso de asignación crea una restricción UNIQUE en la tabla con la propiedad de columna **AllowDBNull** establecida en **false** para cada columna de la restricción. La propiedad **IsPrimaryKey** de la restricción UNIQUE también se establece en **false** , a menos que `msdata:PrimaryKey="true"` haya especificado en el elemento **key** . Esto es idéntico a una restricción única del esquema donde `PrimaryKey="true"`.  
  
 En el siguiente ejemplo de esquema, el elemento **key** especifica la restricción KEY en el elemento **CustomerID** .  
  
```xml  
<xs:schema id="cod"  
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="Customers">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
        <xs:element name="CompanyName" type="xs:string" minOccurs="0" />  
       <xs:element name="Phone" type="xs:string" />  
     </xs:sequence>  
   </xs:complexType>  
 </xs:element>  
<xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element ref="Customers" />  
    </xs:choice>  
  </xs:complexType>  
   <xs:key  msdata:PrimaryKey="true"  
       msdata:ConstraintName="KeyCustID"  
          name="KeyConstCustomerID" >  
     <xs:selector xpath=".//Customers" />  
     <xs:field xpath="CustomerID" />  
    </xs:key>  
 </xs:element>  
</xs:schema>   
```  
  
 El elemento **key** especifica que los valores del elemento secundario **CustomerID** del elemento **Customers** deben tener valores únicos y no pueden tener valores NULL. Al traducir el esquema del lenguaje de definición de esquema XML (XSD), el proceso de asignación crea la tabla siguiente:  
  
```  
Customers(CustomerID, CompanyName, Phone)  
```  
  
 La asignación de esquemas XML también crea una **UniqueConstraint** en la columna **CustomerID** , como se muestra <xref:System.Data.DataSet>a continuación. Para simplificar, sólo se muestran las propiedades relevantes.  
  
```  
      DataSetName: MyDataSet  
TableName: customers  
  ColumnName: CustomerID  
      AllowDBNull: False  
      Unique: True  
  ConstraintName: KeyCustID  
      Table: customers  
      Columns: CustomerID   
      IsPrimaryKey: True  
```  
  
 En el **conjunto de DataSet** que se genera, la propiedad **IsPrimaryKey** de la **UniqueConstraint** se establece en **true** porque el `msdata:PrimaryKey="true"` esquema especifica en el elemento **key** .  
  
 El valor de la propiedad **ConstraintName** de la **UniqueConstraint** en el **DataSet** es el valor del atributo **msdata: ConstraintName** especificado en el elemento **key** del esquema.  
  
## <a name="see-also"></a>Vea también

- [Asignación de restricciones de un esquema XML (XSD) a restricciones de conjuntos de datos](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [Generación de relaciones de objetos DataSet en un esquema XML (XSD)](generating-dataset-relations-from-xml-schema-xsd.md)
- [Información general sobre ADO.NET](../ado-net-overview.md)
