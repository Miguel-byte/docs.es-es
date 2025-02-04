---
title: MDA de gcUnmanagedToManaged
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), garbage collection
- GC unmanaged to managed
- transitioning threads unmanaged to managed code
- GcUnmanagedToManaged MDA
- threading [.NET Framework], garbage collection
- managed debugging assistants (MDAs), garbage collection
- threading [.NET Framework], managed debugging assistants
- garbage collection, run-time errors
- unmanaged to managed garbage collection
ms.assetid: 103eb3a3-1cf0-4406-8a9a-a7798fdc22d1
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 1679f87276262a08f5717ea81d263f4600542971
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052760"
---
# <a name="gcunmanagedtomanaged-mda"></a>MDA de gcUnmanagedToManaged
El asistente para la depuración administrada (MDA) `gcUnmanagedToManaged` produce una recolección de elementos no utilizados siempre que un subproceso realice la transición de código no administrado a administrado.  
  
## <a name="symptoms"></a>Síntomas  
 Una aplicación que ejecute componentes de usuario no administrados con la invocación de plataforma y COM genera una infracción de acceso no determinista en CLR.  
  
## <a name="cause"></a>Causa  
 Si una aplicación está ejecutando componentes de usuario no administrados, dichos componentes podrían haber dañado el montón de recolección de elementos no utilizados. Esto provoca una infracción de acceso en CLR cuando el recolector de elementos no utilizados intenta desplazarse por el gráfico de objetos.  
  
## <a name="resolution"></a>Resolución  
 Al habilitar este asistente, se reduce el tiempo entre el momento en que el componente no administrado daña la pila de recolección de elementos no utilizados y el momento en que se produce la infracción de acceso al forzar que tenga lugar una recolección antes de cada transición administrada.  
  
## <a name="effect-on-the-runtime"></a>Efecto en el Runtime  
 Produce una recolección de elementos no utilizados siempre que un subproceso realice la transición de código no administrado a administrado.  
  
## <a name="output"></a>Resultados  
 Este MDA no produce ninguna salida.  
  
## <a name="configuration"></a>Configuración  
  
```xml  
<mdaConfig>  
  <assistants>  
    <gcUnmanagedToManaged/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [Diagnosing Errors with Managed Debugging Assistants (Diagnóstico de errores con asistentes para la depuración administrada)](diagnosing-errors-with-managed-debugging-assistants.md)
- [gcManagedToUnmanaged](gcmanagedtounmanaged-mda.md)
- [Serialización de interoperabilidad](../interop/interop-marshaling.md)
