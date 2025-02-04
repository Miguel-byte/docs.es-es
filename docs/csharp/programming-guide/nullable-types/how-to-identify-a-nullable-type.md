---
title: 'Identificación de tipos de valor que admiten un valor NULL: Guía de programación de C#'
ms.custom: seodec18
description: Obtenga información sobre cómo determinar si un tipo es un tipo de valor que admite un valor NULL o una instancia es de un tipo de valor que admite un valor NULL
ms.date: 09/26/2019
helpviewer_keywords:
- nullable value types [C#], identifying
ms.assetid: d4b67ee2-66e8-40c1-ae9d-545d32c71387
ms.openlocfilehash: 15b1ffedf57648955ee5a004514841a5d140292b
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392610"
---
# <a name="how-to-identify-a-nullable-value-type-c-programming-guide"></a>Identificación de tipos de valor que admiten un valor NULL (Guía de programación de C#)

El ejemplo siguiente muestra cómo determinar si una instancia <xref:System.Type?displayProperty=nameWithType> representa un tipo de valor genérico cerrado que admite un valor NULL, es decir, el tipo <xref:System.Nullable%601?displayProperty=nameWithType> con un parámetro de tipo especificado `T`:

[!code-csharp-interactive[whether Type is nullable](../../../../samples/snippets/csharp/programming-guide/nullable-types/IdentifyNullableType.cs#1)]

Como se muestra en el ejemplo, se usa el operador [typeof](../../language-reference/operators/type-testing-and-cast.md#typeof-operator) para crear un objeto <xref:System.Type?displayProperty=nameWithType>.

Si quiere determinar si una instancia es de un tipo de valor que admite un valor NULL, no use el método <xref:System.Object.GetType%2A?displayProperty=nameWithType> para obtener una instancia de <xref:System.Type> para probarla con el código anterior. Cuando se llama al método <xref:System.Object.GetType%2A?displayProperty=nameWithType> en una instancia de un tipo de valor que admite un valor NULL, [se aplica la conversión boxing](using-nullable-types.md#boxing-and-unboxing) a la instancia para convertirla en <xref:System.Object>. Como la conversión boxing de una instancia que no es NULL de un tipo de valor que admite un valor NULL equivale la conversión boxing de un valor del tipo subyacente, <xref:System.Object.GetType%2A> devuelve un objeto <xref:System.Type> que representa el tipo de valor subyacente que admite un valor NULL:

[!code-csharp-interactive[GetType example](../../../../samples/snippets/csharp/programming-guide/nullable-types/IdentifyNullableType.cs#2)]

No use el operador [is](../../language-reference/keywords/is.md) para determinar si una instancia es de un tipo de valor que admite un valor NULL. Como se muestra en el ejemplo siguiente, no se pueden distinguir los tipos de instancias de un tipo de valor que admite un valor NULL y su tipo subyacente mediante el operador `is`:

[!code-csharp-interactive[is operator example](../../../../samples/snippets/csharp/programming-guide/nullable-types/IdentifyNullableType.cs#3)]

Se puede usar el código que se presenta en el ejemplo siguiente para determinar si una instancia es de un tipo de valor que admite un valor NULL:

[!code-csharp-interactive[whether an instance is of a nullable type](../../../../samples/snippets/csharp/programming-guide/nullable-types/IdentifyNullableType.cs#4)]

## <a name="see-also"></a>Vea también

- [Tipos de valores que aceptan valores NULL](index.md)
- [Uso de tipos que admiten un valor NULL](using-nullable-types.md)
- <xref:System.Nullable.GetUnderlyingType%2A>
