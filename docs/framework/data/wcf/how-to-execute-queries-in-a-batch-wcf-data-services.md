---
title: Procedimiento Ejecutar consultas en un lote (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, batch requests
ms.assetid: 3b4db7df-bd33-43a1-8ea4-63a18e131f97
ms.openlocfilehash: a825fe83ff62d935740fb69871ba2d1e2120e9ec
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2019
ms.locfileid: "70790496"
---
# <a name="how-to-execute-queries-in-a-batch-wcf-data-services"></a>Procedimiento Ejecutar consultas en un lote (WCF Data Services)
Mediante el uso [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] de la biblioteca de cliente, puede ejecutar más de una consulta en el servicio de datos en un único lote. Para obtener más información, vea [operaciones de procesamiento por lotes](batching-operations-wcf-data-services.md).  
  
 En el ejemplo de este tema se usa el servicio de datos de ejemplo Northwind y las clases del servicio de datos de cliente generadas automáticamente. Este servicio y las clases de datos de cliente se crean al completar la guía de [Inicio rápido de WCF Data Services](quickstart-wcf-data-services.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo llamar al método <xref:System.Data.Services.Client.DataServiceContext.ExecuteBatch%2A> para ejecutar una matriz de los objetos <xref:System.Data.Services.Client.DataServiceRequest%601> que contiene consultas que devuelven objetos `Customers` y `Products` del servicio de datos de Northwind. La colección de objetos <xref:System.Data.Services.Client.QueryOperationResponse%601> del objeto <xref:System.Data.Services.Client.DataServiceResponse> devuelto es de tipo enumerado y la colección de objetos contenida en cada <xref:System.Data.Services.Client.QueryOperationResponse%601> también lo es.  
  
 [!code-csharp[Astoria Northwind Client#BatchQuery](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#batchquery)]
 [!code-vb[Astoria Northwind Client#BatchQuery](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#batchquery)]  
  
## <a name="see-also"></a>Vea también

- [Biblioteca cliente de Servicios de datos de WCF](wcf-data-services-client-library.md)
