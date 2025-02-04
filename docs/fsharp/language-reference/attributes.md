---
title: Atributos
description: Obtenga información F# sobre cómo los atributos permiten aplicar metadatos a una construcción de programación.
ms.date: 05/16/2016
ms.openlocfilehash: 17822891109b8e8eaa10044f82f0b872ce9d30b5
ms.sourcegitcommit: 878ca7550b653114c3968ef8906da2b3e60e3c7a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2019
ms.locfileid: "71736812"
---
# <a name="attributes"></a>Atributos

Los atributos permiten aplicar metadatos a una construcción de programación.

## <a name="syntax"></a>Sintaxis

```fsharp
[<target:attribute-name(arguments)>]
```

## <a name="remarks"></a>Comentarios

En la sintaxis anterior, el *destino* es opcional y, si está presente, especifica el tipo de entidad de programa a la que se aplica el atributo. Los valores válidos para el *destino* se muestran en la tabla que aparece más adelante en este documento.

El *atributo-name* hace referencia al nombre (posiblemente calificado con espacios de nombres) de un tipo de atributo válido, con o sin `Attribute` el sufijo que se suele utilizar en los nombres de tipo de atributo. Por ejemplo, el tipo `ObsoleteAttribute` se puede acortar a simplemente `Obsolete` en este contexto.

Los *argumentos* son los argumentos del constructor para el tipo de atributo. Si un atributo tiene un constructor sin parámetros, se pueden omitir la lista de argumentos y los paréntesis. Los atributos admiten argumentos posicionales y argumentos con nombre. Los *argumentos posicionales* son argumentos que se usan en el orden en que aparecen. Se pueden usar argumentos con nombre si el atributo tiene propiedades públicas. Puede establecerlos mediante la siguiente sintaxis en la lista de argumentos.

```fsharp
property-name = property-value
```

Dichas inicializaciones de propiedad pueden estar en cualquier orden, pero deben seguir cualquier argumento posicional. El siguiente es un ejemplo de un atributo que usa argumentos posicionales e inicializaciones de propiedad:

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6202.fs)]

En este ejemplo, el atributo es `DllImportAttribute`, que se usa en forma abreviada. El primer argumento es un parámetro posicional y el segundo es una propiedad.

Los atributos son una construcción de programación de .NET que permite asociar un objeto conocido como *atributo* a un tipo u otro elemento de programa. El elemento de programa al que se aplica un atributo se conoce como *destino de atributo*. El atributo normalmente contiene metadatos sobre su destino. En este contexto, los metadatos pueden ser cualquier dato sobre el tipo que no sea sus campos y miembros.

Los atributos F# de se pueden aplicar a las siguientes construcciones de programación: funciones, métodos, ensamblados, módulos, tipos (clases, registros, estructuras, interfaces, delegados, enumeraciones, uniones, etc.), constructores, propiedades, campos, parámetros, parámetros de tipo y valores devueltos. No se permiten atributos en `let` los enlaces dentro de las clases, expresiones o expresiones de flujo de trabajo.

Normalmente, la declaración de atributo aparece directamente antes de la declaración del destino de atributo. Se pueden usar varias declaraciones de atributos juntas, como se indica a continuación:

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6603.fs)]

Puede consultar los atributos en tiempo de ejecución mediante la reflexión de .NET.

Puede declarar varios atributos individualmente, como en el ejemplo de código anterior, o puede declararlos en un conjunto de corchetes si usa un punto y coma para separar los atributos y constructores individuales, como se indica a continuación:

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6604.fs)]

Normalmente, los atributos encontrados `Obsolete` incluyen el atributo, atributos para las consideraciones de seguridad, atributos para la compatibilidad con com, atributos que se relacionan con la propiedad del código y atributos que indican si un tipo se puede serializar. En el siguiente ejemplo se muestra el uso `Obsolete` del atributo.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6605.fs)]

En el caso de `assembly` los `module`destinos de atributo y, aplique los atributos a un `do` enlace de nivel superior en el ensamblado. Puede incluir la palabra `assembly` o `module` en la declaración de atributo, como se indica a continuación:

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6606.fs)]

Si se omite el destino de atributo para un atributo aplicado a `do` un enlace, F# el compilador intenta determinar el destino de atributo que tiene sentido para ese atributo. Muchas clases de atributos tienen un atributo de `System.AttributeUsageAttribute` tipo que incluye información sobre los posibles destinos admitidos para ese atributo. `System.AttributeUsageAttribute` Si indica que el atributo admite funciones como destinos, se toma el atributo para aplicar al punto de entrada principal del programa. `System.AttributeUsageAttribute` Si indica que el atributo admite ensamblados como destinos, el compilador toma el atributo para aplicar al ensamblado. La mayoría de los atributos no se aplican a las funciones y los ensamblados, pero en los casos en que lo hacen, el atributo se toma para aplicarse a la función principal del programa. Si el destino del atributo se especifica explícitamente, el atributo se aplica al destino especificado.

Aunque normalmente no es necesario especificar explícitamente el destino de atributo, en la tabla siguiente se muestran los valores válidos para el *destino* en un atributo junto con ejemplos de uso:

<table>
  <tr>
    <th>Destino de atributo</td>
    <th>Ejemplo</td> 
  </tr>
  <tr>
    <td>ensamblado</td>
    <td><pre lang="fsharp"><code>[&lt;assembly: AssemblyVersionAttribute("1.0.0.0")&gt;]</code></pre></td> 
  </tr>
  <tr>
    <td>return</td>
    <td><pre lang="fsharp"><code>let function1 x : [&lt;return: Obsolete&gt;] int = x + 1</code></pre></td> 
  </tr>
  <tr>
    <td>campo</td>
    <td><pre lang="fsharp"><code>[&lt;field: DefaultValue&gt;] val mutable x: int</code></pre></td> 
  </tr>
  <tr>
    <td>propiedad</td>
    <td><pre lang="fsharp"><code>[&lt;property: Obsolete&gt;] this.MyProperty = x</code></pre></td> 
  </tr>
  <tr>
    <td>param</td>
    <td><pre lang="fsharp"><code>member this.MyMethod([&lt;param: Out&gt;] x : ref&lt;int&gt;) = x := 10</code></pre></td> 
  </tr>
  <tr>
    <td>type</td>
    <td>
        <pre lang="fsharp"><code>
[&lt;type: StructLayout(Sequential)&gt;] 
type MyStruct = 
struct 
x : byte
y : int
end</code></pre>
    </td>
  </tr>
</table>

## <a name="see-also"></a>Vea también

- [Referencia del lenguaje F#](index.md)
