---
title: LIKE (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 8300e6d2-875b-481e-9ef4-e1e7c12d46fa
ms.openlocfilehash: fbe27f6e25c9d69f092a060fa2c3fbf0abc93318
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2019
ms.locfileid: "70250514"
---
# <a name="like-entity-sql"></a>LIKE (Entity SQL)
Determina si un elemento `String` de caracteres específico coincide con un patrón especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
match [NOT] LIKE pattern [ESCAPE escape]  
```  
  
## <a name="arguments"></a>Argumentos  
 `match`  
 Expresión que se evalúa como un `String`. [!INCLUDE[esql](../../../../../../includes/esql-md.md)]  
  
 `pattern`  
 Patrón que va a coincidir con el elemento `String` especificado.  
  
 `escape`  
 Carácter de escape.  
  
 NOT  
 Especifica que el resultado de LIKE se niega.  
  
## <a name="return-value"></a>Valor devuelto  
 `true` si el elemento `string` coincide con el patrón; de lo contrario, `false`.  
  
## <a name="remarks"></a>Comentarios  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]las expresiones que usan el operador LIKE se evalúan de la misma manera que las expresiones que usan igualdad como criterio de filtro. Sin embargo [!INCLUDE[esql](../../../../../../includes/esql-md.md)] , las expresiones que usan el operador like pueden incluir literales y caracteres comodín.  
  
 En la tabla siguiente se describe la sintaxis del patrón `string`.  
  
|Carácter comodín|DESCRIPCIÓN|Ejemplo|  
|------------------------|-----------------|-------------|  
|%|Cualquier elemento `string` de cero o más caracteres.|`title like '%computer%'`busca todos los títulos con la `"computer"` palabra en cualquier parte del título.|  
|_ (carácter de subrayado)|Cualquier carácter individual.|`firstname like '_ean'`busca todos los nombres de cuatro letras que terminan `"ean`en, "como Dean o Juan.|  
|[ ]|Cualquier carácter individual del intervalo ([a-f]) o del conjunto ([abcdef]) que se han especificado.|`lastname like '[C-P]arsen'`busca los apellidos que terminan en "Arsen" y comienza con cualquier carácter individual entre C y P, como Carsen o Larsen.|  
|[^]|Cualquier carácter individual no incluido en el intervalo ([^a-f]) o del conjunto ([^abcdef]) que se han especificado.|`lastname like 'de[^l]%'`busca todos los apellidos que comienzan por "de" y no incluyen "l" como la siguiente letra.|  
  
> [!NOTE]
> El operador LIKE y la cláusula ESCAPE de [!INCLUDE[esql](../../../../../../includes/esql-md.md)] no se pueden aplicar a los valores `System.DateTime` o `System.Guid`.  
  
 LIKE admite operaciones de búsqueda de coincidencias de patrón ASCII y Unicode. Cuando todos los parámetros son caracteres ASCII, se realiza la operación de búsqueda de coincidencias de patrón ASCII. Si uno o más argumentos son Unicode, todos los argumentos se convierten a Unicode y se realiza la operación de búsqueda de coincidencias de patrón Unicode. Cuando se utiliza Unicode con LIKE, los espacios en blanco al final son significativos; sin embargo, no lo son para los datos que no son Unicode. La sintaxis de la cadena [!INCLUDE[esql](../../../../../../includes/esql-md.md)] de patrón de es la misma que la de Transact-SQL.  
  
 Un patrón puede contener caracteres normales y caracteres comodín. Durante la operación de búsqueda de coincidencias de patrón, los caracteres normales deben coincidir exactamente con los caracteres especificados en el elemento `string` de caracteres. Sin embargo, los caracteres comodín pueden coincidir con fragmentos arbitrarios de la cadena de caracteres. Cuando se utiliza con caracteres comodín, el operador LIKE es más flexible que los operadores de comparación de cadenas = y !=.  
  
> [!NOTE]
> Puede utilizar extensiones específicas del proveedor si el destino es un proveedor concreto. Sin embargo, otros proveedores pueden tratar de manera diferente este tipo de estructuras. SqlServer admite patrones [primero-último] y [^primero-último] donde el primero coincide exactamente con un carácter entre el primero y el último, y el segundo coincide exactamente con un carácter que no está entre el primero y el último.  
  
### <a name="escape"></a>Escape  
 El uso de la cláusula ESCAPE permite buscar cadenas de caracteres que incluyen uno o más de los caracteres comodín especiales que se describen en la tabla de la sección anterior. Por ejemplo, suponga que varios documentos incluyen el literal "100%" en el título y desea buscar todos esos documentos. Debido a que el porcentaje (%) el carácter es un carácter comodín, debe escapar mediante la [!INCLUDE[esql](../../../../../../includes/esql-md.md)] cláusula escape para ejecutar la búsqueda correctamente. A continuación se muestra un ejemplo de este filtro.  
  
```  
"title like '%100!%%' escape '!'"  
```  
  
 En esta expresión de búsqueda, el carácter comodín de porcentaje (%) situado inmediatamente después del carácter de exclamación (!) se trata como literal, en lugar de como carácter comodín. Puede usar cualquier carácter como carácter de escape, excepto los [!INCLUDE[esql](../../../../../../includes/esql-md.md)] caracteres comodín y los caracteres de corchete (`[ ]`). En el ejemplo anterior, el carácter de exclamación (!) es el carácter de escape.  
  
## <a name="example"></a>Ejemplo  
 Las dos [!INCLUDE[esql](../../../../../../includes/esql-md.md)] consultas siguientes utilizan los operadores Like y escape para determinar si una cadena de caracteres específica coincide con un patrón especificado. La primera consulta busca el `Name` que empieza con los caracteres. `Down_` Esta consulta utiliza la opción ESCAPE porque el carácter de subrayado (`_`) es un carácter comodín. Sin especificar la opción ESCAPE, la consulta buscaría valores de `Name` que empezasen con la palabra `Down` seguida de cualquier carácter individual diferente del carácter de subrayado. Las consultas se basan en el modelo AdventureWorks Sales. Para compilar y ejecutar esta consulta, siga estos pasos:  
  
1. Siga el procedimiento descrito [en cómo: Ejecuta una consulta que devuelve resultados](../how-to-execute-a-query-that-returns-primitivetype-results.md)PrimitiveType.  
  
2. Pase la consulta siguiente como argumento al método `ExecutePrimitiveTypeQuery` :  
  
 [!code-csharp[DP EntityServices Concepts 2#LIKE](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#like)]  
  
## <a name="see-also"></a>Vea también

- [Referencia de Entity SQL](entity-sql-reference.md)
