---
title: 'Operador ?: (referencia de C#)'
ms.custom: seodec18
ms.date: 11/20/2018
f1_keywords:
- ?:_CSharpKeyword
- ?_CSharpKeyword
- :_CSharpKeyword
helpviewer_keywords:
- '?: operator [C#]'
- conditional operator (?:) [C#]
ms.assetid: e83a17f1-7500-48ba-8bee-2fbc4c847af4
ms.openlocfilehash: 923591634599a6bbac74d43b105f4e46b492fa1a
ms.sourcegitcommit: bbfcc913c275885381820be28f61efcf8e83eecc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/05/2019
ms.locfileid: "68796466"
---
# <a name="-operator-c-reference"></a>Operador ?: (referencia de C#)

El operador condicional `?:`, normalmente conocido como operador condicional ternario, evalúa una expresión booleana y devuelve el resultado de evaluar una de dos expresiones, en función de que la expresión booleana se evalúe como `true` o `false`. A partir C# 7.2, la [expresión condicional ref](#conditional-ref-expression) devuelve la referencia al resultado de una de las dos expresiones.

La sintaxis del operador condicional es la siguiente:

```csharp
condition ? consequent : alternative
```

La expresión `condition` debe evaluarse como `true` o `false`. Si `condition` se evalúa como `true`, se evalúa la expresión `consequent` y su resultado se convierte en el resultado de la operación. Si `condition` se evalúa como `false`, se evalúa la expresión `alternative` y su resultado se convierte en el resultado de la operación. Solo se evalúan `consequent` o `alternative`.

Los tipos de `consequent` y `alternative` deben coincidir o debe haber una conversión implícita de un tipo al otro.

El operador condicional es asociativo a la derecha, es decir, una expresión de la forma

```csharp
a ? b : c ? d : e
```

se evalúa como

```csharp
a ? b : (c ? d : e)
```

> [!TIP]
> Puede utilizar el siguiente recurso mnemotécnico para recordar cómo se evalúa el operador condicional:
>
> ```text
> is this condition true ? yes : no
> ```

En el siguiente ejemplo se muestra el uso del operador condicional:

[!code-csharp-interactive[non ref conditional](~/samples/csharp/language-reference/operators/ConditionalOperator.cs#ConditionalValue)]

## <a name="conditional-ref-expression"></a>Expresión condicional ref

A partir C# 7.2, puede utilizar la expresión condicional ref para devolver la referencia al resultado de una de las dos expresiones. Puede asignar esa referencia a una variable [ref local](../keywords/ref.md#ref-locals) o [ref readonly local](../keywords/ref.md#ref-readonly-locals), o bien usarla como un [valor devuelto de referencia](../keywords/ref.md#reference-return-values) o como un [parámetro de método `ref`](../keywords/ref.md#passing-an-argument-by-reference).

La sintaxis de la expresión condicional ref es la siguiente:

```csharp
condition ? ref consequent : ref alternative
```

Al igual que el operador condicional original, la expresión condicional ref evalúa solo una de las dos expresiones: ya sea `consequent` o `alternative`.

En el caso de la expresión condicional ref, los tipos de `consequent` y `alternative` deben coincidir.

En el siguiente ejemplo se muestra el uso de la expresión condicional ref:

[!code-csharp-interactive[conditional ref](~/samples/csharp/language-reference/operators/ConditionalOperator.cs#ConditionalRef)]

Para más información, vea la [nota de propuesta de características](~/_csharplang/proposals/csharp-7.2/conditional-ref.md).

## <a name="conditional-operator-and-an-ifelse-statement"></a>Operador condicional y una instrucción `if..else`

El uso del operador condicional a través de una instrucción [if-else](../keywords/if-else.md) podría traducirse en código más conciso en aquellos casos en los que potencialmente tenga que calcular un valor. El ejemplo siguiente muestra dos maneras de clasificar un entero como negativo o no negativo:

[!code-csharp[conditional and if-else](~/samples/csharp/language-reference/operators/ConditionalOperator.cs#CompareWithIf)]

## <a name="operator-overloadability"></a>Posibilidad de sobrecarga del operador

El operador condicional no se puede sobrecargar.

## <a name="c-language-specification"></a>Especificación del lenguaje C#

Para más información, vea la sección sobre [operadores condicionales](~/_csharplang/spec/expressions.md#conditional-operator) de la [Especificación del lenguaje C#](~/_csharplang/spec/introduction.md).

## <a name="see-also"></a>Vea también

- [Referencia de C#](../index.md)
- [Operadores de C#](index.md)
- [Instrucción if-else](../keywords/if-else.md)
- [Operadores ?. y ?[]](member-access-operators.md#null-conditional-operators--and-)
- [Operador ??](null-coalescing-operator.md)
- [ref (palabra clave)](../keywords/ref.md)
