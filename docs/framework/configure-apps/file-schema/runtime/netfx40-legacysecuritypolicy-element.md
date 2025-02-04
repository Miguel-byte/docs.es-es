---
title: Elemento <NetFx40_LegacySecurityPolicy>
ms.date: 03/30/2017
helpviewer_keywords:
- <NetFx40_LegacySecurityPolicy> element
- NetFx40_LegacySecurityPolicy element
ms.assetid: 07132b9c-4a72-4710-99d7-e702405e02d4
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2cd6f937811ae503dd4de7ff989510c4eb8b8933
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252440"
---
# <a name="netfx40_legacysecuritypolicy-element"></a>\<NetFx40_LegacySecurityPolicy >, elemento

Especifica si el runtime usa la directiva de seguridad de acceso al código (CAS) heredada.

[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<> en tiempo de ejecución**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<> NetFx40_LegacySecurityPolicy**  

## <a name="syntax"></a>Sintaxis

```xml
<NetFx40_LegacySecurityPolicy
   enabled="true|false"/>
```

## <a name="attributes-and-elements"></a>Atributos y elementos

En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.

### <a name="attributes"></a>Atributos

|Atributo|DESCRIPCIÓN|
|---------------|-----------------|
|`enabled`|Atributo necesario.<br /><br /> Especifica si el Runtime usa una directiva CAS heredada.|

## <a name="enabled-attribute"></a>Atributo enabled

|Valor|DESCRIPCIÓN|
|-----------|-----------------|
|`false`|El runtime no utiliza la Directiva CAS heredada. Este es el valor predeterminado.|
|`true`|El Runtime usa una directiva CAS heredada.|

### <a name="child-elements"></a>Elementos secundarios

Ninguno.

### <a name="parent-elements"></a>Elementos primarios

|Elemento|DESCRIPCIÓN|
|-------------|-----------------|
|`configuration`|Elemento raíz de cada archivo de configuración usado por las aplicaciones de Common Language Runtime y .NET Framework.|
|`runtime`|Contiene información sobre las opciones de inicialización del motor en tiempo de ejecución.|

## <a name="remarks"></a>Comentarios

En la versión 3,5 de .NET Framework y versiones anteriores, la Directiva CAS está siempre en vigor. En el .NET Framework 4, la Directiva de CAS debe estar habilitada.

La Directiva CAS es específica de la versión. Las directivas de CA personalizadas que existen en versiones anteriores del .NET Framework deben reespecificarse en el .NET Framework 4.

Aplicar el `<NetFx40_LegacySecurityPolicy>` elemento a un ensamblado de .NET Framework 4 no afecta al [código transparente en seguridad](../../../misc/security-transparent-code.md); las reglas de transparencia se siguen aplicando.

> [!IMPORTANT]
> Aplicar el `<NetFx40_LegacySecurityPolicy>` elemento puede dar lugar a penalizaciones de rendimiento significativas para los ensamblados de imagen nativa creados por el [generador de imágenes nativas (Ngen. exe)](../../../tools/ngen-exe-native-image-generator.md) que no están instalados en la [caché global de ensamblados](../../../app-domains/gac.md). La degradación del rendimiento se debe a la incapacidad del tiempo de ejecución para cargar los ensamblados como imágenes nativas cuando se aplica el atributo, lo que da lugar a que se carguen como ensamblados Just-in-Time.

> [!NOTE]
> Si especifica una versión de .NET Framework de destino anterior a la .NET Framework 4 en la configuración del proyecto para el proyecto de Visual Studio, se habilitará la Directiva de CAS, incluidas las directivas CA personalizadas que haya especificado para esa versión. Sin embargo, no podrá usar los nuevos tipos y miembros de .NET Framework 4. También puede especificar una versión anterior del .NET Framework mediante el [ \<elemento supportedRuntime >](../startup/supportedruntime-element.md) en el esquema de configuración de inicio en el [archivo de configuración](../../index.md)de la aplicación.

> [!NOTE]
> La sintaxis del archivo de configuración distingue mayúsculas de minúsculas. Debe utilizar la sintaxis que se proporciona en las secciones sintaxis y ejemplo.

## <a name="configuration-file"></a>Archivo de configuración

Este elemento solo se puede usar en el archivo de configuración de la aplicación.

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se muestra cómo habilitar la Directiva CAS heredada para una aplicación.

```xml
<configuration>
   <runtime>
      <NetFx40_LegacySecurityPolicy enabled="true"/>
   </runtime>
</configuration>
```

## <a name="see-also"></a>Vea también

- [Esquema de la configuración de Common Language Runtime](index.md)
- [Esquema de los archivos de configuración](../index.md)
