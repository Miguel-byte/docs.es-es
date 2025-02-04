---
title: Los límites de matriz no pueden aparecer en los especificadores de tipo
ms.date: 07/20/2015
f1_keywords:
- vbc30638
- bc30638
helpviewer_keywords:
- BC30638
ms.assetid: 93b654f4-70fa-4a48-baed-ffae42075550
ms.openlocfilehash: 951f710160ae1023671773c21c73946f5ae94c2b
ms.sourcegitcommit: 463f3f050cecc0b6403e67f19a61f870fb8e7b7d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2019
ms.locfileid: "68512763"
---
# <a name="array-bounds-cannot-appear-in-type-specifiers"></a>Los límites de matriz no pueden aparecer en los especificadores de tipo

Los tamaños de la matriz no se pueden declarar como parte de un especificador de tipo de datos.

**IDENTIFICADOR de error:** BC30638

## <a name="to-correct-this-error"></a>Para corregir este error

- Especifique el tamaño de la matriz inmediatamente después del nombre de la variable en lugar de colocar el tamaño de la matriz después del tipo, como se muestra en el ejemplo siguiente.

  ```vb
  Dim Array(8) As Integer
  ```

- Defina una matriz e inicialícela con el número deseado de elementos, como se muestra en el ejemplo siguiente.

  ```vb
  Dim Array2() As Integer = New Integer(8) {}
  ```

## <a name="see-also"></a>Vea también

- [Matrices](../../../visual-basic/programming-guide/language-features/arrays/index.md)
