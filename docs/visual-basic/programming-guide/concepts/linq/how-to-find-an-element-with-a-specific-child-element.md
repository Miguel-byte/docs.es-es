---
title: Procedimiento Buscar un elemento con un elemento secundario específico (Visual Basic)
ms.date: 07/20/2015
ms.assetid: b0d0a463-6a85-46c3-8453-ad25b0ecf93c
ms.openlocfilehash: af8667b6aa6870accb62fa22bd5243ce029b32c9
ms.sourcegitcommit: eb9ff6f364cde6f11322e03800d8f5ce302f3c73
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68709064"
---
# <a name="how-to-find-an-element-with-a-specific-child-element-visual-basic"></a>Procedimiento Buscar un elemento con un elemento secundario específico (Visual Basic)
Este tema muestra cómo encontrar un elemento en particular que tenga un elemento secundario con un valor específico.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo busca el elemento `Test` que tenga un elemento secundario `CommandLine` con el valor de "Examp2.EXE".  
  
 Este ejemplo utiliza el siguiente documento XML: [Archivo XML de ejemplo: Configuración de prueba (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-test-configuration-linq-to-xml.md).  
  
```vb  
Dim root As XElement = XElement.Load("TestConfig.xml")  
Dim tests As IEnumerable(Of XElement) = _  
    From el In root.<Test> _  
    Where el.<CommandLine>.Value = "Examp2.EXE" _  
    Select el  
For Each el as XElement In tests  
    Console.WriteLine(el.@TestId)  
Next  
```  
  
 Este código genera el siguiente resultado:  
  
```  
0002  
0006  
```  
  
 Tenga en cuenta que en este ejemplo se usa la propiedad de [eje secundario XML](../../../../visual-basic/language-reference/xml-axis/xml-child-axis-property.md), la [propiedad de eje de atributo XML](../../../../visual-basic/language-reference/xml-axis/xml-attribute-axis-property.md)y la [propiedad de valor XML](../../../../visual-basic/language-reference/xml-axis/xml-value-property.md).  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo muestra la misma consulta sobre un XML que se encuentra en un espacio de nombres. Para obtener más información, vea [información general sobre los espacios de nombres (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md).  
  
 Este ejemplo utiliza el siguiente documento XML: [Archivo XML de ejemplo: Configuración de prueba en un espacio de nombres](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-test-configuration-in-a-namespace.md).  
  
```vb  
Imports <xmlns='http://www.adatum.com'>  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = XElement.Load("TestConfigInNamespace.xml")  
        Dim tests As IEnumerable(Of XElement) = _  
            From el In root.<Test> _  
            Where el.<CommandLine>.Value = "Examp2.EXE" _  
            Select el  
        For Each el As XElement In tests  
            Console.WriteLine(el.@TestId)  
        Next  
    End Sub  
End Module  
```  
  
 Este código genera el siguiente resultado:  
  
```  
0002  
0006  
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.Xml.Linq.XElement.Attribute%2A>
- <xref:System.Xml.Linq.XContainer.Elements%2A>
- [Consultas básicas (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/basic-queries-linq-to-xml.md)
- [Información general sobre operadores de consulta estándar (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [Operaciones de proyección (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/projection-operations.md)
