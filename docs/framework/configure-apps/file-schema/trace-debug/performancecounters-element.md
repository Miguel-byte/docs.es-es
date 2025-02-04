---
title: <performanceCounters> (Elemento)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/performanceCounters
- http://schemas.microsoft.com/.NetConfiguration/v2.0#performanceCounters
helpviewer_keywords:
- performanceCounters element
- <performanceCounters> element
ms.assetid: a71f605b-c7d9-4501-a5c3-abcbb964a43f
ms.openlocfilehash: f52fdb2d5b0b7911de63f96663e70735d2f2496c
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2019
ms.locfileid: "71697155"
---
# <a name="performancecounters-element"></a>\<performanceCounters >, elemento

Especifica el tamaño de la memoria global que comparten los contadores de rendimiento.

[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **\<System. diagnostics >** ](system-diagnostics-element.md)  
&nbsp; @ no__t-1 @ no__t-2 @ no__t-3 **\<performanceCounters >**  

## <a name="syntax"></a>Sintaxis

```xml
<performanceCounters filemappingsize="524288" />
```

## <a name="attributes-and-elements"></a>Atributos y elementos

En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.

### <a name="attributes"></a>Atributos

|Atributo|Descripción|
|---------------|-----------------|
|filemappingsize|Atributo necesario.<br /><br /> Especifica el tamaño, en bytes, de la memoria global compartida por los contadores de rendimiento. El valor predeterminado es 524288.|

### <a name="child-elements"></a>Elementos secundarios

Ninguno.

### <a name="parent-elements"></a>Elementos primarios

|Elemento|Descripción|
|-------------|-----------------|
|`Configuration`|Elemento raíz de cada archivo de configuración usado por las aplicaciones de Common Language Runtime y .NET Framework.|
|`system.diagnostics`|Especifica el elemento raíz de la sección de configuración de ASP.NET.|

## <a name="remarks"></a>Comentarios

Los contadores de rendimiento usan un archivo asignado a la memoria, o la memoria compartida, para publicar datos de rendimiento.  El tamaño de la memoria compartida determina el número de instancias que se pueden usar a la vez.  Hay dos tipos de memoria compartida: memoria compartida global y memoria compartida independiente.  Todas las categorías de contadores de rendimiento que se instalan con las .NET Framework versiones 1,0 o 1,1 utilizan la memoria compartida global.  Las categorías de contadores de rendimiento instaladas con la .NET Framework versión 2,0 usan una memoria compartida independiente, y cada categoría de contador de rendimiento tiene su propia memoria.

El tamaño de la memoria compartida global solo se puede establecer con un archivo de configuración.  El tamaño predeterminado es 524.288 BSÍ, el tamaño máximo es de 33.554.432 bytes y el tamaño mínimo es de 32.768 bytes.  Dado que todos los procesos y las categorías comparten la memoria compartida global, el primer creador especifica el tamaño.  Si define el tamaño en el archivo de configuración de la aplicación, ese tamaño solo se utiliza si la aplicación es la primera aplicación que hace que se ejecuten los contadores de rendimiento.  Por lo tanto, la ubicación correcta para especificar el valor de `filemappingsize` es el archivo Machine. config.  Los contadores de rendimiento individuales no pueden liberar memoria en la memoria compartida global, por lo que finalmente se agota la memoria compartida global si se crea un gran número de instancias de contador de rendimiento con nombres diferentes.

Para el tamaño de la memoria compartida independiente, se hace referencia primero al valor DWORD FileMappingSize en la clave del registro HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services @ no__t-0 *\<category nombre >* \Performance, seguido del valor se especifica para la memoria compartida global en el archivo de configuración. Si el valor FileMappingSize no existe, el tamaño de la memoria compartida independiente se establece en un cuarto (1/4) la configuración global del archivo de configuración.

## <a name="see-also"></a>Vea también

- <xref:System.Diagnostics.PerformanceCounter>
- <xref:System.Diagnostics.PerformanceCounterCategory>
- <xref:System.Diagnostics.PerformanceCounter.InstanceLifetime%2A>
- <xref:System.Diagnostics.PerformanceCounterInstanceLifetime>
