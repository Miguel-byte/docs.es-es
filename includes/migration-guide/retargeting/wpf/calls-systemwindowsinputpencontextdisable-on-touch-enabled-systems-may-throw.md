---
ms.openlocfilehash: 0778285ef1b5702bd79743038a1bd21ba04612d6
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67804326"
---
### <a name="calls-to-systemwindowsinputpencontextdisable-on-touch-enabled-systems-may-throw-an-argumentexception"></a>Las llamadas a System.Windows.Input.PenContext.Disable en sistemas táctiles pueden iniciar una excepción ArgumentException

|   |   |
|---|---|
|Detalles|En algunas circunstancias, las llamadas al método interno <strong>System.Windows.Intput.PenContext.Disable</strong> en sistemas táctiles pueden iniciar una excepción <code>T:System.ArgumentException</code> no controlada debido a la reentrada.|
|Sugerencia|Este problema se ha corregido en .NET Framework 4.7. Para evitar la excepción, actualice a una versión de .NET Framework a partir de .NET Framework 4.7.|
|Ámbito|Borde|
|Versión|4.6.1|
|Tipo|Redestinación|

