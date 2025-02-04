---
title: Procedimiento Contener más de un valor en una variable (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- classes [Visual Basic], composite data types
- composite types [Visual Basic]
- composite data types [Visual Basic]
- data types [Visual Basic], composite
- arrays [Visual Basic], composite data types
- structures [Visual Basic], composite data types
- arrays [Visual Basic], compilation errors
- types [Visual Basic], composite
ms.assetid: 5fe0e558-aac2-4a40-b7f2-7cfea7336917
ms.openlocfilehash: 8d07a34a98303f9d220dba0a3c955120b421340e
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71054196"
---
# <a name="how-to-hold-more-than-one-value-in-a-variable-visual-basic"></a>Procedimiento Contener más de un valor en una variable (Visual Basic)

Una variable contiene más de un valor si se declara como un *tipo de datos compuesto*.

Los [tipos de datos compuestos](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md) incluyen estructuras, matrices y clases. Una variable de un tipo de datos compuesto puede contener una combinación de tipos de datos básicos y otros tipos compuestos. Las estructuras y las clases pueden contener código y datos.

## <a name="to-hold-more-than-one-value-in-a-variable"></a>Para contener más de un valor en una variable

1. Determine qué tipo de datos compuesto desea usar para la variable.

2. Si el tipo de datos compuesto todavía no está definido, debe definirlo para que la variable pueda usarlo.

    - Defina una estructura con una [instrucción Structure](../../../../visual-basic/language-reference/statements/structure-statement.md).

    - Defina una matriz con una [instrucción Dim](../../../../visual-basic/language-reference/statements/dim-statement.md).

    - Defina una clase con una [instrucción de clase](../../../../visual-basic/language-reference/statements/class-statement.md).

3. Declare la variable con `Dim` una instrucción.

4. Siga el nombre de la variable `As` con una cláusula.

5. Siga la `As` palabra clave con el nombre del tipo de datos compuesto adecuado.

## <a name="see-also"></a>Vea también

- [Tipos de datos](../../../../visual-basic/language-reference/data-types/index.md)
- [Caracteres de tipo](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)
- [Tipos de datos compuestos](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)
- [Estructuras](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [Matrices](../../../../visual-basic/programming-guide/language-features/arrays/index.md)
- [Objetos y clases](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
- [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
