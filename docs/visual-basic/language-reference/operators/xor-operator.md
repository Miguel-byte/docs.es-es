---
title: Xor (Operador, Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Xor
helpviewer_keywords:
- exclusive OR operator [Visual Basic]
- logical exclusion
- operators [Visual Basic], exclusive or
- exclusion operator [Visual Basic]
- operators [Visual Basic], bitwise
- bitwise operators [Visual Basic], XOR operator
- Xor operator [Visual Basic]
- Xor keyword [Visual Basic]
- bitwise comparison [Visual Basic]
ms.assetid: 036000a9-3934-4e7f-a9d0-a816de3d84a6
ms.openlocfilehash: d82018a3018e2cf4362b9904ed127c20f56f6f0c
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701272"
---
# <a name="xor-operator-visual-basic"></a>Xor (Operador, Visual Basic)
Realiza una exclusión lógica en dos expresiones `Boolean` o una exclusión bit a bit en dos expresiones numéricas.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
result = expression1 Xor expression2  
```  
  
## <a name="parts"></a>Elementos  
 `result`  
 Obligatorio. Cualquier variable `Boolean` o Numeric. En la comparación booleana, `result` es la exclusión lógica (disyunción lógica exclusiva) de dos valores `Boolean`. Para las operaciones bit a bit, `result` es un valor numérico que representa la exclusión bit a bit (disyunción bit a bit exclusiva) de dos modelos de bits numéricos.  
  
 `expression1`  
 Obligatorio. Cualquier `Boolean` expresión numérica o.  
  
 `expression2`  
 Obligatorio. Cualquier `Boolean` expresión numérica o.  
  
## <a name="remarks"></a>Comentarios  
 En la comparación booleana, `result` es `True` si y solo si exactamente uno de `expression1` y `expression2` se evalúa en `True`. Es decir, si y solo si `expression1` y `expression2` se evalúan como valores de @no__t 2 opuestos. En la tabla siguiente se muestra cómo se determina `result`.  
  
|Si `expression1` es|Y `expression2` es|El valor de `result` es|  
|-------------------------|--------------------------|------------------------------|  
|`True`|`True`|`False`|  
|`True`|`False`|`True`|  
|`False`|`True`|`True`|  
|`False`|`False`|`False`|  
  
> [!NOTE]
> En una comparación booleana, el operador `Xor` siempre evalúa ambas expresiones, lo que podría incluir la realización de llamadas a procedimientos. No hay ningún homólogo de cortocircuito en `Xor`, porque el resultado siempre depende de ambos operandos. Para los operadores lógicos de *cortocircuito* , vea [operador AndAlso](../../../visual-basic/language-reference/operators/andalso-operator.md) y [operador OrElse](../../../visual-basic/language-reference/operators/orelse-operator.md).  
  
 Para las operaciones bit a bit, el operador `Xor` realiza una comparación bit a bit de los bits colocados de forma idéntica en dos expresiones numéricas y establece el bit correspondiente en `result` según la tabla siguiente.  
  
|Si el bit de `expression1` es|Y bit en `expression2` es|El bit en `result` es|  
|--------------------------------|---------------------------------|----------------------------|  
|1|1|0|  
|1|0|1|  
|0|1|1|  
|0|0|0|  
  
> [!NOTE]
> Puesto que los operadores lógicos y bit a bit tienen una prioridad más baja que otros operadores aritméticos y relacionales, las operaciones bit a bit deben ir entre paréntesis para garantizar una ejecución precisa.  
  
 Por ejemplo, 5 `Xor` 3 es 6. Para ver por qué es así, convierta 5 y 3 en sus representaciones binarias, 101 y 011. A continuación, use la tabla anterior para determinar que 101 XOR 011 es 110, que es la representación binaria del número decimal 6.  
  
## <a name="data-types"></a>Tipos de datos  
 Si los operandos constan de una expresión `Boolean` y una expresión numérica, Visual Basic convierte la expresión `Boolean` a un valor numérico (-1 para `True` y 0 para `False`) y realiza una operación bit a bit.  
  
 Para una comparación `Boolean`, el tipo de datos del resultado es `Boolean`. En una comparación bit a bit, el tipo de datos del resultado es un tipo numérico adecuado para los tipos de datos de `expression1` y `expression2`. Vea la tabla "comparaciones relacionales y bit a bit" en [tipos de datos de resultados de operadores](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md).  
  
## <a name="overloading"></a>Sobrecarga  
 El operador `Xor` se puede *sobrecargar*, lo que significa que una clase o estructura puede volver a definir su comportamiento cuando un operando tiene el tipo de esa clase o estructura. Si el código usa este operador en una clase o estructura de este tipo, asegúrese de que entiende su comportamiento redefinido. Para obtener más información, consulta [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se usa el operador `Xor` para realizar una exclusión lógica (disyunción lógica exclusiva) en dos expresiones. El resultado es un valor `Boolean` que indica si exactamente una de las expresiones es `True`.  
  
 [!code-vb[VbVbalrOperators#40](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#40)]  
  
 En el ejemplo anterior se generan los resultados de `False`, `True` y `False`, respectivamente.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se usa el operador `Xor` para realizar una exclusión lógica (disyunción lógica exclusiva) en los bits individuales de dos expresiones numéricas. El bit en el patrón del resultado se establece si exactamente uno de los bits correspondientes de los operandos está establecido en 1.  
  
 [!code-vb[VbVbalrOperators#41](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#41)]  
  
 En el ejemplo anterior se generan los resultados de 2, 12 y 14, respectivamente.  
  
## <a name="see-also"></a>Vea también

- [Operadores lógicos y bit a bit (Visual Basic)](../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)
- [Prioridad de operador en Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [Operadores enumerados por funcionalidad](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [Operadores lógicos y bit a bit en Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)
