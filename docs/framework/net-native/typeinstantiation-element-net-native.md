---
title: <TypeInstantiation>Elemento (.NET Native)
ms.date: 03/30/2017
ms.assetid: a5eada64-075b-4162-9655-ded84e4681f2
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 375c95a30f4f60bb711e176cb6c2d0c5fd763e2f
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049110"
---
# <a name="typeinstantiation-element-net-native"></a>\<Elemento > TypeInstantiation (.NET Native)
Aplica la directiva de reflexión en tiempo de ejecución a un tipo genérico construido.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<TypeInstantiation Name="type_name"  
                   Arguments="type_arguments"  
                   Activate="policy_type"  
                   Browse="policy_type"  
                   Dynamic="policy_type"  
                   Serialize="policy_type"  
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
|`Name`|General|Atributo necesario. Especifica el nombre del tipo.|  
|`Arguments`|General|Atributo necesario. Especifica los argumentos de tipo genérico. Si hay varios argumentos, se separan mediante coma.|  
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
  
|Value|DESCRIPCIÓN|  
|-----------|-----------------|  
|*type_name*|Nombre del tipo. Si el elemento `<TypeInstantiation>` es un elemento secundario de un elemento [\<Namespace>](namespace-element-net-native.md), un elemento [\<Type>](type-element-net-native.md) u otro elemento `<TypeInstantiation>`, *type_name* puede especificar el nombre del tipo sin su espacio de nombres. De lo contrario, *type_name* debe incluir el nombre de tipo completo. El nombre de tipo no es representativo. Por ejemplo, para un objeto <xref:System.Collections.Generic.List%601?displayProperty=nameWithType>, el elemento `<TypeInstantiation>` puede aparecer del siguiente modo:<br /><br /> `\<TypeInstantiation Name=System.Collections.Generic.List Dynamic="Required Public" />`|  
  
## <a name="arguments-attribute"></a>Arguments (atributo)  
  
|Valor|DESCRIPCIÓN|  
|-----------|-----------------|  
|*type_argument*|Especifica los argumentos de tipo genérico. Si hay varios argumentos, se separan mediante coma. Cada argumento debe contener el nombre de tipo completo.|  
  
## <a name="all-other-attributes"></a>Resto de atributos  
  
|Valor|DESCRIPCIÓN|  
|-----------|-----------------|  
|*policy_setting*|Configuración que se aplica a este tipo de directiva para el tipo genérico construido. Los valores posibles son `All`, `Auto`, `Excluded`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal` y `Required All`. Para obtener más información, vea [Runtime Directive Policy Settings](runtime-directive-policy-settings.md) (Configuración de directiva de la directiva en tiempo de ejecución).|  
  
### <a name="child-elements"></a>Elementos secundarios  
  
|Elemento|DESCRIPCIÓN|  
|-------------|-----------------|  
|[\<Event>](event-element-net-native.md)|Aplica la directiva de reflexión a un evento perteneciente a este tipo.|  
|[\<Field>](field-element-net-native.md)|Aplica la directiva de reflexión a un campo de este tipo.|  
|[\<ImpliesType>](impliestype-element-net-native.md)|Aplica la directiva a un tipo, en caso de que dicha directiva se haya aplicado al tipo representado por el elemento `<TypeInstantiation>` que lo contiene.|  
|[\<Method>](method-element-net-native.md)|Aplica la directiva de reflexión a un método perteneciente a este tipo.|  
|[\<MethodInstantiation>](methodinstantiation-element-net-native.md)|Aplica la directiva de reflexión a un método genérico construido perteneciente a este tipo.|  
|[\<Property>](property-element-net-native.md)|Aplica la directiva de reflexión a una propiedad de este tipo.|  
|[\<Type>](type-element-net-native.md)|Aplica la directiva de reflexión a un tipo anidado.|  
|`<TypeInstantiation>`|Aplica la directiva de reflexión a un tipo genérico construido anidado.|  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|DESCRIPCIÓN|  
|-------------|-----------------|  
|[\<Application>](application-element-net-native.md)|Sirve de contenedor de los tipos y miembros de tipo de la aplicación cuyos metadatos están disponibles para la reflexión en tiempo de ejecución.|  
|[\<Assembly>](assembly-element-net-native.md)|Aplica la directiva de reflexión a todos los tipos en un ensamblado especificado.|  
|[\<Library>](library-element-net-native.md)|Define el ensamblado que contiene los tipos y miembros de tipo cuyos metadatos están disponibles para la reflexión en tiempo de ejecución.|  
|[\<Namespace>](namespace-element-net-native.md)|Aplica la directiva de reflexión a todos los tipos en un espacio de nombres.|  
|[\<Type>](type-element-net-native.md)|Aplica la directiva de reflexión a un tipo y a todos sus miembros.|  
|`<TypeInstantiation>`|Aplica la directiva de reflexión a un tipo genérico construido y a todos sus miembros.|  
  
## <a name="remarks"></a>Comentarios  
 La reflexión, la serialización y los atributos de interoperabilidad son opcionales. Sin embargo, al menos uno debe estar presente.  
  
 Si un elemento `<TypeInstantiation>` es un elemento secundario de un elemento [\<Assembly>](assembly-element-net-native.md), [\<Namespace>](namespace-element-net-native.md) o [\<Type>](type-element-net-native.md), invalida la configuración de directiva definida por el elemento primario. Si un elemento [\<Type>](type-element-net-native.md) establece una definición de tipo genérico correspondiente, el elemento `<TypeInstantiation>` invalida la directiva de reflexión en tiempo de ejecución solo en el caso de la creación de instancias del tipo genérico construido especificado.  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se usa la reflexión para recuperar la definición de tipo genérico de un objeto <xref:System.Collections.Generic.Dictionary%602> construido. También se usa la reflexión para mostrar información sobre objetos <xref:System.Type> que representan tipos genéricos construidos y definiciones de tipos genéricos. La variable `b` del ejemplo es un <xref:Windows.UI.Xaml.Controls.TextBlock> control.  
  
 [!code-csharp[ProjectN_Reflection#2](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/makegenerictype1.cs#2)]  
  
 Después de la compilación con la cadena de herramientas de .net Native, en el ejemplo se produce una excepción [MissingMetadataException](missingmetadataexception-class-net-native.md) en <xref:System.Type.GetGenericTypeDefinition%2A?displayProperty=nameWithType> la línea que llama al método. Puede eliminar la excepción e indicar los metadatos necesarios agregando el siguiente elemento `<TypeInstantiation>` al archivo de directivas en tiempo de ejecución:  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
  <Application>  
    <Assembly Name="*Application*" Dynamic="Required All" />  
     <TypeInstantiation Name="System.Collections.Generic.Dictionary"  
                        Arguments="System.String,GenericType.Example"  
                        Dynamic="Required Public" />  
  </Application>  
</Directives>  
```  
  
## <a name="see-also"></a>Vea también

- [Runtime Directives (rd.xml) Configuration File Reference (Referencia del archivo de configuración de directivas en tiempo de ejecución (rd.xml))](runtime-directives-rd-xml-configuration-file-reference.md)
- [Runtime Directive Elements (Elementos de directivas en tiempo de ejecución)](runtime-directive-elements.md)
- [Runtime Directive Policy Settings](runtime-directive-policy-settings.md) (Configuración de directiva de la directiva en tiempo de ejecución)
