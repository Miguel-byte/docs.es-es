---
title: <Namespace>Elemento (.NET Native)
ms.date: 03/30/2017
ms.assetid: 57c614e5-18a9-4e87-bfd5-d0fe3396a192
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7be004776d2a2fd3b4c41fb21b3ac244946f2166
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049427"
---
# <a name="namespace-element-net-native"></a>\<Elemento namespace > (.NET Native)
Aplica la de reflexión en tiempo de ejecución a todos los tipos en un espacio de nombres especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<Namespace Name="namespace_name"   
           Activate="policy_type"   
           Browse="policy_type"  
           Dynamic="policy_setting"  
           Serialize="policy_setting"  
           DataContractSerializer="policy_setting"  
           DataContractJsonSerializer="policy_setting"  
           XmlSerializer="policy_setting"  
           MarshalObject="policy_setting"  
           MarshalDelegate="policy_setting"  
           MarshalStructure="policy_setting" />  
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Tipo de atributo|DESCRIPCIÓN|  
|---------------|--------------------|-----------------|  
|`Name`|General|Atributo necesario. Especifica el nombre del espacio de nombres.|  
|`Activate`|Reflexión|Atributo opcional. Controla el acceso en tiempo de ejecución a los constructores para permitir la activación de instancias.|  
|`Browse`|Reflexión|Atributo opcional. Controla la consulta para obtener información sobre los elementos de programa, pero no permite el acceso en tiempo de ejecución.|  
|`Dynamic`|Reflexión|Atributo opcional. Controla el acceso en tiempo de ejecución a todos los miembros de tipo (incluidos constructores, métodos, campos, propiedades y eventos) para permitir la programación dinámica.|  
|`Serialize`|Serialización|Atributo opcional. Controla el acceso en tiempo de ejecución a constructores, campos y propiedades para permitir que bibliotecas como el serializador JSON Newtonsoft puedan serializar y deserializar instancias de tipo.|  
|`DataContractSerializer`|Serialización|Atributo opcional. Controla la directiva de serialización que usa la clase <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType>.|  
|`DataContractJsonSerializer`|Serialización|Atributo opcional. Controla la directiva de serialización JSON que usa la clase <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType>.|  
|`XmlSerializer`|Serialización|Atributo opcional. Controla la directiva de serialización XML que usa la clase <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType>.|  
|`MarshalObject`|Interop|Atributo opcional. Controla la directiva de serialización de tipos de referencia a Windows Runtime y COM.|  
|`MarshalDelegate`|Interop|Atributo opcional. Controla la directiva de serialización de tipos de delegado como punteros de función a código nativo.|  
|`MarshalStructure`|Interop|Atributo opcional. Controla la directiva para calcular referencias de estructuras a código nativo.|  
  
## <a name="name-attribute"></a>Name (atributo)  
  
|Valor|DESCRIPCIÓN|  
|-----------|-----------------|  
|*namespace_name*|El espacio de nombres. Si \<Namespace> es un elemento secundario de un elemento [\<Application>](application-element-net-native.md), [\<Library>](library-element-net-native.md) o [\<Assembly>](assembly-element-net-native.md), *namespace_name* debe ser un nombre de espacio de nombres completo. Si \<Namespace> es un elemento secundario de otro elemento \<Namespace>, *namespace_name* debe ser un nombre de espacio de nombres relativo.|  
  
## <a name="all-other-attributes"></a>Resto de atributos  
  
|Valor|DESCRIPCIÓN|  
|-----------|-----------------|  
|*policy_setting*|La configuración que se aplica a este tipo de directiva para todos los tipos del espacio de nombres. Los valores posibles son `All`, `Auto`, `Excluded`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal` y `Required All`. Para obtener más información, vea [Runtime Directive Policy Settings](runtime-directive-policy-settings.md) (Configuración de directiva de la directiva en tiempo de ejecución).|  
  
### <a name="child-elements"></a>Elementos secundarios  
  
|Elemento|DESCRIPCIÓN|  
|-------------|-----------------|  
|`<Namespace>`|Aplica la directiva de reflexión en tiempo de ejecución a todos los tipos en un espacio de nombres primario.|  
|[\<Type>](type-element-net-native.md)|Aplica la directiva de reflexión a un tipo.|  
|[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|Aplica la directiva de reflexión a un tipo genérico construido.|  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|DESCRIPCIÓN|  
|-------------|-----------------|  
|[\<Application>](application-element-net-native.md)|Sirve de contenedor de los tipos y miembros de tipo de la aplicación cuyos metadatos están disponibles para la reflexión en tiempo de ejecución. El elemento [\<Application>](application-element-net-native.md) puede tener cero, uno o más elementos [\<Assembly>](assembly-element-net-native.md).|  
|[\<Assembly>](assembly-element-net-native.md)|Aplica la directiva de reflexión en tiempo de ejecución a todos los tipos en un ensamblado especificado.|  
|[\<Library>](library-element-net-native.md)|Define el ensamblado que contiene los tipos y miembros de tipo cuyos metadatos están disponibles para la reflexión en tiempo de ejecución. El elemento [\<Library>](library-element-net-native.md) puede tener cero o un elemento [\<Assembly>](assembly-element-net-native.md).|  
|`<Namespace>`|Aplica la directiva de reflexión a todos los tipos en un espacio de nombres primario.|  
  
## <a name="remarks"></a>Comentarios  
 Los atributos `Activate`, `Browse`, `Dynamic` y `Serialize` son opcionales. Si ninguno está presente, el elemento `<Namespace>` solo actúa como contenedor para los elementos secundarios. Si están presentes, el elemento `<Namespace>` aplica la directiva de reflexión en tiempo de ejecución a todos los tipos del espacio de nombres especificado.  
  
 Cuando es un elemento secundario del elemento [\<Assembly>](assembly-element-net-native.md), el elemento `<Namespace>` reemplaza la directiva de reflexión en tiempo de ejecución definida por el elemento [\<Assembly>](assembly-element-net-native.md).  
  
## <a name="see-also"></a>Vea también

- [Runtime Directive Policy Settings](runtime-directive-policy-settings.md) (Configuración de directiva de la directiva en tiempo de ejecución)
- [Runtime Directives (rd.xml) Configuration File Reference (Referencia del archivo de configuración de directivas en tiempo de ejecución (rd.xml))](runtime-directives-rd-xml-configuration-file-reference.md)
- [Runtime Directive Elements (Elementos de directivas en tiempo de ejecución)](runtime-directive-elements.md)
