---
title: Procedimiento para descargar un dominio de aplicación
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Unload method
- application domains, unloading
- unloading application domains
ms.assetid: f356116d-e415-4f7c-a332-6e6a60227192
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f7419725f3822622a8e4210d4f3f5d8e9e59dbdd
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053135"
---
# <a name="how-to-unload-an-application-domain"></a>Procedimiento para descargar un dominio de aplicación
Cuando haya terminado de usar un dominio de aplicación, descárguelo con el método <xref:System.AppDomain.Unload%2A?displayProperty=nameWithType>. El método **Unload** cierra discretamente el dominio de aplicación especificado. Durante el proceso de descarga, ningún subproceso nuevo puede obtener acceso al dominio de aplicación. Además, se liberan todas las estructuras de datos específicas del dominio de aplicación.  
  
 Los ensamblados cargados en el dominio de aplicación se quitan y dejan de estar disponibles. Si un ensamblado del dominio de aplicación es neutral respecto al dominio, sus datos permanecen en la memoria hasta que se cierra todo el proceso. No existe ningún mecanismo para descargar un ensamblado neutral con respecto al dominio, aparte de cerrar todo el proceso. Existen situaciones en las que la solicitud para descargar un dominio de aplicación no funciona y genera como resultado una <xref:System.CannotUnloadAppDomainException>.  
  
 En el ejemplo siguiente se crea un nuevo dominio de aplicación denominado `MyDomain`, se imprime cierta información en la consola y, a continuación, se descarga el dominio de aplicación. Tenga en cuenta que, después, el código intenta imprimir en la consola el nombre descriptivo del dominio de aplicación descargado. Esta acción genera una excepción que controlan las instrucciones try/catch al final del programa.  
  
## <a name="example"></a>Ejemplo  
 [!code-cpp[System.AppDomain.Load#3](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.appdomain.load/cpp/source3.cpp#3)]
 [!code-csharp[System.AppDomain.Load#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.load/cs/source3.cs#3)]
 [!code-vb[System.AppDomain.Load#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.load/vb/source3.vb#3)]  
  
## <a name="see-also"></a>Vea también

- [Programar con dominios de aplicación](application-domains.md#programming-with-application-domains)
- [Cómo: Crear un dominio de aplicación](how-to-create-an-application-domain.md)
- [Utilizar dominios de aplicación](use.md)
