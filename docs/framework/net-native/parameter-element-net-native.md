---
title: <Parameter>Elemento (.NET Native)
ms.date: 03/30/2017
ms.assetid: 22aaa1f3-596f-4733-93db-f4bcabcb5240
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5c9a462e75df535504d0e98c22c34c11ff7af7d8
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049346"
---
# <a name="parameter-element-net-native"></a>\<Elemento Parameter > (.NET Native)
Aplica la directiva de reflexión al tipo del argumento que se pasa a un método.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<Parameter Name="parameter_name"  
           Activate="policy_type"  
           Browse="policy_type"  
           Dynamic="policy_type"  
           Serialize="policy_type"  
           DataContractSerializer="policy_type"  
           DataContractJsonSerializer="policy_type"  
           XmlSerializer="policy_type"  
           MarshalObject="policy_type"  
           MarshalDelegate="policy_type"  
           MarshalStructure="policy_type" />  
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Tipo de atributo|DESCRIPCIÓN|  
|---------------|--------------------|-----------------|  
|`Name`|General|Atributo necesario. Nombre del parámetro. Por ejemplo, para la signatura del método `String.CompareTo(Object value)`, el valor del atributo `Name` es "value".|  
|`Activate`|Reflexión|Atributo opcional. Controla el acceso en tiempo de ejecución a los constructores para permitir la activación de instancias.|  
|`Browse`|Reflexión|Atributo opcional. Controla la consulta para obtener información sobre los elementos de programa, pero no permite el acceso en tiempo de ejecución.|  
|`Dynamic`|Reflexión|Atributo opcional. Controla el acceso en tiempo de ejecución a todos los miembros de tipo (incluidos constructores, métodos, campos, propiedades y eventos) para permitir la programación dinámica.|  
|`Serialize`|Serialización|Atributo opcional. Controla el acceso en tiempo de ejecución a constructores, campos y propiedades para permitir que bibliotecas como el serializador JSON Newtonsoft puedan serializar y deserializar instancias de tipo.|  
|`DataContractSerializer`|Serialización|Atributo opcional. Controla la directiva de serialización que usa la clase <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType>.|  
|`DataContractJsonSerializer`|Serialización|Atributo opcional. Controla la directiva de serialización JSON que usa la clase <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType>.|  
|`XmlSerializer`|Serialización|Atributo opcional. Controla la directiva de serialización XML que usa la clase <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType>.|  
|`MarshalObject`|Interop|Atributo opcional. Controla la directiva de cálculo de referencias de tipos de referencia para WinRT y COM.|  
|`MarshalDelegate`|Interop|Atributo opcional. Controla la directiva de serialización de tipos de delegado como punteros de función a código nativo.|  
|`MarshalStructure`|Interop|Atributo opcional. Controla la directiva de cálculo de referencias de tipos de valor a código nativo.|  
  
## <a name="name-attribute"></a>Name (atributo)  
  
|Valor|DESCRIPCIÓN|  
|-----------|-----------------|  
|*parameter_name*|Nombre del parámetro de método al que se aplica la directiva. Por ejemplo, para la signatura del método `String.CompareTo(Object value)`, el valor del atributo `Name` es "value".|  
  
## <a name="all-other-attributes"></a>Resto de atributos  
  
|Valor|DESCRIPCIÓN|  
|-----------|-----------------|  
|*policy_setting*|Configuración que se va a aplicar a este tipo de directiva. Los valores posibles son `All`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal` y `Required All`. Para obtener más información, vea [Runtime Directive Policy Settings](runtime-directive-policy-settings.md) (Configuración de directiva de la directiva en tiempo de ejecución).|  
  
### <a name="child-elements"></a>Elementos secundarios  
 Ninguno.  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|DESCRIPCIÓN|  
|-------------|-----------------|  
|[\<Method>](method-element-net-native.md)|Aplica la directiva de reflexión en tiempo de ejecución a un constructor o método.|  
  
## <a name="remarks"></a>Comentarios  
 `<Parameter>` es un elemento secundario del elemento [\<Method>](method-element-net-native.md) y se usa para aplicar directivas a un parámetro de método concreto. El parámetro de método determinado se especifica mediante el nombre en lugar del tipo. Debe haber presente al menos un atributo que represente un tipo de directiva, como `Activate` o `Dynamic`.  
  
## <a name="see-also"></a>Vea también

- [Elemento \<Method>](method-element-net-native.md)
- [Runtime Directives (rd.xml) Configuration File Reference (Referencia del archivo de configuración de directivas en tiempo de ejecución (rd.xml))](runtime-directives-rd-xml-configuration-file-reference.md)
- [Runtime Directive Policy Settings](runtime-directive-policy-settings.md) (Configuración de directiva de la directiva en tiempo de ejecución)
- [Runtime Directive Elements (Elementos de directivas en tiempo de ejecución)](runtime-directive-elements.md)
