---
title: Elemento <remove> para bypasslist (configuración de red)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy/bypasslist/remove
- http://schemas.microsoft.com/.NetConfiguration/v2.0#remove
helpviewer_keywords:
- <bypasslist>, remove element
- remove element, bypasslist
- bypasslist, remove element
- remove element, bypasslist
ms.assetid: 61dcfb4a-e3d9-4abf-a2cd-7d685fe2f64b
ms.openlocfilehash: 97b49a8a520d6a4f72945366874991d2deb18710
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2019
ms.locfileid: "71697891"
---
# <a name="remove-element-for-bypasslist-network-settings"></a>\<remove > elemento para BypassList (configuración de red)

Quita una dirección IP o un nombre DNS de la lista de omisión de proxy.

[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **@no__t -4System. net >** ](system-net-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t-2 @ no__t-3[ **\<defaultProxy >** ](defaultproxy-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t-2 @ no__t-3 @ no__t-4 @ no__t-5[ **\<bypasslist >** ](bypasslist-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t-2 @ no__t-3 @ no__t-4 @ no__t-5 @ no__t-6 @ no__t-7 **\<remove >**  

## <a name="syntax"></a>Sintaxis

```xml
<remove
  address="regular expression"
/>
```

## <a name="attributes-and-elements"></a>Atributos y elementos

En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.

### <a name="attributes"></a>Atributos

|**Attribute**|**Descripción**|
|-------------------|---------------------|
|`address`|Expresión regular que describe una dirección IP o un nombre DNS.|

### <a name="child-elements"></a>Elementos secundarios

Ninguno.

### <a name="parent-elements"></a>Elementos primarios

|**Element**|**Descripción**|
|-----------------|---------------------|
|[bypasslist](bypasslist-element-network-settings.md)|Proporciona un conjunto de expresiones regulares que describen las direcciones que no utilizan un proxy.|

## <a name="remarks"></a>Comentarios

El elemento `remove` quita las expresiones regulares que describen las direcciones IP o los nombres de servidor DNS de la lista de direcciones que omiten un servidor proxy. Las direcciones se definieron anteriormente en el archivo de configuración o en un nivel superior en la jerarquía de configuración.

El valor del atributo `address` debe ser una expresión regular que describa un conjunto de direcciones IP o nombres de host.

Para obtener más información acerca de las expresiones regulares, vea. [.NET Framework expresiones regulares](../../../../standard/base-types/regular-expressions.md).

## <a name="configuration-files"></a>Archivos de configuración

Este elemento se puede usar en el archivo de configuración de la aplicación o en el archivo de configuración del equipo (Machine.config).

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se quita cualquier definición anterior del dominio adventure-works.com y, a continuación, se agrega el dominio contoso.com a la lista de omisiones.

```xml
<configuration>
  <system.net>
    <defaultProxy>
      <bypasslist>
        <remove address="[a-z]+\.adventure-works\.com$" />
        <add address="[a-z]+\.contoso\.com$" />
      </bypasslist>
    </defaultProxy>
  </system.net>
</configuration>
```

## <a name="see-also"></a>Vea también

- <xref:System.Net.WebProxy?displayProperty=nameWithType>
- [Esquema de la configuración de red](index.md)
