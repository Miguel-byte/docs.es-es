---
title: MDA de dirtyCastAndCallOnInterface
ms.date: 03/30/2017
helpviewer_keywords:
- managed debugging assistants (MDAs), early bound calls AutoDispatch
- dispatch-only mode
- dirtyCastAndCallOnInterface
- early-bound managed classes
- early bound calls on AutoDispatch
- MDAs (managed debugging assistants), early bound calls AutoDispatch
- EarlyBoundCallOnAutorDispatchClassInteface MDA
ms.assetid: aa388ed3-7e3d-48ea-a0b5-c47ae19cec38
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6ac43f6b92198fec03e722b6cf5e12b86df6f4b8
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052865"
---
# <a name="dirtycastandcalloninterface-mda"></a>MDA de dirtyCastAndCallOnInterface
El Asistente para la depuración administrada (MDA) `dirtyCastAndCallOnInterface` se activa cuando se intenta realizar una llamada enlazada en tiempo de compilación a través de una vtable en una interfaz de clase que se ha marcado solo como enlazada en tiempo de ejecución.  
  
## <a name="symptoms"></a>Síntomas  
 Una aplicación produce una infracción de acceso o tiene un comportamiento inesperado cuando se realiza una llamada enlazada en tiempo de compilación a CLR a través de COM.  
  
## <a name="cause"></a>Causa  
 El código intenta realizar una llamada enlazada en tiempo de compilación a través de una vtable mediante una interfaz de clase que es solo enlazada en tiempo de ejecución. Tenga en cuenta que las interfaces de clase predeterminadas se identifican solo como enlazadas en tiempo de ejecución. También pueden identificarse como enlazadas en tiempo de ejecución cuando el atributo <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> tiene un valor <xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDispatch> (`[ClassInterface(ClassInterfaceType.AutoDispatch)]`).  
  
## <a name="resolution"></a>Resolución  
 La solución recomendada es definir una interfaz explícita para que COM la use y hacer que los clientes COM llamen a través de esta interfaz en lugar de la interfaz de clase que se genera automáticamente. Como alternativa, la llamada desde COM se puede transformar en una llamada enlazada en tiempo de ejecución mediante `IDispatch`.  
  
 Por último, es posible identificar la clase como <xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDual> (`[ClassInterface(ClassInterfaceType.AutoDual)]`) para permitir que se realicen llamadas enlazadas en tiempo de compilación desde COM; sin embargo, se desaconseja usar <xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDual> debido a las limitaciones del control de versiones descritas en <xref:System.Runtime.InteropServices.ClassInterfaceAttribute>.  
  
## <a name="effect-on-the-runtime"></a>Efecto en el Runtime  
 Este MDA no tiene ningún efecto en el CLR. Solo notifica datos sobre las llamadas enlazadas en tiempo de compilación en interfaces enlazadas en tiempo de ejecución.  
  
## <a name="output"></a>Resultados  
 El nombre del método o el nombre del campo al que se va a acceder mediante enlace en tiempo de compilación.  
  
## <a name="configuration"></a>Configuración  
  
```xml  
<mdaConfig>  
  <assistants>  
    <dirtyCastAndCallOnInterface />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.Runtime.InteropServices.ClassInterfaceAttribute>
- [Diagnosing Errors with Managed Debugging Assistants (Diagnóstico de errores con asistentes para la depuración administrada)](diagnosing-errors-with-managed-debugging-assistants.md)
