---
title: No se puede convertir un tipo anónimo en un árbol de expresión porque contiene un campo que se usa en la inicialización de otro campo
ms.date: 07/20/2015
f1_keywords:
- bc36548
- vbc36548
helpviewer_keywords:
- BC36548
ms.assetid: 27de068f-080e-4160-86bf-1ec23fd1925a
ms.openlocfilehash: ba14c0cd8781b8771ac8b746e3efec29a457294a
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701189"
---
# <a name="cannot-convert-anonymous-type-to-expression-tree-because-it-contains-a-field-that-is-used-in-the-initialization-of-another-field"></a>No se puede convertir un tipo anónimo en un árbol de expresión porque contiene un campo que se usa en la inicialización de otro campo
El compilador no acepta la conversión de un anónimo en un árbol de expresión cuando se usa una propiedad del tipo anónimo para inicializar otra propiedad del tipo anónimo. Por ejemplo, en el código siguiente, `Prop1` se declara en la lista de inicialización y, a continuación, se usa como el valor inicial de `Prop2`.  
  
```vb  
Module M2  
  
    Sub ExpressionExample(Of T)(ByVal x As Expressions.Expression(Of Func(Of T)))  
    End Sub  
  
    Sub Main()  
        ' The following line causes the error.  
        ' ExpressionExample(Function() New With {.Prop1 = 2, .Prop2 = .Prop1})  
  
    End Sub  
End Module  
```  
  
 **IDENTIFICADOR de error:** BC36548  
  
## <a name="to-correct-this-error"></a>Para corregir este error  
  
- Asigne el valor inicial de `Prop1` a una variable local. Asigne esa variable a `Prop1` y `Prop2`, tal y como se muestra en el código siguiente.  
  
    ```vb  
    Sub Main()  
  
        Dim temp = 2  
        ExpressionExample(Function() New With {.Prop1 = temp, .Prop2 = temp})  
  
    End Sub  
    ```  
  
## <a name="see-also"></a>Vea también

- [Tipos anónimos (Visual Basic)](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)
- [Árboles de expresión (Visual Basic)](../../programming-guide/concepts/expression-trees/index.md)
- [Cómo: Usar árboles de expresión para generar consultas dinámicas (Visual Basic) ](../../programming-guide/concepts/expression-trees/how-to-use-expression-trees-to-build-dynamic-queries.md)
