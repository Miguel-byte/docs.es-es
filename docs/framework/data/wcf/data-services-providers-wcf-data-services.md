---
title: Proveedores de Data Services (Data Services de WCF)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, providers
ms.assetid: a0160b1b-3d9c-4cc8-8391-cb0986a60a41
ms.openlocfilehash: 7623c2b743d6a61362c8cf0e1228b4663c9e7d48
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2019
ms.locfileid: "70780390"
---
# <a name="data-services-providers-wcf-data-services"></a>Proveedores de Data Services (Data Services de WCF)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]admite varios modelos de proveedor para exponer los datos como [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] una fuente. En este tema se proporciona información con el fin de permitirle seleccionar el proveedor de [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] más adecuado para su origen de datos.  
  
## <a name="data-source-providers"></a>Proveedores de orígenes de datos  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]admite los siguientes proveedores para definir el modelo de datos de un servicio de datos.  
  
|Proveedor|DESCRIPCIÓN|  
|--------------|-----------------|  
|Proveedor de Entity Framework|Este proveedor utiliza ADO.NET Entity Framework para permitir el uso de datos relacionales con un servicio de datos definiendo un modelo de datos que se asigne a datos relacionales. Su origen de datos puede ser SQL Server o cualquier otro origen de datos con compatibilidad de otros proveedores para Entity Framework. Debería usar el proveedor de Entity Framework cuando tenga un origen de datos relacional, como una base de datos SQL Server. Para obtener más información, vea [proveedor de Entity Framework](entity-framework-provider-wcf-data-services.md).|  
|Proveedor de reflexión|Este proveedor utiliza la reflexión para permitir la definición de un modelo de datos basado en las clases de datos existente que se pueden exponer como instancias de la interfaz <xref:System.Linq.IQueryable%601>. Las actualizaciones se habilitan implementando la interfaz <xref:System.Data.Services.IUpdatable>. Debe usar este proveedor cuando tenga clases de datos estáticas que se definen en tiempo de ejecución, como aquellas generadas por LINQ para SQL o las definidas por un conjunto de datos con tipo. Para obtener más información, vea [proveedor de reflexión](reflection-provider-wcf-data-services.md).|  
|Proveedores de servicios de datos personalizados|[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] incluye un conjunto de proveedores que le permiten definir de forma dinámica un modelo de datos basado en tipos de datos enlazados en tiempo de ejecución. Debería implementar estas interfaces cuando no se conozcan los datos que se están exponiendo, cuando se esté diseñando la aplicación o cuando los proveedores de Entity Framework o de reflexión no sean suficientes. Para obtener más información, vea [proveedores de servicios de datos personalizados](custom-data-service-providers-wcf-data-services.md).|  
  
## <a name="other-data-service-providers"></a>Otros proveedores de servicios de datos  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]tiene el siguiente proveedor de servicios de datos adicional que mejora el rendimiento de un origen de datos definido mediante uno de los otros proveedores.  
  
|Proveedor|DESCRIPCIÓN|  
|--------------|-----------------|  
|Proveedor de transmisiones por secuencias|Este proveedor permite exponer tipos de datos de objetos binarios grandes usando [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]. Si implementa la interfaz <xref:System.Data.Services.Providers.IDataServiceStreamProvider>, se crea un proveedor de transmisiones por secuencias. Este proveedor se puede implementar junto con cualquier proveedor de orígenes de datos. Para obtener más información, consulte [proveedor de streaming](streaming-provider-wcf-data-services.md).|  
  
## <a name="see-also"></a>Vea también

- [Definir Servicios de datos de WCF](defining-wcf-data-services.md)
- [Configuración del servicio de datos](configuring-the-data-service-wcf-data-services.md)
- [Hospedaje del servicio de datos](hosting-the-data-service-wcf-data-services.md)
