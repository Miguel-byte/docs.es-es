---
title: Procedimiento Trabajar con diccionarios mediante LINQ to XML (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 6cb3f969-1986-414a-b850-87418712edea
ms.openlocfilehash: 9773b926d16b51ea912792b0f348a26a9a3c7a29
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/03/2019
ms.locfileid: "71835086"
---
# <a name="how-to-work-with-dictionaries-using-linq-to-xml-visual-basic"></a>Procedimiento Trabajar con diccionarios mediante LINQ to XML (Visual Basic)
A menudo resulta cómodo convertir variedades de estructuras de datos a XML y de XML a otras estructuras de datos. Este tema muestra una implementación específica de este enfoque general convirtiendo un <xref:System.Collections.Generic.Dictionary%602> a XML y de XML.  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo se usan literales XML y una consulta en una expresión incrustada. La consulta proyecta nuevos objetos <xref:System.Xml.Linq.XElement>, que se convierten en el nuevo contenido del objeto `Root` <xref:System.Xml.Linq.XElement>.  
  
```vb  
Dim dict As Dictionary(Of String, String) = New Dictionary(Of String, String)()  
dict.Add("Child1", "Value1")  
dict.Add("Child2", "Value2")  
dict.Add("Child3", "Value3")  
dict.Add("Child4", "Value4")  
Dim root As XElement = _  
    <Root>  
        <%= From keyValue In dict _  
            Select New XElement(keyValue.Key, keyValue.Value) %>  
    </Root>  
Console.WriteLine(root)  
```  
  
 Este código genera el siguiente resultado:  
  
```xml  
          <Root>  
  <Child1>Value1</Child1>  
  <Child2>Value2</Child2>  
  <Child3>Value3</Child3>  
  <Child4>Value4</Child4>  
</Root>  
```  
  
## <a name="example"></a>Ejemplo  
 El siguiente código genera un diccionario de XML.  
  
```vb  
Dim root As XElement = _  
        <Root>  
            <Child1>Value1</Child1>  
            <Child2>Value2</Child2>  
            <Child3>Value3</Child3>  
            <Child4>Value4</Child4>  
        </Root>  
  
Dim dict As Dictionary(Of String, String) = New Dictionary(Of String, String)  
For Each el As XElement In root.Elements  
    dict.Add(el.Name.LocalName, el.Value)  
Next  
For Each str As String In dict.Keys  
    Console.WriteLine("{0}:{1}", str, dict(str))  
Next  
```  
  
 Este código genera el siguiente resultado:  
  
```console  
Child1:Value1  
Child2:Value2  
Child3:Value3  
Child4:Value4  
```  
  
## <a name="see-also"></a>Vea también

- [Proyecciones y transformaciones (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/projections-and-transformations-linq-to-xml.md)
