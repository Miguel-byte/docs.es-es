---
title: EXISTS (Entity SQL)
ms.date: 03/30/2017
ms.assetid: d28ead43-4afb-4bdc-af64-efd2e05005d7
ms.openlocfilehash: 44f128a292b013fd3a3a80efdd2d10a63e3cfb07
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833837"
---
# <a name="exists-entity-sql"></a>EXISTS (Entity SQL)
Determina si una colección está vacía.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
[NOT] EXISTS ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 `expression`  
 Expresión de consulta válida que devuelve una colección.  
  
 NOT  
 Especifica que el resultado de EXISTS se niega.  
  
## <a name="return-value"></a>Valor devuelto  
 `true` si la colección no está vacía; en caso contrario, `false`.  
  
## <a name="remarks"></a>Comentarios  
 EXISTS es uno de los operadores de conjuntos de [!INCLUDE[esql](../../../../../../includes/esql-md.md)]. Todos los operadores de conjuntos de [!INCLUDE[esql](../../../../../../includes/esql-md.md)] se evalúan de izquierda a derecha. Para obtener información sobre la prioridad de los operadores de conjuntos [!INCLUDE[esql](../../../../../../includes/esql-md.md)], vea [Except](except-entity-sql.md).  
  
## <a name="example"></a>Ejemplo  
 La siguiente consulta de Entity SQL usa el operador EXISTS para determinar si la colección está vacía. La consulta se basa en el modelo AdventureWorks Sales. Para compilar y ejecutar esta consulta, siga estos pasos:  
  
1. Siga el procedimiento descrito en [How para: Ejecute una consulta que devuelva los resultados de StructuralType @ no__t-0.  
  
2. Pase la consulta siguiente como argumento al método `ExecuteStructuralTypeQuery` :  
  
 [!code-sql[DP EntityServices Concepts#EXISTS](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#exists)]  
  
## <a name="see-also"></a>Vea también

- [Referencia de Entity SQL](entity-sql-reference.md)
