---
title: Sugerencias para mejorar el rendimiento de .NET
ms.date: 03/30/2017
helpviewer_keywords:
- C# language, performance
- performance [C#]
- Visual Basic, performance
- performance [Visual Basic]
ms.assetid: ae275793-857d-4102-9095-b4c2a02d57f4
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 14ed06bbd09d7551707628060b460584816e4711
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046294"
---
# <a name="net-performance-tips"></a>Sugerencias para mejorar el rendimiento de .NET
El término *rendimiento* suele hacer referencia a la velocidad de ejecución de un programa. A veces se puede aumentar la velocidad de ejecución si se siguen algunas reglas básicas en el código fuente. En algunos programas, es importante examinar el código detenidamente y usar generadores de perfiles para asegurarse de que se está ejecutando lo más rápidamente posible. En otros programas, no es necesario realizar esta optimización, ya que el código se ejecuta con una velocidad aceptable mientras se escribe. En este artículo se enumeran algunas áreas donde el rendimiento puede verse afectado y sugerencias para mejorar, así como vínculos a temas de rendimiento adicionales. Para más información sobre cómo planear y medir el rendimiento, vea [Rendimiento](index.md)  
  
## <a name="boxing-and-unboxing"></a>Conversión boxing y conversión unboxing  
 Es mejor evitar el uso de tipos de valor en situaciones en las que se debe aplicar la conversión boxing un gran número de veces, por ejemplo, en las clases de colecciones no genéricas como <xref:System.Collections.ArrayList?displayProperty=nameWithType>. Puede evitar la conversión boxing de tipos de valor mediante el uso de colecciones genéricas como <xref:System.Collections.Generic.List%601?displayProperty=nameWithType>. Las conversiones boxing y unboxing son procesos que consumen muchos recursos. Cuando se aplica la conversión boxing a un tipo de valor, se debe crear un objeto completamente nuevo. Esto puede tardar hasta 20 veces más que la asignación de una referencia simple. Cuando se aplica la conversión unboxing, el proceso de conversión puede tardar cuatro veces más que una asignación. Para obtener más información, vea [Conversión boxing y unboxing](../../csharp/programming-guide/types/boxing-and-unboxing.md).  
  
## <a name="strings"></a>Cadenas  
 Al concatenar un gran número de variables de cadena, por ejemplo en un bucle compacto, use <xref:System.Text.StringBuilder?displayProperty=nameWithType> en lugar del [operador +](../../csharp/language-reference/operators/addition-operator.md) de C# o los [operadores de concatenación](../../visual-basic/language-reference/operators/concatenation-operators.md) de Visual Basic. Para obtener más información, vea [Cómo: Concatenar varias cadenas](../../csharp/how-to/concatenate-multiple-strings.md) y [operadores de concatenación en Visual Basic](../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md).  
  
## <a name="destructors"></a>Destructores  
 No se deben utilizar destructores vacíos. Cuando una clase contiene un destructor, se crea una entrada en la cola Finalize. Cuando se llama al destructor, se invoca al recolector de elementos no utilizados para procesar la cola. Si el destructor está vacío, simplemente se produce una pérdida de rendimiento. Para obtener más información, vea [destructores](../../csharp/programming-guide/classes-and-structs/destructors.md) y [duración de los objetos: Cómo se crean y destruyen](../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)los objetos.  
  
## <a name="other-resources"></a>Otros recursos  
  
- [Escritura de código administrado más rápido: Conocer el costo de las cosas](https://go.microsoft.com/fwlink/?LinkId=99294)  
  
- [Escritura de aplicaciones administradas de alto rendimiento: Un manual](https://go.microsoft.com/fwlink/?LinkId=99295)  
  
- [Garbage Collector Basics and Performance Hints](https://go.microsoft.com/fwlink/?LinkId=99296) (Conceptos básicos del recolector de elementos no utilizados y sugerencias de rendimiento)  
  
- [Performance Tips and Tricks in .NET Applications](https://go.microsoft.com/fwlink/?LinkId=99297) (Sugerencias y trucos de rendimiento en aplicaciones .NET)  

- [Rico Mariani's Performance Tidbits](https://go.microsoft.com/fwlink/?LinkId=115679) (Curiosidades sobre rendimiento de Rico Mariani)  

- [Blog de Saavedra Morrison](https://blogs.msdn.microsoft.com/vancem/)
  
## <a name="see-also"></a>Vea también

- [Rendimiento](index.md)
- [Guía de programación en Visual Basic](../../visual-basic/programming-guide/index.md)
- [Guía de programación de C#](../../csharp/programming-guide/index.md)
