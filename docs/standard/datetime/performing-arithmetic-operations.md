---
title: Efectuar operaciones aritméticas con fechas y horas
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- times [.NET Framework], arithmetic operations
- dates [.NET Framework], arithmetic operations
- time zones [.NET Framework], arithmetic operations
- arithmetic operations [.NET Framework], dates and times
- dates [.NET Framework], comparing
- DateTime structure, arithmetic operations
- DateTimeOffset structure, arithmetic operations
ms.assetid: 87c7ddf2-f15e-48af-8602-b3642237e6d0
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 01314c160fc531f5c97a1369c8444dce7f590d53
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2019
ms.locfileid: "70106614"
---
# <a name="performing-arithmetic-operations-with-dates-and-times"></a>Efectuar operaciones aritméticas con fechas y horas

Aunque las <xref:System.DateTime> <xref:System.DateTimeOffset> estructuras y proporcionan miembros que realizan operaciones aritméticas en sus valores, los resultados de las operaciones aritméticas son muy diferentes. En este tema se examinan estas diferencias, se relacionan con los grados de reconocimiento de la zona horaria en los datos de fecha y hora, y se explica cómo realizar operaciones con reconocimiento completo de la zona horaria mediante datos de fecha y hora.

## <a name="comparisons-and-arithmetic-operations-with-datetime-values"></a>Comparaciones y operaciones aritméticas con valores DateTime

La <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> propiedad permite asignar <xref:System.DateTimeKind> un valor a la fecha y hora para indicar si representa la hora local, la hora universal coordinada (UTC) o la hora de una zona horaria no especificada. Sin embargo, esta información limitada de zona horaria se omite al comparar o realizar operaciones aritméticas de <xref:System.DateTimeKind> fecha y hora en valores. Esto se muestra en el ejemplo siguiente, que compara la hora local actual con la hora UTC actual.

