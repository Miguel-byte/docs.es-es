---
title: MDA de pInvokeStackImbalance
ms.date: 03/30/2017
helpviewer_keywords:
- signatures, platform invoke
- stack depth
- platform invoke stack imbalance
- MDAs (managed debugging assistants), platform invoke
- platform invoke, run-time errors
- PInvokeStackImbalance MDA
- managed debugging assistants (MDAs), platform invoke
ms.assetid: 34ddc6bd-1675-4f35-86aa-de1645d5c631
author: mairaw
ms.author: mairaw
ms.openlocfilehash: dc4a48c79fc39b12f8231bd913b4ca8970c0f46f
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052366"
---
# <a name="pinvokestackimbalance-mda"></a>MDA de PInvokeStackImbalance

El `PInvokeStackImbalance` Asistente para la depuración administrada (MDA) se activa cuando CLR detecta que la profundidad de la pila después de una llamada de invocación de plataforma no coincide con la profundidad de pila <xref:System.Runtime.InteropServices.DllImportAttribute> esperada, dada la Convención de llamada especificada en el atributo y el parámetro Declaración de los parámetros en la firma administrada.

El MDA `PInvokeStackImbalance` solo se implementa para plataformas de x86 de 32 bits.

> [!NOTE]
> El `PInvokeStackImbalance` MDA está deshabilitado de forma predeterminada. En Visual Studio 2017, el `PInvokeStackImbalance` MDA aparece en la **lista asistentes para la depuración administrada** en el cuadro de diálogo **configuración de excepciones** (que se muestra al seleccionar**ventanas**  >   >  **de depuración). Configuración de excepciones**). Sin embargo, al activar o desactivar la casilla **interrumpir cuando se produce** no se habilita o deshabilita el MDA; solo controla si Visual Studio produce una excepción cuando se activa el MDA.

## <a name="symptoms"></a>Síntomas

Una aplicación se encuentra con una infracción de acceso o daños en la memoria cuando se realiza una llamada de invocación de plataforma o después de realizar una.

## <a name="cause"></a>Causa

La firma administrada de la llamada de invocación de plataforma podría no coincidir con la firma no administrada del método al que se llama.  Esta falta de coincidencia puede deberse a que la firma administrada no declara el número correcto de parámetros o no especifica el tamaño adecuado para los parámetros.  El MDA también puede activarse porque la convención de llamada, posiblemente especificada por el atributo <xref:System.Runtime.InteropServices.DllImportAttribute>, no coincide con la convención de llamada no administrada.

## <a name="resolution"></a>Resolución

Revise la firma de la invocación de plataforma administrada y la convención de llamada para confirmar que coincide con la firma y la convención de llamada del destino nativo.  Pruebe a especificar explícitamente la convención de llamada en ambos lados, administrado y no administrado. También es posible, aunque no probable, que la función no administrada haya desequilibrado la pila por algún otro motivo, por ejemplo, un error en el compilador no administrado.

## <a name="effect-on-the-runtime"></a>Efecto en el Runtime

Obliga a todas las llamadas de invocación de plataforma a tomar la ruta de acceso no optimizada en CLR.

## <a name="output"></a>Resultados

El mensaje del MDA indica el nombre de la llamada al método de invocación de plataforma que causa el desequilibrio de la pila. Un mensaje de ejemplo de una llamada de invocación de plataforma en el método `SampleMethod` es:

**Una llamada a la función PInvoke ' SampleMethod ' ha desequilibrado la pila. Probablemente, esto se debe a que la firma de PInvoke administrada no coincide con la firma de destino no administrada. Compruebe que la Convención de llamada y los parámetros de la firma PInvoke coinciden con la firma no administrada de destino.**

## <a name="configuration"></a>Configuración

```xml
<mdaConfig>
  <assistants>
    <pInvokeStackImbalance />
  </assistants>
</mdaConfig>
```

## <a name="see-also"></a>Vea también

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [Diagnosing Errors with Managed Debugging Assistants (Diagnóstico de errores con asistentes para la depuración administrada)](diagnosing-errors-with-managed-debugging-assistants.md)
- [Serialización de interoperabilidad](../interop/interop-marshaling.md)
