---
title: Char (Tipo de datos, Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Char
helpviewer_keywords:
- literal type characters [Visual Basic], C
- Char data type
- C literal type character [Visual Basic]
- data types [Visual Basic], assigning
- Char data type [Visual Basic], character literals
ms.assetid: cd7547a9-7855-4e8e-b216-35d74a362657
ms.openlocfilehash: 8313c2282a3b4b7b035f9f3b685a786c4471f53a
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630140"
---
# <a name="char-data-type-visual-basic"></a>Char (Tipo de datos, Visual Basic)

Contiene puntos de código sin signo de 16 bits (2 bytes) con un valor comprendido entre 0 y 65535. Cada *punto de código*, o código de carácter, representa un único carácter Unicode.

## <a name="remarks"></a>Comentarios

Utilice el `Char` tipo de datos cuando necesite contener un solo carácter y no necesite la sobrecarga de. `String` En algunos casos puede usar `Char()`, una matriz de `Char` elementos, para contener varios caracteres.

El valor predeterminado de `Char` es el carácter con un punto de código de 0.

## <a name="unicode-characters"></a>Caracteres Unicode

Los primeros 128 puntos de código (0 – 127) de Unicode corresponden a las letras y símbolos de un teclado estándar de EE. UU. Estos primeros 128 puntos de código son los mismos que los que define el juego de caracteres ASCII. Los dos puntos de código 128 (128 – 255) representan caracteres especiales, como Letras de alfabetos basados en latín, acentos, símbolos de moneda y fracciones. Unicode usa los puntos de código restantes (256-65535) para una amplia variedad de símbolos, incluidos los caracteres de texto en todo el mundo, los signos diacríticos y los símbolos matemáticos y técnicos.

Puede usar métodos como <xref:System.Char.IsDigit%2A> y <xref:System.Char.IsPunctuation%2A> en una `Char` variable para determinar su clasificación Unicode.

## <a name="type-conversions"></a>Conversiones de tipos

Visual Basic no convierte directamente entre `Char` y los tipos numéricos. Puede usar la <xref:Microsoft.VisualBasic.Strings.Asc%2A> función o <xref:Microsoft.VisualBasic.Strings.AscW%2A> para convertir un `Char` valor en un `Integer` que represente su punto de código. Puede usar la <xref:Microsoft.VisualBasic.Strings.Chr%2A> función o <xref:Microsoft.VisualBasic.Strings.ChrW%2A> para convertir un `Integer` valor en un `Char` que tiene ese punto de código.

Si el modificador de comprobación de tipo ( [Option Strict Statement](../../../visual-basic/language-reference/statements/option-strict-statement.md)) está activado, debe anexar el carácter de tipo literal a un literal de cadena de un solo carácter `Char` para identificarlo como el tipo de datos. Esto se ilustra en el siguiente ejemplo: La primera asignación a la `charVar` variable genera el error del compilador [BC30512](../../misc/bc30512.md) porque `Option Strict` es on. La segunda se compila correctamente porque el carácter `c` de tipo literal identifica el literal como un `Char` valor.

```vb
Option Strict On

Module CharType
    Public Sub Main()
        Dim charVar As Char

        ' This statement generates compiler error BC30512 because Option Strict is On.  
        charVar = "Z"  

        ' The following statement succeeds because it specifies a Char literal.  
        charVar = "Z"c
    End Sub
End Module
```

## <a name="programming-tips"></a>Sugerencias de programación

- **Números negativos.** `Char`es un tipo sin signo y no puede representar un valor negativo. En cualquier caso, no debe usar `Char` para contener valores numéricos.

- **Consideraciones de interoperabilidad.** Si la interfaz con componentes no escritos para el .NET Framework, por ejemplo, objetos de automatización o COM, recuerde que los tipos de caracteres tienen un ancho de datos diferente (8 bits) en otros entornos. Si pasa un argumento de 8 bits a este componente, declárelo como `Byte` en lugar de `Char` en el nuevo código de Visual Basic.

- **Ampliación.** El `Char` tipo de datos se amplía `String`a. Esto significa que puede convertir `Char` a `String` <xref:System.OverflowException?displayProperty=nameWithType>y no encontrará.

- **Caracteres de tipo.** Anexar el carácter `C` de tipo literal a un literal de cadena de un solo carácter lo `Char` convierte al tipo de datos. `Char`no tiene ningún carácter de tipo de identificador.

- **Tipo de marco.** El tipo correspondiente en .NET Framework es la estructura <xref:System.Char?displayProperty=nameWithType>.

## <a name="see-also"></a>Vea también

- <xref:System.Char?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Strings.Asc%2A>
- <xref:Microsoft.VisualBasic.Strings.AscW%2A>
- <xref:Microsoft.VisualBasic.Strings.Chr%2A>
- <xref:Microsoft.VisualBasic.Strings.ChrW%2A>
- [Tipos de datos](../../../visual-basic/language-reference/data-types/index.md)
- [String (tipo de datos)](../../../visual-basic/language-reference/data-types/string-data-type.md)
- [Funciones de conversión de tipos](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [Resumen de conversión](../../../visual-basic/language-reference/keywords/conversion-summary.md)
- [Cómo: Llamar a una función de Windows que adopta tipos sin signo](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
- [Uso eficiente de tipos de datos](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
