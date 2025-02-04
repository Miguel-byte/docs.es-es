---
title: Procedimiento Personalizar fuentes con el proveedor de Entity Framework (WCF Data Services)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, customizing
- WCF Data Services, customizing feeds
ms.assetid: fd16272e-36f2-415e-850e-8a81f2b17525
ms.openlocfilehash: 8f994065ea42d6fc522fa297cafa8c46a8164e67
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2019
ms.locfileid: "70780155"
---
# <a name="how-to-customize-feeds-with-the-entity-framework-provider-wcf-data-services"></a>Procedimiento Personalizar fuentes con el proveedor de Entity Framework (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] le permite personalizar la serialización Atom en una respuesta del servicio de datos para que las propiedades de una entidad se puedan asignar a los elementos no usados que se definen en el protocolo AtomPub. En este tema se explica cómo definir los atributos de asignación para los tipos de entidad en un modelo de datos definido en un archivo .edmx utilizando el proveedor de Entity Framework. Para obtener más información, vea [Personalización de fuentes](feed-customization-wcf-data-services.md).  
  
 En este tema modificará manualmente el archivo .edmx generado por la herramienta que contiene el modelo de datos. Dado que Entity Designer no admite las extensiones al modelo de datos, debe modificar manualmente el archivo. Para obtener más información sobre el archivo. edmx generado por las herramientas de Entity Data Model, vea [información general sobre el archivo. edmx (Entity Framework)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100)). En el ejemplo de este tema se usa el servicio de datos de ejemplo Northwind y las clases del servicio de datos de cliente generadas automáticamente. Este servicio y las clases de datos de cliente se crean al completar la guía de [Inicio rápido de WCF Data Services](quickstart-wcf-data-services.md).  
  
### <a name="to-manually-modify-the-northwindedmx-file-to-add-feed-customization-attributes"></a>Para modificar manualmente el archivo Northwind.edmx para agregar los atributos de personalización de fuente  
  
1. En **Explorador de soluciones**, haga clic con el `Northwind.edmx` botón secundario en el archivo y, a continuación, haga clic en **abrir con**.  
  
2. En el cuadro de diálogo **abrir con-Northwind. edmx** , seleccione **Editor XML**y, a continuación, haga clic en **Aceptar**.  
  
3. Busque el elemento `ConceptualModels` y reemplace el tipo de entidad `Customers` existente con el siguiente elemento que contiene los atributos de asignación de personalización de la fuente:  
  
     [!code-xml[Astoria Custom Feeds#EdmFeedCustomers](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria_custom_feeds/xml/northwind.csdl#edmfeedcustomers)]  
  
4. Guarde los cambios y cierre el archivo Northwind.edmx.  
  
5. Opta Haga clic con el botón secundario en el archivo Northwind. edmx y, a continuación, haga clic en **Ejecutar herramienta personalizada**.  
  
     Esto regenera el archivo de capa de objeto, que puede ser necesario.  
  
6. Compile de nuevo el proyecto.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo anterior se devuelve el resultado siguiente para el identificador URI `http://myservice/Northwind.svc/Customers('ALFKI')`.  
  
 [!code-xml[Astoria Custom Feeds#EdmFeedResult](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria_custom_feeds/xml/edmfeedresult.xml#edmfeedresult)]  
  
## <a name="see-also"></a>Vea también

- [Proveedor de Entity Framework](entity-framework-provider-wcf-data-services.md)
