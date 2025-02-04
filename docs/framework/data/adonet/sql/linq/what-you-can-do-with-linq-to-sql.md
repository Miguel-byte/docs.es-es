---
title: Qué puede hacer con LINQ to SQL
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 061d98b2-baa7-4336-8ad2-c14de8134d91
ms.openlocfilehash: 8baf361ba66ba33927121ae20edcc6c12964c21c
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792097"
---
# <a name="what-you-can-do-with-linq-to-sql"></a>Qué puede hacer con LINQ to SQL
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] admite toda la funcionalidad clave que puede esperar un programador de SQL. Puede consultar, insertar, actualizar y eliminar información en las tablas.  
  
## <a name="selecting"></a>Selección  
 Para la selección (*proyección*), basta con que escriba una consulta [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] en su propio lenguaje de programación y, después, la ejecute para recuperar los resultados. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] traduce automáticamente todas las operaciones necesarias a las operaciones SQL correspondientes con la que ya está familiarizado. Para obtener más información, consulta [LINQ to SQL](index.md).  
  
 En el ejemplo siguiente se recuperan los nombres de las compañías de los clientes de Londres y se muestran en la ventana de la consola.  
  
 [!code-csharp[DLinqGettingStarted#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqGettingStarted/cs/Program.cs#1)]
 [!code-vb[DLinqGettingStarted#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqGettingStarted/vb/Module1.vb#1)]  
  
## <a name="inserting"></a>Inserción  
 Para realizar una operación `Insert`de SQL, basta con que agregue objetos al modelo de objetos que ha creado y llame a <xref:System.Data.Linq.DataContext.SubmitChanges%2A> en <xref:System.Data.Linq.DataContext>.  
  
 En el ejemplo siguiente se agrega un nuevo cliente, e información sobre el cliente, a la tabla `Customers` utilizando el método <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A>.  
  
 [!code-csharp[DLinqGettingStarted#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqGettingStarted/cs/Program.cs#2)]
 [!code-vb[DLinqGettingStarted#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqGettingStarted/vb/Module1.vb#2)]  
  
## <a name="updating"></a>Updating  
 Para realizar una operación `Update` en una entrada de base de datos, primero recupere el elemento y modifíquelo directamente en el modelo de objetos. Después de haber modificado el objeto, llame a <xref:System.Data.Linq.DataContext.SubmitChanges%2A> en <xref:System.Data.Linq.DataContext> para actualizar la base de datos.  
  
 En el ejemplo siguiente se recuperan todos los clientes que son de Londres. A continuación, el nombre de la ciudad se cambia de "London" a "London - Metro". Finalmente, se llama a <xref:System.Data.Linq.DataContext.SubmitChanges%2A> para enviar los cambios a la base de datos.  
  
 [!code-csharp[DLinqGettingStarted#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqGettingStarted/cs/Program.cs#3)]
 [!code-vb[DLinqGettingStarted#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqGettingStarted/vb/Module1.vb#3)]  
  
## <a name="deleting"></a>Eliminando  
 Para realizar una operación `Delete` en un elemento, quite el elemento de la colección a la que pertenece y, a continuación, llame al método <xref:System.Data.Linq.DataContext.SubmitChanges%2A> en <xref:System.Data.Linq.DataContext> para confirmar el cambio.  
  
> [!NOTE]
> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] no reconoce las operaciones de eliminación en cascada. Si desea eliminar una fila de una tabla que tiene restricciones, consulte [How to: Eliminar filas de la base](how-to-delete-rows-from-the-database.md)de datos.  
  
 En el ejemplo siguiente, se recupera el cliente cuyo `CustomerID` es `98128` de la base de datos. A continuación, después de confirmar que se recuperó la fila del cliente, se llama a <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A> para quitar ese objeto de la colección. Finalmente, se llama a <xref:System.Data.Linq.DataContext.SubmitChanges%2A> para transmitir la eliminación a la base de datos.  
  
 [!code-csharp[DLinqGettingStarted#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqGettingStarted/cs/Program.cs#4)]
 [!code-vb[DLinqGettingStarted#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqGettingStarted/vb/Module1.vb#4)]  
  
## <a name="see-also"></a>Vea también

- [Guía de programación](programming-guide.md)
- [Modelo de objetos de LINQ to SQL](the-linq-to-sql-object-model.md)
- [Introducción](getting-started.md)