[!code-csharp[System.DateTimeOffset.Conceptual#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual2.cs#2)]
[!code-vb[System.DateTimeOffset.Conceptual#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual2.vb#2)]

El <xref:System.DateTime.CompareTo%28System.DateTime%29> método informa de que la hora local es anterior a (o menor que) la hora UTC, y la operación de resta indica que la diferencia entre la hora UTC y la hora local de un sistema de EE. UU. es de siete horas. Pero, dado que estos dos valores proporcionan representaciones diferentes de un único punto en el tiempo, resulta evidente en este caso que este intervalo de tiempo es totalmente atribuible a la diferencia horaria de la zona horaria local respecto de la hora UTC.

En general, la <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> propiedad no afecta a los resultados devueltos por <xref:System.DateTime.Kind> los métodos aritméticos y de comparación (como se indica en la comparación de dos puntos idénticos en el tiempo), aunque puede afectar a la interpretación de los resultados. Por ejemplo:

- El resultado de cualquier operación aritmética realizada en dos valores de fecha y hora <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> cuyas propiedades son <xref:System.DateTimeKind> iguales refleja el intervalo de tiempo real entre los dos valores. Del mismo modo, la comparación de estos dos valores de fecha y hora refleja con exactitud la relación entre los tiempos.

- El resultado de cualquier operación aritmética o de comparación realizada en dos valores de fecha y <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> hora cuyas propiedades <xref:System.DateTimeKind> sean iguales o en dos valores de fecha y <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> hora con diferentes valores de propiedad refleja la diferencia en el tiempo de reloj. entre los dos valores.

- Las operaciones aritméticas o de comparación en valores de fecha y hora local no tienen en cuenta si un valor concreto es ambiguo o no válido, ni tienen en cuenta el efecto de las reglas de ajuste que son consecuencia de la transición de la zona horaria local hacia o desde el horario de verano.

- Las operaciones que comparen o calculen la diferencia entre la hora UTC y una hora local incluyen en el resultado un intervalo de tiempo igual a la diferencia horaria de la zona horaria local respecto de la hora UTC.

- Las operaciones que comparen o calculen la diferencia entre una hora no especificada y la hora UTC o la hora local reflejan la hora de reloj simple. No se consideran las diferencias de zona horaria y el resultado no refleja la aplicación de reglas de ajuste de zona horaria.

- Las operaciones que comparen o calculen la diferencia entre dos horas no especificadas pueden incluir un intervalo desconocido que refleje la diferencia entre la hora de dos zonas horarias diferentes.

Hay muchos escenarios en los que las diferencias de zona horaria no afectan a los cálculos de fecha y hora (para obtener una explicación de algunos de ellos, vea [elegir entre DateTime, DateTimeOffset, TimeSpan y TimeZoneInfo](../../../docs/standard/datetime/choosing-between-datetime.md)) o en los que el contexto de los datos de fecha y hora define el significado de las operaciones aritméticas o de comparación.

## <a name="comparisons-and-arithmetic-operations-with-datetimeoffset-values"></a>Comparaciones y operaciones aritméticas con valores DateTimeOffset

Un <xref:System.DateTimeOffset> valor incluye no solo una fecha y hora, sino también un desplazamiento que define sin ambigüedad esa fecha y hora con respecto a la hora UTC. Esto permite definir la igualdad de forma ligeramente distinta a la <xref:System.DateTimeOffset> de los valores. Mientras <xref:System.DateTime> que los valores son iguales si tienen el mismo valor de fecha y <xref:System.DateTimeOffset> hora, los valores son iguales si ambos hacen referencia al mismo punto en el tiempo. Esto hace que <xref:System.DateTimeOffset> un valor sea más preciso y menor que la necesidad de interpretación cuando se usa en comparaciones y en la mayoría de las operaciones aritméticas que determinan el intervalo entre dos fechas y horas. En el ejemplo siguiente, que es <xref:System.DateTimeOffset> el equivalente al ejemplo anterior que comparó valores locales <xref:System.DateTimeOffset> y UTC, se muestra esta diferencia de comportamiento.

[!code-csharp[System.DateTimeOffset.Conceptual#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual3.cs#3)]
[!code-vb[System.DateTimeOffset.Conceptual#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual3.vb#3)]

En este ejemplo, el <xref:System.DateTimeOffset.CompareTo%2A> método indica que la hora local actual y la hora UTC actual son iguales, y la resta de <xref:System.DateTimeOffset.CompareTo(System.DateTimeOffset)> valores indica que la diferencia entre las dos horas es <xref:System.TimeSpan.Zero?displayProperty=nameWithType>.

La principal limitación de usar <xref:System.DateTimeOffset> valores en las operaciones aritméticas de fecha y <xref:System.DateTimeOffset> hora es que, aunque los valores tienen algún reconocimiento de zona horaria, no son totalmente compatibles con la zona horaria. Aunque el <xref:System.DateTimeOffset> desplazamiento del valor refleja el desplazamiento de una zona horaria con respecto a <xref:System.DateTimeOffset> la hora UTC cuando se asigna por primera vez un valor a una variable, se desasocia de la zona horaria a partir de entonces. Dado que ya no está directamente asociada con una hora identificable, la suma y resta de intervalos de fecha y hora no tiene en cuenta las reglas de ajuste de una zona horaria.

Por ejemplo, la transición al horario de verano en la zona de la hora estándar central de los Estados Unidos se produce a las 2:00 a. m. del 9 de marzo de 2008. Esto significa que la suma de un intervalo de dos horas y media a la hora estándar central 1:30 a. m. del día 9 de marzo de 2008 debería generar la siguiente fecha y hora: 5:00 a. m. del 9 de marzo de 2008. Pero como se muestra en el ejemplo siguiente, el resultado de la suma es 4:00 a. m. del 9 de marzo de 2008. Observe que el resultado de esta operación representa el punto correcto en el tiempo, aunque no es la hora de la zona horaria que nos interesa (es decir, no tiene la diferencia horaria de la zona horaria esperada).

[!code-csharp[System.DateTimeOffset.Conceptual#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual4.cs#4)]
[!code-vb[System.DateTimeOffset.Conceptual#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual4.vb#4)]

## <a name="arithmetic-operations-with-times-in-time-zones"></a>Operaciones aritméticas con horas en zonas horarias

La <xref:System.TimeZoneInfo> clase incluye una serie de métodos de conversión que aplican automáticamente los ajustes cuando convierten las horas de una zona horaria a otra. Entre ellas se incluyen las siguientes:

- Los <xref:System.TimeZoneInfo.ConvertTime%2A> métodos <xref:System.TimeZoneInfo.ConvertTimeBySystemTimeZoneId%2A> y, que convierten las horas entre dos zonas horarias cualesquiera.

- Los <xref:System.TimeZoneInfo.ConvertTimeFromUtc%2A> métodos <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A> y, que convierten la hora de una zona horaria determinada en una hora UTC o convierta la hora UTC a la hora de una zona horaria determinada.

Para obtener más información, consulte [convertir horas entre zonas horarias](../../../docs/standard/datetime/converting-between-time-zones.md).

La <xref:System.TimeZoneInfo.ConvertTimeToUtc(System.DateTime)> clase no proporciona métodos que apliquen automáticamente reglas de ajuste al realizar operaciones aritméticas de fecha y hora. Para hacerlo, puede convertir la hora de una zona horaria a la hora UTC, realizar la operación aritmética y, después, convertir la hora UTC de nuevo a la hora de la zona horaria. Para obtener más detalles, vea [Cómo: Usar zonas horarias en operaciones aritméticas](../../../docs/standard/datetime/use-time-zones-in-arithmetic.md)de fecha y hora.

Por ejemplo, el código siguiente se parece al código anterior que sumaba dos horas y media a la fecha y hora 2:00 a. m. del 9 de marzo de 2008. Pero, dado que convierte una hora estándar central a la hora UTC antes de realizar la operación aritmética de fecha y hora y, después, convierte el resultado en hora UTC de nuevo a la hora estándar central, la hora resultante refleja la transición de la zona de la hora estándar central al horario de verano.

[!code-csharp[System.DateTimeOffset.Conceptual#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual5.cs#5)]
[!code-vb[System.DateTimeOffset.Conceptual#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual5.vb#5)]

## <a name="see-also"></a>Vea también

- [Fechas, horas y zonas horarias](../../../docs/standard/datetime/index.md)
- [Cómo: Usar zonas horarias en operaciones aritméticas de fecha y hora](../../../docs/standard/datetime/use-time-zones-in-arithmetic.md)
