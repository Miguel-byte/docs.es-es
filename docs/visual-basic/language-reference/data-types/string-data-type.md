---
title: String (Tipo de datos, Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.String
helpviewer_keywords:
- strings [Visual Basic], character
- strings [Visual Basic], fixed-length
- string keyword [Visual Basic]
- fixed-length strings [Visual Basic], string data type
- literals [Visual Basic], string
- text [Visual Basic], String data type
- $ identifier type character
- String data type
- fixed-length strings
- string literals [Visual Basic]
- data types [Visual Basic], assigning
- String literals [Visual Basic]
- identifier type characters [Visual Basic], $
ms.assetid: 15ac03f5-cabd-42cc-a754-1df3893c25d9
ms.openlocfilehash: 6d2fd226735622de5cd7197060c05b8ac12b69f1
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2019
ms.locfileid: "71696836"
---
# <a name="string-data-type-visual-basic"></a>String (Tipo de datos, Visual Basic)
Contiene secuencias de puntos de código sin signo de 16 bits (2 bytes) que van desde 0 hasta 65535. Cada *punto de código*, o código de carácter, representa un único carácter Unicode. Una cadena puede contener entre 0 y aproximadamente 2 mil millones (2 ^ 31) caracteres Unicode.  
  
## <a name="remarks"></a>Comentarios  
 Utilice el tipo de datos `String` para contener varios caracteres sin la sobrecarga de administración de la matriz de `Char()`, una matriz de elementos `Char`.  
  
 El valor predeterminado de `String` es `Nothing` (referencia nula). Tenga en cuenta que esto no es lo mismo que la cadena vacía (valor `""`).  
  
## <a name="unicode-characters"></a>Caracteres Unicode  
 Los primeros 128 puntos de código (0 – 127) de Unicode corresponden a las letras y símbolos de un teclado estándar de EE. UU. Estos primeros 128 puntos de código son los mismos que los que define el juego de caracteres ASCII. Los dos puntos de código 128 (128 – 255) representan caracteres especiales, como Letras de alfabetos basados en latín, acentos, símbolos de moneda y fracciones. Unicode utiliza el resto de puntos de código (256-65535) para una amplia variedad de símbolos. Esto incluye los caracteres de texto, los signos diacríticos y los símbolos matemáticos y técnicos del mundo.  
  
 Puede usar métodos como <xref:System.Char.IsDigit%2A> y <xref:System.Char.IsPunctuation%2A> en un carácter individual de una variable `String` para determinar su clasificación Unicode.  
  
## <a name="format-requirements"></a>Requisitos de formato  
 Debe incluir un literal @no__t 0 entre comillas (`" "`). Si debe incluir una comilla tipográfica como uno de los caracteres de la cadena, utilice dos comillas contiguas (`""`). Esto se ilustra en el siguiente ejemplo:  
  
```vb  
Dim j As String = "Joe said ""Hello"" to me."  
Dim h As String = "Hello"  
' The following messages all display the same thing:  
' "Joe said "Hello" to me."  
MsgBox(j)  
MsgBox("Joe said " & """" & h & """" & " to me.")  
MsgBox("Joe said """ & h & """ to me.")  
```  
  
 Tenga en cuenta que las comillas contiguas que representan una comilla en la cadena son independientes de las comillas que comienzan y finalizan el literal `String`.  
  
## <a name="string-manipulations"></a>Manipulaciones de cadenas  
 Una vez que se asigna una cadena a una variable `String`, esa cadena es *inmutable*, lo que significa que no se puede cambiar su longitud o su contenido. Al modificar una cadena de alguna manera, Visual Basic crea una nueva cadena y abandona la anterior. A continuación, la variable `String` apunta a la nueva cadena.  
  
 Puede manipular el contenido de una variable `String` mediante una variedad de funciones de cadena. En el ejemplo siguiente se muestra la función <xref:Microsoft.VisualBasic.Strings.Left%2A>  
  
```vb  
Dim S As String = "Database"  
' The following statement sets S to a new string containing "Data".  
S = Microsoft.VisualBasic.Left(S, 4)  
```  
  
 Una cadena creada por otro componente se puede rellenar con espacios iniciales o finales. Si recibe este tipo de cadena, puede usar las funciones <xref:Microsoft.VisualBasic.Strings.Trim%2A>, <xref:Microsoft.VisualBasic.Strings.LTrim%2A> y <xref:Microsoft.VisualBasic.Strings.RTrim%2A> para quitar estos espacios.  
  
 Para obtener más información sobre las manipulaciones de cadenas, vea [cadenas](../../../visual-basic/programming-guide/language-features/strings/index.md).  
  
## <a name="programming-tips"></a>Sugerencias de programación  
  
- **Números negativos.** Recuerde que los caracteres que contiene `String` están sin signo y no pueden representar valores negativos. En cualquier caso, no debe utilizar `String` para contener valores numéricos.  
  
- **Consideraciones de interoperabilidad.** Si interactúa con componentes que no se han escrito para el .NET Framework, por ejemplo, objetos de automatización o COM, recuerde que los caracteres de cadena tienen un ancho de datos diferente (8 bits) en otros entornos. Si va a pasar un argumento de cadena de caracteres de 8 bits a este componente, declárelo como `Byte()`, una matriz de elementos `Byte`, en lugar de `String` en el nuevo código de Visual Basic.  
  
- **Caracteres de tipo.** Anexar el carácter de tipo de identificador `$` a cualquier identificador lo convierte al tipo de datos `String`. `String` no tiene ningún carácter de tipo literal. Sin embargo, el compilador trata los literales entre comillas (`" "`) como `String`.  
  
- **Tipo de marco.** El tipo correspondiente en el .NET Framework es la clase <xref:System.String?displayProperty=nameWithType>.  
  
## <a name="see-also"></a>Vea también

- <xref:System.String?displayProperty=nameWithType>
- [Tipos de datos](../../../visual-basic/language-reference/data-types/index.md)
- [Char (tipo de datos)](../../../visual-basic/language-reference/data-types/char-data-type.md)
- [Funciones de conversión de tipos](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [Resumen de conversión](../../../visual-basic/language-reference/keywords/conversion-summary.md)
- [Cómo: Llamar a una función de Windows que adopta tipos sin signo](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
- [Uso eficiente de tipos de datos](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
