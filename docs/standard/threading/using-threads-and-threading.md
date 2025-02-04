---
title: Uso de subprocesos y subprocesamiento
ms.date: 08/08/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- threading [.NET Framework], about threading
- managed threading
ms.assetid: 9b5ec2cd-121b-4d49-b075-222cf26f2344
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d23a12ff92202ace69cb80ff59d6afcb5d8f8243
ms.sourcegitcommit: ffd7dd79468a81bbb0d6449f6d65513e050c04c4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2019
ms.locfileid: "65960378"
---
# <a name="using-threads-and-threading"></a>Uso de subprocesos y subprocesamiento

Con .NET, se pueden escribir aplicaciones que realicen varias operaciones al mismo tiempo. Las operaciones con la posibilidad de contener otras operaciones se pueden ejecutar en subprocesos independientes, lo que se conoce como *multithreading* o *subprocesamiento libre*.  
  
Las aplicaciones que usan multithreading responden mejor a la entrada del usuario, ya que la interfaz de usuario permanece activa mientras las tareas que requieren un uso intensivo del procesador se ejecutan en subprocesos separados. El multithreading también es útil cuando se crean aplicaciones escalables, porque se pueden agregar subprocesos a medida que aumenta la carga de trabajo.

> [!NOTE]
> Si necesita más control sobre el comportamiento de los subprocesos de la aplicación, puede administrar los subprocesos por su cuenta. Pero a partir de .NET Framework 4, la programación multiproceso se ha simplificado significativamente con las clases <xref:System.Threading.Tasks.Parallel?displayProperty=nameWithType> y <xref:System.Threading.Tasks.Task?displayProperty=nameWithType>, [Parallel LINQ (PLINQ)](../parallel-programming/parallel-linq-plinq.md), clases de colecciones simultáneas nuevas en el espacio de nombres <xref:System.Collections.Concurrent?displayProperty=nameWithType> y un nuevo modelo de programación basado en el concepto de tareas en lugar de subprocesos. Para obtener más información, vea [Programación en paralelo](../parallel-programming/index.md) y [Biblioteca de procesamiento paralelo basado en tareas (TPL)](../parallel-programming/task-parallel-library-tpl.md).

## <a name="how-to-create-and-start-a-new-thread"></a>Procedimiento para crear e iniciar un subproceso nuevo

Un subproceso se crea mediante la creación de una instancia de la clase <xref:System.Threading.Thread?displayProperty=nameWithType> y proporcionando al constructor el nombre del método que se quiere ejecutar en un subproceso nuevo. Para iniciar un subproceso creado, llame al método <xref:System.Threading.Thread.Start%2A?displayProperty=nameWithType>. Para obtener más información y ejemplos, vea el artículo [Creación de subprocesos y análisis de los datos en el inicio](creating-threads-and-passing-data-at-start-time.md) y la referencia de la API <xref:System.Threading.Thread>.

## <a name="how-to-stop-a-thread"></a>Procedimiento para detener un subproceso

Para terminar la ejecución de un subproceso, use el método <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>. Ese método genera una excepción <xref:System.Threading.ThreadAbortException> en el subproceso en el que se invoca. Para obtener más información, vea [Destruir subprocesos](destroying-threads.md).

A partir de .NET Framework 4, se puede usar <xref:System.Threading.CancellationToken?displayProperty=nameWithType> para cancelar un subproceso de forma cooperativa. Para más información, consulte [Cancelación de subprocesos administrados](cancellation-in-managed-threads.md).

Use el método <xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType> para hacer que el subproceso que realiza la llamada espere a la finalización del subproceso en el que se invoca el método.

## <a name="how-to-pause-or-interrupt-a-thread"></a>Procedimiento para pausar o interrumpir un subproceso

El método <xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType> se usa para pausar el subproceso actual durante un período de tiempo especificado. Un subproceso bloqueado se puede interrumpir mediante una llamada al método <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType>. Para obtener más información, vea [Pausa e interrupción de subprocesos](pausing-and-resuming-threads.md).

## <a name="thread-properties"></a>Propiedades de subproceso

En la tabla siguiente se muestran algunas de las propiedades de <xref:System.Threading.Thread>:  
  
|Propiedad.|Descripción|  
|--------------|-----------|  
|<xref:System.Threading.Thread.IsAlive%2A>|Devuelve `true` si el subproceso se ha iniciado y todavía no ha terminado con normalidad o se ha anulado.|  
|<xref:System.Threading.Thread.IsBackground%2A>|Obtiene o establece un valor booleano que indica si un subproceso es un subproceso en segundo plano. Los subprocesos en segundo plano son como los subprocesos en primer plano, con la diferencia de que un subproceso en segundo plano no impide que un proceso se detenga. Una vez que se hayan detenido todos los subprocesos en primer plano que pertenecen a un proceso, Common Language Runtime finaliza el proceso mediante una llamada al método <xref:System.Threading.Thread.Abort%2A> en los subprocesos en segundo plano que continúan activos. Para obtener más información, vea [Subprocesos de primer y segundo plano](foreground-and-background-threads.md).|  
|<xref:System.Threading.Thread.Name%2A>|Obtiene o establece el nombre de un subproceso. Suele usarse para detectar subprocesos individuales durante la depuración.|  
|<xref:System.Threading.Thread.Priority%2A>|Obtiene o establece un valor <xref:System.Threading.ThreadPriority> que el sistema operativo usa para dar prioridad a la programación de subprocesos. Para obtener más información, vea [Planear subprocesos](scheduling-threads.md) y la referencia de <xref:System.Threading.ThreadPriority>.|  
|<xref:System.Threading.Thread.ThreadState%2A>|Obtiene un valor <xref:System.Threading.ThreadState> que contiene los estados actuales de un subproceso.|  

## <a name="see-also"></a>Vea también

- <xref:System.Threading.Thread?displayProperty=nameWithType>
- [Subprocesos y subprocesamiento](threads-and-threading.md)
- [Programación en paralelo](../parallel-programming/index.md)
