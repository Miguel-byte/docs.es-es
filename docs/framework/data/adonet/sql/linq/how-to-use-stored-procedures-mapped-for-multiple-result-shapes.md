---
title: Procedimiento para usar procedimientos almacenados asignados en varias formas de resultados
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c2b84dfe-7fec-489a-92de-45215cec4518
ms.openlocfilehash: d32faf026789923ca4343271c9fd1b6bbdb068df
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793096"
---
# <a name="how-to-use-stored-procedures-mapped-for-multiple-result-shapes"></a>Procedimiento para usar procedimientos almacenados asignados en varias formas de resultados
Cuando un procedimiento almacenado puede devolver varias formas de resultados, el tipo de valor devuelto no puede estar fuertemente tipado para una forma de proyección única. Aunque [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] puede generar todos los tipos de proyección posibles, no puede conocer el orden en que se devolverán.  
  
 Compare este escenario con los procedimientos almacenados que generan varias formas de resultados secuencialmente. Para obtener más información, consulte [Cómo Use procedimientos almacenados asignados para las formas](how-to-use-stored-procedures-mapped-for-sequential-result-shapes.md)de resultados secuenciales.  
  
 El atributo <xref:System.Data.Linq.Mapping.ResultTypeAttribute> se aplica a los procedimientos almacenados que devuelven varios tipos de resultados para especificar el conjunto de tipos que el procedimiento puede devolver.  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo de código SQL, la forma del resultado depende de la entrada (`shape =1` o `shape = 2`). No se sabe qué proyección se devolverá primero.  
  
```  
CREATE PROCEDURE VariableResultShapes(@shape int)  
AS  
if(@shape = 1)  
    select CustomerID, ContactTitle, CompanyName from customers  
else if(@shape = 2)  
    select OrderID, ShipName from orders  
```  
  
 [!code-csharp[DLinqSprox#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSprox/cs/northwind-sprox.cs#4)]
 [!code-vb[DLinqSprox#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSprox/vb/northwind-sprox.vb#4)]  
  
## <a name="example"></a>Ejemplo  
 Usaría código similar al siguiente para ejecutar este procedimiento almacenado.  
  
> [!NOTE]
> Debe utilizar el patrón <xref:System.Data.Linq.IMultipleResults.GetResult%2A> para obtener un enumerador del tipo correcto, basado en su conocimiento del procedimiento almacenado.  
  
 [!code-csharp[DLinqSprox#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSprox/cs/Program.cs#5)]
 [!code-vb[DLinqSprox#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSprox/vb/Module1.vb#5)]  
  
## <a name="see-also"></a>Vea también

- [Procedimientos almacenados](stored-procedures.md)
