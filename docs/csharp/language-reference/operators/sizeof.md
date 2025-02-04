---
title: 'Operador sizeof: Referencia de C#'
ms.custom: seodec18
ms.date: 07/25/2019
f1_keywords:
- sizeof_CSharpKeyword
- sizeof
helpviewer_keywords:
- sizeof keyword [C#]
ms.assetid: c548592c-677c-4f40-a4ce-e613f7529141
ms.openlocfilehash: c455804923f4d0e7cc8f556bb9b9df34b6332d82
ms.sourcegitcommit: bbfcc913c275885381820be28f61efcf8e83eecc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/05/2019
ms.locfileid: "68796517"
---
# <a name="sizeof-operator-c-reference"></a>Operador sizeof (referencia de C#)

El operador `sizeof` devuelve el número de bytes ocupados por una variable de un tipo determinado. El argumento del operador `sizeof` debe ser el nombre de un [tipo administrado](../builtin-types/unmanaged-types.md) o un parámetro de tipo que está [restringido](../../programming-guide/generics/constraints-on-type-parameters.md#unmanaged-constraint) para ser un tipo no administrado.

El operador `sizeof` requiere un contexto de [unsafe](../keywords/unsafe.md). Sin embargo, las expresiones presentadas en la tabla siguiente se evalúan en tiempo de compilación según los valores de constantes correspondientes y no necesitan un contexto de unsafe:

|Expresión|Valor constante|
|---------|---------------|
|`sizeof(sbyte)`|1|
|`sizeof(byte)`|1|
|`sizeof(short)`|2|
|`sizeof(ushort)`|2|
|`sizeof(int)`|4|
|`sizeof(uint)`|4|
|`sizeof(long)`|8|
|`sizeof(ulong)`|8|
|`sizeof(char)`|2|
|`sizeof(float)`|4|
|`sizeof(double)`|8|
|`sizeof(decimal)`|16|
|`sizeof(bool)`|1|

Tampoco es necesario usar un contexto de unsafe cuando el operando del operador `sizeof` es el nombre de un tipo [enum](../keywords/enum.md).

En el siguiente ejemplo se muestra el uso del operador `sizeof`:

[!code-csharp[sizeof examples](~/samples/csharp/language-reference/operators/SizeOfOperator.cs)]

El operador `sizeof` devuelve un número de bytes que asignará Common Language Runtime en la memoria administrada. Para los tipos [struct](../keywords/struct.md), el valor incluye el relleno, tal y como se muestra en el ejemplo anterior. El resultado del operador `sizeof` puede ser distinto del resultado del método <xref:System.Runtime.InteropServices.Marshal.SizeOf%2A?displayProperty=nameWithType>, que devuelve el tamaño de un tipo en la memoria *no administrada*.

## <a name="c-language-specification"></a>Especificación del lenguaje C#

Para obtener más información, vea la sección [Operador sizeof](~/_csharplang/spec/unsafe-code.md#the-sizeof-operator) de la [Especificación del lenguaje C#](~/_csharplang/spec/introduction.md).

## <a name="see-also"></a>Vea también

- [Referencia de C#](../index.md)
- [Operadores de C#](index.md)
- [Operadores relacionados con el puntero](pointer-related-operators.md)
- [Tipos de puntero](../../programming-guide/unsafe-code-pointers/pointer-types.md)
- [Tipos relacionados con el intervalo y la memoria](../../../standard/memory-and-spans/index.md)
