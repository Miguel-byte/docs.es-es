---
title: Información general sobre el modelo de fábrica
ms.date: 03/30/2017
ms.assetid: b5dc81c4-7554-44b9-b513-769bd61e2e7b
ms.openlocfilehash: 7d50ddd3b02b66a5b2be41eaba5cf9a497b5f1b3
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795089"
---
# <a name="factory-model-overview"></a>Información general sobre el modelo de fábrica
ADO.NET 2.0 incorporó nuevas clases base en el espacio de nombres <xref:System.Data.Common>. No se pueden crear instancias directamente de las clases base debido a que son abstractas. Entre ellas se incluyen <xref:System.Data.Common.DbConnection>, <xref:System.Data.Common.DbCommand> y <xref:System.Data.Common.DbDataAdapter>, y las utilizan los proveedores de datos .NET Framework como <xref:System.Data.SqlClient> y <xref:System.Data.OleDb>. El aumento de clases base simplifica la agregación de funcionalidades a los proveedores de datos .NET Framework sin necesidad de crear nuevas interfaces.  
  
 ADO.NET 2.0 incorporó también clases base abstractas, con permiten al desarrollador escribir código de acceso a datos genérico que no dependa de un proveedor de datos concreto.  
  
## <a name="the-factory-design-pattern"></a>Patrón de diseño de generador  
 El modelo de programación para la escritura de código independiente del proveedor se basa en el uso del patrón de diseño de generador utiliza una única API para tener acceso a las bases de datos de varios proveedores. Este patrón tiene un nombre muy apropiado, dado que exige el uso de un objeto especializado solamente para crear otros objetos, de forma muy parecida a una fábrica del mundo real. Para obtener una descripción más detallada del patrón de diseño de generador, vea [escribir código genérico de acceso a datos en ASP.NET 2,0 y ADO.NET 2,0](https://go.microsoft.com/fwlink/?LinkId=55915).
  
 A partir de ADO.NET 2.0, la clase <xref:System.Data.Common.DbProviderFactories> proporciona métodos `static` (o `Shared` en Visual Basic) para crear una instancia de <xref:System.Data.Common.DbProviderFactory>. La instancia devuelve luego un objeto fuertemente tipado basado en la información sobre el proveedor y la cadena de conexión suministrada en tiempo de ejecución.  
  
## <a name="see-also"></a>Vea también

- [Obtención de un objeto DbProviderFactory](obtaining-a-dbproviderfactory.md)
- [DbConnection, DbCommand y DbException](dbconnection-dbcommand-and-dbexception.md)
- [Modificación de datos con un objeto DbDataAdapter](modifying-data-with-a-dbdataadapter.md)
- [Información general sobre ADO.NET](ado-net-overview.md)
