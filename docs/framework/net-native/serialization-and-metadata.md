---
title: Serialización y metadatos
ms.date: 03/30/2017
ms.assetid: 619ecf1c-1ca5-4d66-8934-62fe7aad78c6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ec8180da9637ec2b2c4e1b432773b4f9f1ac908b
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049183"
---
# <a name="serialization-and-metadata"></a>Serialización y metadatos

Si la aplicación serializa y deserializa objetos, es posible que deba agregar entradas al archivo de directivas en tiempo de ejecución (.rd.xml) para asegurarse de que los metadatos necesarios están presentes en tiempo de ejecución. Existen dos categorías de serializadores y cada una requiere un tratamiento distinto en el archivo de directivas en tiempo de ejecución:  
  
- Serializadores de terceros basados en la reflexión. Estos requieren modificaciones en el archivo de directivas en tiempo de ejecución y se describen en la sección siguiente.  
  
- Serializadores no basados en reflexión que se encuentran en la biblioteca de clases de. NET Framework. Estos pueden exigir modificaciones en el archivo de directivas en tiempo de ejecución, y se explican en la sección [Serializadores de Microsoft](#Microsoft).  
  
<a name="ThirdParty"></a>
## <a name="third-party-serializers"></a>Serializadores de terceros

 Los serializadores de terceros, entre los que está Newtonsoft.JSON, normalmente están basados en reflexión. Dado un objeto binario grande (BLOB) de datos serializados, los campos de los datos se asignan a un tipo concreto mediante la búsqueda por nombre de los campos del tipo de destino. Como mínimo, el empleo de estas bibliotecas produce excepciones [MissingMetadataException](missingmetadataexception-class-net-native.md) para cada objeto <xref:System.Type> que se intenta serializar o deserializar en una colección `List<Type>`.  
  
 La forma más sencilla de solucionar los problemas causados por la falta de metadatos para estos serializadores es recopilar los tipos que se utilizarán en la serialización en un único espacio de nombres (como `App.Models`) y aplicar una directiva de metadatos `Serialize`:  
  
```xml  
<Namespace Name="App.Models" Serialize="Required PublicAndInternal" />  
```  
  
 Para más información sobre la sintaxis usada en el ejemplo, vea [Elemento \<Namespace>](namespace-element-net-native.md).  
  
<a name="Microsoft"></a>
## <a name="microsoft-serializers"></a>Serializadores de Microsoft

 Aunque las clases <xref:System.Runtime.Serialization.DataContractSerializer>, <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> y <xref:System.Xml.Serialization.XmlSerializer> no se basan en la reflexión, necesitan generar código en función del objeto que se va a serializar o deserializar. Los constructores sobrecargados de cada serializador incluyen un parámetro <xref:System.Type> que especifica el tipo que se va a serializar o deserializar. La forma de especificar ese tipo en el código define la acción que se debe realizar, como se explica en las dos secciones siguientes.  
  
### <a name="typeof-used-in-the-constructor"></a>typeof utilizado en el constructor

 Si llama a un constructor de estas clases de serialización e incluye C# el operador [typeof](../../csharp/language-reference/operators/type-testing-and-cast.md#typeof-operator) en la llamada al método, **no tiene que realizar ningún trabajo adicional**. Por ejemplo, en cada una de las siguientes llamadas a un constructor de clase de serialización, la palabra clave `typeof` se utiliza como parte de la expresión que se pasa al constructor.  
  
 [!code-csharp[ProjectN#5](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/serialize1.cs#5)]  
  
 El compilador de .NET Native administrará automáticamente este código.  
  
### <a name="typeof-used-outside-the-constructor"></a>typeof usado fuera del constructor

 Si se llama a un constructor de estas clases de serialización y C# se usa el operador [typeof](../../csharp/language-reference/operators/type-testing-and-cast.md#typeof-operator) fuera de la expresión proporcionada al <xref:System.Type> parámetro del constructor, como en el código siguiente, el compilador .net Native no puede resolver el tipo:  
  
 [!code-csharp[ProjectN#6](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/serialize1.cs#6)]  
  
 En este caso, debe especificar el tipo en el archivo de directivas de tiempo de ejecución mediante la adición de una entrada como la siguiente:  
  
```xml  
<Type Name="DataSet" Browse="Required Public" />  
```  
  
 Del mismo modo, si llama a un constructor <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Type%5B%5D%29?displayProperty=nameWithType> como y proporciona una matriz de <xref:System.Type> objetos adicionales para serializar, como en el código siguiente, el compilador .net Native no puede resolver estos tipos.  
  
 [!code-csharp[ProjectN#7](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/serialize1.cs#7)]  
  
 Debe agregar entradas como la siguiente para cada tipo en el archivo de directivas de tiempo de ejecución:  
  
```xml  
<Type Name="t" Browse="Required Public" />  
```  
  
 Para más información sobre la sintaxis usada en el ejemplo, vea [Elemento \<Type>](type-element-net-native.md).  
  
## <a name="see-also"></a>Vea también

- [Runtime Directives (rd.xml) Configuration File Reference (Referencia del archivo de configuración de directivas en tiempo de ejecución (rd.xml))](runtime-directives-rd-xml-configuration-file-reference.md)
- [Runtime Directive Elements (Elementos de directivas en tiempo de ejecución)](runtime-directive-elements.md)
- [\<Tipo > elemento](type-element-net-native.md)
- [Elemento \<Namespace>](namespace-element-net-native.md)
