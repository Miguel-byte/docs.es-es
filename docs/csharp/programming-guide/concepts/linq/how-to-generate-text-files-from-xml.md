---
title: Procedimiento para generar archivos de texto a partir de XML (C#)
ms.date: 07/20/2015
ms.assetid: 9ad283f7-7cac-42ff-bf32-92aa866e6883
ms.openlocfilehash: 76fcca69236ef97374855ebbb19259aa5e119ea0
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2019
ms.locfileid: "70253591"
---
# <a name="how-to-generate-text-files-from-xml-c"></a>Procedimiento para generar archivos de texto a partir de XML (C#)
Este ejemplo muestra cómo generar un archivo de valores separados por comas (CSV) a partir de un archivo XML.  
  
## <a name="example"></a>Ejemplo  
 La versión en C# de este ejemplo utiliza sintaxis de métodos y el operador `Aggregate` para generar un archivo CSV a partir de un documento XML en una única expresión. Para obtener más información, vea [Query Syntax and Method Syntax in LINQ](./query-syntax-and-method-syntax-in-linq.md) (Sintaxis de consulta y sintaxis de método en LINQ).  
  
 Este ejemplo utiliza el siguiente documento XML: [Archivo XML de ejemplo: Clientes y pedidos (LINQ to XML)](./sample-xml-file-customers-and-orders-linq-to-xml-2.md).  
  
```csharp  
XElement custOrd = XElement.Load("CustomersOrders.xml");  
string csv =  
    (from el in custOrd.Element("Customers").Elements("Customer")  
    select  
        String.Format("{0},{1},{2},{3},{4},{5},{6},{7},{8},{9}{10}",  
            (string)el.Attribute("CustomerID"),  
            (string)el.Element("CompanyName"),  
            (string)el.Element("ContactName"),  
            (string)el.Element("ContactTitle"),  
            (string)el.Element("Phone"),  
            (string)el.Element("FullAddress").Element("Address"),  
            (string)el.Element("FullAddress").Element("City"),  
            (string)el.Element("FullAddress").Element("Region"),  
            (string)el.Element("FullAddress").Element("PostalCode"),  
            (string)el.Element("FullAddress").Element("Country"),  
            Environment.NewLine  
        )  
    )  
    .Aggregate(  
        new StringBuilder(),  
        (sb, s) => sb.Append(s),  
        sb => sb.ToString()  
    );  
Console.WriteLine(csv);  
```  
  
 Este código genera el siguiente resultado:  
  
```output  
GREAL,Great Lakes Food Market,Howard Snyder,Marketing Manager,(503) 555-7555,2732 Baker Blvd.,Eugene,OR,97403,USA  
HUNGC,Hungry Coyote Import Store,Yoshi Latimer,Sales Representative,(503) 555-6874,City Center Plaza 516 Main St.,Elgin,OR,97827,USA  
LAZYK,Lazy K Kountry Store,John Steel,Marketing Manager,(509) 555-7969,12 Orchestra Terrace,Walla Walla,WA,99362,USA  
LETSS,Let's Stop N Shop,Jaime Yorres,Owner,(415) 555-5938,87 Polk St. Suite 5,San Francisco,CA,94117,USA  
```  
  
## <a name="see-also"></a>Vea también

- [Proyecciones y transformaciones (LINQ to XML) (C#)](./projections-and-transformations-linq-to-xml.md)
