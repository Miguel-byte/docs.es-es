---
title: <Application>Elemento (.NET Native)
ms.date: 03/30/2017
ms.assetid: b4e9b37a-059b-4076-8f56-cb3f9cef0cd9
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2183a64f4e30a5188940abd5108a7ca1bddfe120
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049932"
---
# <a name="application-element-net-native"></a>\<Elemento Application > (.NET Native)
Sirve de contenedor de los tipos y miembros de tipo de la aplicación cuyos metadatos están disponibles para la reflexión en tiempo de ejecución y aplica la directiva de reflexión en tiempo de ejecución a todos los elementos de programa en una aplicación.  
  
 Elemento \<Directives>  
Elemento \<Application> (rd.xml)  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<Application Activate="policy_setting"  
             Browse="policy_setting"  
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
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios. En la tabla de elementos secundarios, la directiva hace referencia al tipo de metadatos que hay disponible para determinados elementos de programa en tiempo de ejecución.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Tipo de atributo|DESCRIPCIÓN|  
|---------------|--------------------|-----------------|  
|`Activate`|Reflexión|Atributo opcional. Controla el acceso en tiempo de ejecución a los constructores para permitir la activación de instancias.|  
|`Browse`|Reflexión|Atributo opcional. Controla la consulta para obtener información acerca de los tipos o la enumeración de los tipos, pero no permite el acceso dinámico en tiempo de ejecución.|  
|`Dynamic`|Reflexión|Atributo opcional. Controla el acceso en tiempo de ejecución a todos los miembros de tipo (incluidos constructores, métodos, campos, propiedades y eventos) para permitir la programación dinámica.|  
|`Serialize`|Serialización|Atributo opcional. Controla el acceso en tiempo de ejecución a constructores, campos y propiedades para permitir que bibliotecas como el serializador JSON Newtonsoft puedan serializar y deserializar instancias de tipo.|  
|`DataContractSerializer`|Serialización|Atributo opcional. Controla la directiva de serialización que usa la clase <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType>.|  
|`DataContractJsonSerializer`|Serialización|Atributo opcional. Controla la directiva de serialización JSON que usa la clase <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType>.|  
|`XmlSerializer`|Serialización|Atributo opcional. Controla la directiva de serialización XML que usa la clase <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType>.|  
|`MarshalObject`|Interop|Atributo opcional. Controla la directiva de serialización de tipos de referencia a Windows Runtime y COM.|  
|`MarshalDelegate`|Interop|Atributo opcional. Controla la directiva de serialización de tipos de delegado como punteros de función a código nativo.|  
|`MarshalStructure`|Interop|Atributo opcional. Controla la directiva para calcular referencias de estructuras a código nativo.|  
  
## <a name="all-attributes"></a>Todos los atributos  
  
|Value|DESCRIPCIÓN|  
|-----------|-----------------|  
|*policy_setting*|Configuración de esta directiva que se aplica a los tipos en la aplicación. Los valores posibles son `All`, `Auto`, `Excluded`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal` y `Required All`. Para obtener más información, vea [Runtime Directive Policy Settings](runtime-directive-policy-settings.md) (Configuración de directiva de la directiva en tiempo de ejecución).|  
  
### <a name="child-elements"></a>Elementos secundarios  
  
|Elemento|DESCRIPCIÓN|  
|-------------|-----------------|  
|[\<Assembly>](assembly-element-net-native.md)|Aplica la directiva a todos los tipos en un ensamblado determinado.|  
|[\<Namespace>](namespace-element-net-native.md)|Aplica la directiva a todos los tipos en un espacio de nombres determinado.|  
|[\<Type>](type-element-net-native.md)|Aplica la directiva a un tipo determinado, como una clase o una estructura.|  
|[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|Aplica la directiva a un tipo genérico construido. Por ejemplo, se podría usar un elemento [\<TypeInstantiation>](typeinstantiation-element-net-native.md) para definir la directiva para un tipo `List<String>`.|  
|[\<Method>](method-element-net-native.md)|Aplica la directiva a un método en un tipo determinado.|  
|[\<MethodInstantiation>](methodinstantiation-element-net-native.md)|Aplica la directiva a un método genérico construido.|  
|[\<Property>](property-element-net-native.md)|Aplica la directiva a una propiedad en un tipo determinado.|  
|[\<Field>](field-element-net-native.md)|Aplica la directiva a un campo en un tipo determinado.|  
|[\<Event>](event-element-net-native.md)|Aplica la directiva a un evento en un tipo determinado.|  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|DESCRIPCIÓN|  
|-------------|-----------------|  
|[\<Directives>](directives-element-net-native.md)|Elemento raíz de un archivo de directivas en tiempo de ejecución.|  
  
## <a name="remarks"></a>Comentarios  
 El elemento [\<Directives>](directives-element-net-native.md) puede contener cero o un elemento `<Application>`. No se admiten varios elementos `<Application>` en un único archivo de directivas de reflexión.  
  
 El elemento `<Application>` se puede usar de dos maneras:  
  
- Como un contenedor para definir los elementos de programa cuyos metadatos son necesarios en tiempo de ejecución. En este caso, el elemento `<Application>` no necesita tener atributos. En tiempo de compilación, las herramientas del compilador realizan búsquedas en todas las bibliotecas (incluidas las bibliotecas principales de .NET Framework) para encontrar los elementos de programa identificados por los elementos secundarios del elemento `<Application>`. Por el contrario, las herramientas del compilador realizan búsquedas únicamente en la biblioteca designada por el elemento [\<Library>](library-element-net-native.md) para encontrar los elementos de programa identificados por los elementos secundarios del elemento [\<Library>](library-element-net-native.md).  
  
- Como un elemento que establece la directiva de la aplicación para la reflexión, serialización e interoperabilidad. Los atributos del elemento `<Application>` definen las directivas de la aplicación, que pueden ser invalidadas por los elementos secundarios definidos por el elemento `<Application>` o [\<Library>](library-element-net-native.md).  
  
## <a name="see-also"></a>Vea también

- [\<Elemento > de la biblioteca](library-element-net-native.md)
- [\<Directivas > elemento](directives-element-net-native.md)
- [Runtime Directive Elements (Elementos de directivas en tiempo de ejecución)](runtime-directive-elements.md)
- [Runtime Directives (rd.xml) Configuration File Reference (Referencia del archivo de configuración de directivas en tiempo de ejecución (rd.xml))](runtime-directives-rd-xml-configuration-file-reference.md)
