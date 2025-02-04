---
title: Una matriz declarada como variable de control de bucle no se puede declarar con un tamaño inicial
ms.date: 07/20/2015
f1_keywords:
- vbc32039
- bc32039
helpviewer_keywords:
- BC32039
ms.assetid: 1d8b6560-c9eb-4b71-a038-24c6f5a5ce46
ms.openlocfilehash: 9e8bb7b79b5a770c3c92e47d8e7c01c5b83d6061
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701211"
---
# <a name="array-declared-as-for-loop-control-variable-cannot-be-declared-with-an-initial-size"></a>Una matriz declarada como variable de control de bucle no se puede declarar con un tamaño inicial
Un bucle `For Each` usa una matriz como su variable de iteración de *elemento* , pero inicializa esa matriz.  
  
 Las instrucciones siguientes muestran cómo se puede generar este error.  
  
```vb  
Dim arrayList As New List(Of Integer())  
For Each listElement() As Integer In arrayList  
For Each listElement(1) As Integer In arrayList  
```  
  
 La primera instrucción `For Each` es la manera correcta de tener acceso a los elementos de `arrayList`. La segunda instrucción `For Each` genera este error.  
  
 **IDENTIFICADOR de error:** BC32039  
  
## <a name="to-correct-this-error"></a>Para corregir este error  
  
- Quite la inicialización de la declaración de la variable de iteración del *elemento* .  
  
## <a name="see-also"></a>Vea también

- [For...Next (instrucción)](../../../visual-basic/language-reference/statements/for-next-statement.md)
- [Matrices](../../../visual-basic/programming-guide/language-features/arrays/index.md)
- [Colecciones](../../../standard/collections/index.md)
