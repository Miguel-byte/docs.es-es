---
title: Procedimiento para obtener información sobre tipos y miembros mediante la reflexión
ms.date: 09/03/2019
helpviewer_keywords:
- reflection, obtaining member information
- types [.NET Framework], obtaining member information from
ms.assetid: 348ae651-ccda-4f13-8eda-19e8337e9438
author: rpetrusha
ms.author: ronpet
dev_langs:
- cpp
- csharp
- vb
ms.openlocfilehash: da71845ea276267220636cfd661465ea02b2b50d
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972862"
---
# <a name="how-to-get-type-and-member-information-by-using-reflection"></a>Procedimiento para obtener información sobre tipos y miembros mediante la reflexión
El espacio de nombres <xref:System.Reflection> contiene muchos métodos para obtener información sobre los tipos y sus miembros. En este artículo se muestra uno de estos métodos, <xref:System.Type.GetMembers%2A?displayProperty=nameWithType>. Para obtener más información, vea [Reflexión en .NET](reflection.md).
  
## <a name="example"></a>Ejemplo

En el ejemplo siguiente se obtiene información sobre tipos y miembros mediante la reflexión:

[!code-cpp[Get type members](../../../samples/snippets/standard/reflection/memberinfo/gettypemembers.cpp)]
[!code-csharp[Get type members](../../../samples/snippets/standard/reflection/memberinfo/gettypemembers.cs)]
[!code-vb[Get type members](../../../samples/snippets/standard/reflection/memberinfo/gettypemembers.vb)]

## <a name="see-also"></a>Vea también

- [Programación con dominios de aplicación](../app-domains/application-domains.md#programming-with-application-domains)
- [Reflexión](reflection.md)
- [Utilizar dominios de aplicación](../app-domains/use.md)
