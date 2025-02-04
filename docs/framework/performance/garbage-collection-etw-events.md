---
title: Eventos ETW de recolección de elementos no utilizados
ms.date: 03/30/2017
helpviewer_keywords:
- GC events
- garbage collection events [.NET Framework]
- ETW, garbage collection events (CLR)
ms.assetid: f14b6fd7-0966-4d87-bc89-54ef3a44a94a
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ec90d022a0c72782f413a84b6fbd2c1b8d663a73
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046504"
---
# <a name="garbage-collection-etw-events"></a>Eventos ETW de recolección de elementos no utilizados
<a name="top"></a> Estos eventos recopilan información sobre la recolección de elementos no utilizados. Ayudan en el diagnóstico y depuración, así como en la determinación de cuántas veces se realizó la recolección de elementos no utilizados, cuánta memoria se liberó durante la recolección de elementos no utilizados, etc.  
  
 Esta categoría consta de los siguientes eventos:  
  
- [Evento GCStart_V1](#gcstart_v1_event)  
  
- [Evento GCEnd_V1](#gcend_v1_event)  
  
- [Evento GCHeapStats_V1](#gcheapstats_v1_event)  
  
- [Evento GCCreateSegment_V1](#gccreatesegment_v1_event)  
  
- [Evento GCFreeSegment_V1](#gcfreesegment_v1_event)  
  
- [Evento GCRestartEEBegin_V1](#gcrestarteebegin_v1_event)  
  
- [Evento GCRestartEEEnd_V1](#gcrestarteeend_v1_event)  
  
- [Evento GCSuspendEE_V1](#gcsuspendee_v1_event)  
  
- [Evento GCSuspendEE_V1](#gcsuspendeeend_v1_event)  
  
- [Evento GCAllocationTick_V2](#gcallocationtick_v2_event)  
  
- [Evento GCFinalizersBegin_V1](#gcfinalizersbegin_v1_event)  
  
- [Evento GCFinalizersEnd_V1](#gcfinalizersend_v1_event)  
  
- [Evento GCCreateConcurrentThread_V1](#gccreateconcurrentthread_v1_event)  
  
- [Evento GCCreateConcurrentThread_V1](#gcterminateconcurrentthread_v1_event)  
  
<a name="gcstart_v1_event"></a>   
## <a name="gcstart_v1-event"></a>Evento GCStart_V1  
 En la tabla siguiente se muestra la palabra clave y el nivel. (Para obtener más información, vea [CLR ETW Keywords and Levels](clr-etw-keywords-and-levels.md)).  
  
|Palabra clave para generar el evento|Nivel|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|Informativo (4)|  
  
 En la siguiente tabla se muestra la información del evento.  
  
|Evento|Id. de evento|Se genera cuando|  
|-----------|--------------|-----------------|  
|`GCStart_V1`|1|Se ha iniciado una recolección de elementos no utilizados.|  
  
 En la siguiente tabla se muestran los datos del evento.  
  
|Nombre de campo|Tipo de datos|DESCRIPCIÓN|  
|----------------|---------------|-----------------|  
|Número|win:UInt32|Recolección de elementos no utilizados número *n*.|  
|Profundidad|win:UInt32|Generación que se está recopilando.|  
|Reason|win:UInt32|¿Por qué se desencadenó la recolección de elementos no utilizados:<br /><br /> 0x0: asignación del montón de objetos pequeños.<br /><br /> 0x1: provocada.<br /><br /> 0x2: memoria insuficiente.<br /><br /> 0x3: vacía.<br /><br /> 0x4: asignación del montón de objetos grandes.<br /><br /> 0x5: espacio insuficiente (para montón de objetos pequeños).<br /><br /> 0x6: espacio insuficiente (para montón de objetos grandes).<br /><br /> 0x7: provocada pero no forzada como bloqueo.|  
|Type|win:UInt32|0x0: el bloqueo de la recolección de elementos no utilizados se produjo fuera de recolección de elementos no utilizados en segundo plano.<br /><br /> 0x1: recolección de elementos no utilizados en segundo plano.<br /><br /> 0x2: el bloqueo de la recolección de elementos no utilizados se produjo durante la recolección de elementos no utilizados en segundo plano.|  
|ClrInstanceID|win:UInt16|Identificador único para la instancia de CLR o CoreCLR.|  
  
 [Volver al principio](#top)  
  
<a name="gcend_v1_event"></a>   
## <a name="gcend_v1-event"></a>Evento GCEnd_V1  
 En la tabla siguiente se muestra la palabra clave y el nivel.  
  
|Palabra clave para generar el evento|Nivel|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|Informativo (4)|  
  
 En la siguiente tabla se muestra la información del evento.  
  
|Evento|Id. de evento|Se genera cuando|  
|-----------|--------------|-----------------|  
|`GCEnd_V1`|2|La recolección de elementos no utilizados ha finalizado.|  
  
 En la siguiente tabla se muestran los datos del evento.  
  
|Nombre de campo|Tipo de datos|DESCRIPCIÓN|  
|----------------|---------------|-----------------|  
|Número|win:UInt32|Recolección de elementos no utilizados número *n*.|  
|Profundidad|win:UInt32|Generación que se recopiló.|  
|ClrInstanceID|win:UInt16|Identificador único para la instancia de CLR o CoreCLR.|  
  
 [Volver al principio](#top)  
  
<a name="gcheapstats_v1_event"></a>   
## <a name="gcheapstats_v1-event"></a>Evento GCHeapStats_V1  
 En la tabla siguiente se muestra la palabra clave y el nivel.  
  
|Palabra clave para generar el evento|Nivel|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|Informativo (4)|  
  
 En la siguiente tabla se muestra la información del evento.  
  
|Evento|Id. de evento|DESCRIPCIÓN|  
|-----------|--------------|-----------------|  
|`GCHeapStats_V1`|4|Muestra las estadísticas del montón al final de cada recolección de elementos no utilizados.|  
  
 En la siguiente tabla se muestran los datos del evento.  
  
|Nombre de campo|Tipo de datos|DESCRIPCIÓN|  
|----------------|---------------|-----------------|  
|GenerationSize0|win:UInt64|Tamaño, en bytes, de la memoria de la generación 0.|  
|TotalPromotedSize0|win:UInt64|Número de bytes que se promueven de generación 0 a generación 1.|  
|GenerationSize1|win:UInt64|Tamaño, en bytes, de la memoria de la generación 1.|  
|TotalPromotedSize1|win:UInt64|Número de bytes que se promueven de generación 1 a generación 2.|  
|GenerationSize2|win:UInt64|Tamaño, en bytes, de la memoria de la generación 2.|  
|TotalPromotedSize2|win:UInt64|Número de bytes que sobrevivieron en la generación 2 después de la última recolección.|  
|GenerationSize3|win:UInt64|Tamaño, en bytes, del montón de objetos grandes.|  
|TotalPromotedSize3|win:UInt64|Número de bytes que sobrevivieron en el montón de objetos grandes después de la última recolección.|  
|FinalizationPromotedSize|win:UInt64|Tamaño total, en bytes, de los objetos que están listos para la finalización.|  
|FinalizationPromotedCount|win:UInt64|Número de objetos que están listos para la finalización.|  
|PinnedObjectCount|win:UInt32|Número de objetos anclados (inamovibles).|  
|SinkBlockCount|win:UInt32|Número de bloques de sincronización en uso.|  
|GCHandleCount|win:UInt32|Número de controles de recolección de elementos no utilizados en uso.|  
|ClrInstanceID|win:UInt16|Identificador único para la instancia de CLR o CoreCLR.|  
  
 [Volver al principio](#top)  
  
<a name="gccreatesegment_v1_event"></a>   
## <a name="gccreatesegment_v1-event"></a>Evento GCCreateSegment_V1  
 En la tabla siguiente se muestra la palabra clave y el nivel.  
  
|Palabra clave para generar el evento|Nivel|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|Informativo (4)|  
  
 En la siguiente tabla se muestra la información del evento.  
  
|Evento|Id. de evento|Se genera cuando|  
|-----------|--------------|-----------------|  
|`GCCreateSegment_V1`|5|Se ha creado un nuevo segmento de recopilación de elementos no utilizados. Además, si se habilita el seguimiento en un proceso que ya se está ejecutando, se genera este evento para cada segmento existente.|  
  
 En la siguiente tabla se muestran los datos del evento.  
  
|Nombre de campo|Tipo de datos|DESCRIPCIÓN|  
|----------------|---------------|-----------------|  
|Dirección|win:UInt64|Dirección del segmento.|  
|Tamaño|win:UInt64|Tamaño del segmento.|  
|Type|win:UInt32|0x0: montón de objetos pequeños.<br /><br /> 0x1: montón de objetos grandes.<br /><br /> 0x2: montón de solo lectura.|  
|ClrInstanceID|win:UInt16|Identificador único para la instancia de CLR o CoreCLR.|  
  
 Tenga en cuenta que el tamaño de los segmentos asignados por el recolector de elementos no utilizados es específico de la implementación y está sujeto a cambios en cualquier momento, incluso en las actualizaciones periódicas. La aplicación nunca debe realizar suposiciones sobre el tamaño de un sector determinado ni depender de él, y tampoco debe intentar configurar la cantidad de memoria disponible para las asignaciones de segmentos.  
  
 [Volver al principio](#top)  
  
<a name="gcfreesegment_v1_event"></a>   
## <a name="gcfreesegment_v1-event"></a>Evento GCFreeSegment_V1  
 En la tabla siguiente se muestra la palabra clave y el nivel.  
  
|Palabra clave para generar el evento|Nivel|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|Informativo (4)|  
  
 En la siguiente tabla se muestra la información del evento.  
  
|Evento|Id. de evento|Se genera cuando|  
|-----------|--------------|-----------------|  
|`GCFreeSegment_V1`|6|Se ha liberado un segmento de recolección de elementos no utilizados.|  
  
 En la siguiente tabla se muestran los datos del evento.  
  
|Nombre de campo|Tipo de datos|DESCRIPCIÓN|  
|----------------|---------------|-----------------|  
|Dirección|win:UInt64|Dirección del segmento.|  
|ClrInstanceID|win:UInt16|Identificador único para la instancia de CLR o CoreCLR.|  
  
 [Volver al principio](#top)  
  
<a name="gcrestarteebegin_v1_event"></a>   
## <a name="gcrestarteebegin_v1-event"></a>Evento GCRestartEEBegin_V1  
 En la tabla siguiente se muestra la palabra clave y el nivel.  
  
|Palabra clave para generar el evento|Nivel|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|Informativo (4)|  
  
 En la siguiente tabla se muestra la información del evento.  
  
|Evento|Id. de evento|Se genera cuando|  
|-----------|--------------|-----------------|  
|`GCRestartEEBegin_V1`|7|Ha comenzado la reanudación de la suspensión de Common Language Runtime.|  
  
 Sin datos del evento.  
  
 [Volver al principio](#top)  
  
<a name="gcrestarteeend_v1_event"></a>   
## <a name="gcrestarteeend_v1-event"></a>Evento GCRestartEEEnd_V1  
 En la tabla siguiente se muestra la palabra clave y el nivel.  
  
|Palabra clave para generar el evento|Nivel|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|Informativo (4)|  
  
 En la siguiente tabla se muestra la información del evento.  
  
|Evento|Id. de evento|Se genera cuando|  
|-----------|--------------|-----------------|  
|`GCRestartEEEnd_V1`|3|Ha finalizado la reanudación de la suspensión de Common Language Runtime.|  
  
 Sin datos del evento.  
  
 [Volver al principio](#top)  
  
<a name="gcsuspendee_v1_event"></a>   
## <a name="gcsuspendee_v1-event"></a>Evento GCSuspendEE_V1  
 En la tabla siguiente se muestra la palabra clave y el nivel.  
  
|Palabra clave para generar el evento|Nivel|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|Informativo (4)|  
  
 En la siguiente tabla se muestra la información del evento.  
  
|Evento|Id. de evento|Se genera cuando|  
|-----------|--------------|-----------------|  
|`GCSuspendEE_V1`|9|Inicio de la suspensión del motor de ejecución de la recolección de elementos no utilizados.|  
  
 En la siguiente tabla se muestran los datos del evento.  
  
|Nombre de campo|Tipo de datos|DESCRIPCIÓN|  
|----------------|---------------|-----------------|  
|Motivo|win:UInt16|0x0: otros.<br /><br /> 0x1: recolección de elementos no utilizados.<br /><br /> 0x2: cierre del dominio de aplicación.<br /><br /> 0x3: eliminación de código nativo.<br /><br /> 0x4: cierre.<br /><br /> 0x5: depurador.<br /><br /> 0x6: preparación para la recolección de elementos no utilizados.|  
|Recuento|win:UInt32|El recuento de GC en el momento. Normalmente, verá un evento Inicio de GC posterior después de esto, y su recuento será este recuento + 1 a medida que aumentamos el índice de GC durante una recolección de elementos no utilizados.|  
|ClrInstanceID|win:UInt16|Identificador único para la instancia de CLR o CoreCLR.|  
  
 [Volver al principio](#top)  
  
<a name="gcsuspendeeend_v1_event"></a>   
## <a name="gcsuspendeeend_v1-event"></a>Evento GCSuspendEE_V1  
 En la tabla siguiente se muestra la palabra clave y el nivel.  
  
|Palabra clave para generar el evento|Nivel|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|Informativo (4)|  
  
 En la siguiente tabla se muestra la información del evento.  
  
|Evento|Id. de evento|Se genera cuando|  
|-----------|--------------|-----------------|  
|`GCSuspendEEEnd_V1`|8|Final de la suspensión del motor de ejecución de la recolección de elementos no utilizados.|  
  
 Sin datos del evento.  
  
 [Volver al principio](#top)  
  
<a name="gcallocationtick_v2_event"></a>   
## <a name="gcallocationtick_v2-event"></a>Evento GCAllocationTick_V2  
 En la tabla siguiente se muestra la palabra clave y el nivel.  
  
|Palabra clave para generar el evento|Nivel|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|Informativo (4)|  
  
 En la siguiente tabla se muestra la información del evento.  
  
|Evento|Id. de evento|Se genera cuando|  
|-----------|--------------|-----------------|  
|`GCAllocationTick_V2`|10|Cada vez se asignan aproximadamente 100 KB.|  
  
 En la siguiente tabla se muestran los datos del evento.  
  
|Nombre de campo|Tipo de datos|DESCRIPCIÓN|  
|----------------|---------------|-----------------|  
|AllocationAmount|win:UInt32|Tamaño de la asignación, en bytes. Este valor es preciso para las asignaciones que son menores que la longitud de ULONG (4.294.967.295 bytes). Si la asignación es mayor, este campo contiene un valor truncado. Use `AllocationAmount64` para asignaciones muy grandes.|  
|AllocationKind|win:UInt32|0x0: asignación de objetos pequeños (la asignación está en un montón de objetos pequeños).<br /><br /> 0x1: asignación de objetos grandes (la asignación está en un montón de objetos grandes).|  
|ClrInstanceID|win:UInt16|Identificador único para la instancia de CLR o CoreCLR.|  
|AllocationAmount64|win:UInt64|Tamaño de la asignación, en bytes. Este valor es preciso para asignaciones muy grandes.|  
|TypeId|win:Pointer|Dirección de la MethodTable. Cuando durante este evento se asignaron varios tipos de objetos, esta es la dirección de la MethodTable que corresponde al último objeto asignado (es decir, el objeto que hizo que se supere el umbral de 100 KB).|  
|TypeName|win:UnicodeString|Nombre del tipo que se asignó. Cuando durante este evento se asignaron varios tipos de objetos, este es el tipo del último objeto asignado (es decir, el objeto que hizo que se supere el umbral de 100 KB).|  
|HeapIndex|win:UInt32|Montón al que se ha asignado el objeto. Este valor es 0 (cero) cuando se ejecuta con la recolección de elementos no utilizados de estación de trabajo.|  
  
 [Volver al principio](#top)  
  
<a name="gcfinalizersbegin_v1_event"></a>   
## <a name="gcfinalizersbegin_v1-event"></a>Evento GCFinalizersBegin_V1  
 En la tabla siguiente se muestra la palabra clave y el nivel.  
  
|Palabra clave para generar el evento|Nivel|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|Informativo (4)|  
  
 En la siguiente tabla se muestra la información del evento.  
  
|Evento|Id. de evento|Se genera cuando|  
|-----------|--------------|-----------------|  
|`GCFinalizersBegin_V1`|14|Inicio de los finalizadores en ejecución.|  
  
 Sin datos del evento.  
  
 [Volver al principio](#top)  
  
<a name="gcfinalizersend_v1_event"></a>   
## <a name="gcfinalizersend_v1-event"></a>Evento GCFinalizersEnd_V1  
 En la tabla siguiente se muestra la palabra clave y el nivel.  
  
|Palabra clave para generar el evento|Nivel|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|Informativo (4)|  
  
 En la siguiente tabla se muestra la información del evento.  
  
|Evento|Id. de evento|Se genera cuando|  
|-----------|--------------|-----------------|  
|`GCFinalizersEnd_V1`|13|Final de los finalizadores en ejecución.|  
  
 En la siguiente tabla se muestran los datos del evento.  
  
|Nombre de campo|Tipo de datos|DESCRIPCIÓN|  
|----------------|---------------|-----------------|  
|Número|win:UInt32|Número de finalizadores que se ejecutó.|  
|ClrInstanceID|win:UInt16|Identificador único para la instancia de CLR o CoreCLR.|  
  
 [Volver al principio](#top)  
  
<a name="gccreateconcurrentthread_v1_event"></a>   
## <a name="gccreateconcurrentthread_v1-event"></a>Evento GCCreateConcurrentThread_V1  
 En la tabla siguiente se muestra la palabra clave y el nivel.  
  
|Palabra clave para generar el evento|Nivel|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|Informativo (4)|  
|`ThreadingKeyword` (0x10000)|Informativo (4)|  
  
 En la siguiente tabla se muestra la información del evento.  
  
|Evento|Id. de evento|Se genera cuando|  
|-----------|--------------|-----------------|  
|`GCCreateConcurrentThread_V1`|11|El subproceso de recolección de elementos no utilizados simultánea se creó.|  
  
 Sin datos del evento.  
  
 [Volver al principio](#top)  
  
<a name="gcterminateconcurrentthread_v1_event"></a>   
## <a name="gcterminateconcurrentthread_v1-event"></a>Evento GCCreateConcurrentThread_V1  
 En la tabla siguiente se muestra la palabra clave y el nivel.  
  
|Palabra clave para generar el evento|Nivel|  
|-----------------------------------|-----------|  
|`GCKeyword` (0x1)|Informativo (4)|  
|`ThreadingKeyword` (0x10000)|Informativo (4)|  
  
 En la siguiente tabla se muestra la información del evento.  
  
|Evento|Id. de evento|Se genera cuando|  
|-----------|--------------|-----------------|  
|`GCTerminateConcurrentThread_V1`|12|El subproceso de recolección de elementos no utilizados simultánea finalizó.|  
  
 Sin datos del evento.  
  
## <a name="see-also"></a>Vea también

- [CLR ETW Events (Eventos ETW de CLR)](clr-etw-events.md)
