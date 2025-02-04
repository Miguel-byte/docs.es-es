---
ms.openlocfilehash: 060da3ebc60057554fd572bd2569652afee6bd0f
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67804473"
---
### <a name="il-ret-not-allowed-in-a-try-region"></a>No se permite ret de IL en una región try

|   |   |
|---|---|
|Detalles|A diferencia del compilador Just-In-Time JIT64, RyuJIT (que se usa en .NET Framework 4.6) no admite una instrucción ret de nivel de integridad en una región try. Devolver desde una región try no permite la especificación de ECMA-335 y ningún compilador administrado conocido genera tal IL. Sin embargo, el compilador JIT64 ejecutará dicho IL si se genera mediante la emisión de reflexión.|
|Sugerencia|Si una aplicación genera un IL que incluye un código de operación de ret en una región try, la aplicación puede tener como destino .NET Framework 4.5 para usar el JIT antiguo y evitar esta interrupción. Como alternativa, se puede actualizar el IL generado para que devuelva después de la región try.|
|Ámbito|Borde|
|Versión|4.6|
|Tipo|Redestinación|

