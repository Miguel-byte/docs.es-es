---
title: EClrOperation (Enumeración)
ms.date: 03/30/2017
api_name:
- EClrOperation
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EClrOperation
helpviewer_keywords:
- EClrOperation enumeration [.NET Framework hosting]
ms.assetid: 5aef6808-5aac-4b2f-a2c7-fee1575c55ed
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 01b000ed3d75ddb6a7882cb8f03ff2cec64fb9fe
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67767875"
---
# <a name="eclroperation-enumeration"></a>EClrOperation (Enumeración)
Describe el conjunto de operaciones para que un host puede aplicar acciones de directiva.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
typedef enum {  
    OPR_ThreadAbort,  
    OPR_ThreadRudeAbortInNonCriticalRegion,  
    OPR_ThreadRudeAbortInCriticalRegion,  
    OPR_AppDomainUnload,  
    OPR_AppDomainRudeUnload,  
    OPR_ProcessExit,  
    OPR_FinalizerRun  
} EClrOperation;  
```  
  
## <a name="members"></a>Miembros  
  
|Member|DESCRIPCIÓN|  
|------------|-----------------|  
|`OPR_AppDomainRudeUnload`|El host puede especificar acciones de directiva va a realizarse cuando un <xref:System.AppDomain> se descargan de forma que no sea estable (forzada).|  
|`OPR_AppDomainUnload`|El host puede especificar acciones de directiva va a realizarse cuando un <xref:System.AppDomain> se descarga.|  
|`OPR_FinalizerRun`|El host puede especificar acciones de directiva que se realizarán cuando ejecutan los finalizadores.|  
|`OPR_ProcessExit`|El host puede especificar acciones de directiva que se realizará cuando se cierra el proceso.|  
|`OPR_ThreadAbort`|El host puede especificar acciones de directiva que se realizará cuando se anula un subproceso.|  
|`OPR_ThreadRudeAbortInCriticalRegion`|El host puede especificar acciones de directiva que se realizarán cuando se produce una anulación a la fuerza en una región crítica del código.|  
|`OPR_ThreadRudeAbortInNonCriticalRegion`|El host puede especificar acciones de directiva que se realizará cuando se produzca una anulación a la fuerza en una región no crítica del código.|  
  
## <a name="remarks"></a>Comentarios  
 La infraestructura de confiabilidad de common language runtime (CLR) distingue entre recursos y las anulaciones de errores de asignación que se producen en regiones críticas del código y las que se producen en las regiones no críticas de código. Esta distinción está diseñada para permitir que los hosts establecer directivas distintas dependiendo de dónde se produce un error en el código.  
  
 Un *región crítica del código* cualquier espacio que el CLR no puede garantizar que no puede completar una solicitud para los recursos afectará únicamente a la tarea actual o anulación de una tarea. Por ejemplo, si una tarea mantiene un bloqueo y recibe un valor HRESULT que indica un error al realizar una solicitud de asignación de memoria, es suficiente con anular la tarea para garantizar la estabilidad de la <xref:System.AppDomain>, porque el <xref:System.AppDomain> podría contener otros tareas en espera para el mismo bloqueo. Para abandonar actual tarea podría provocar que deje de responder esas otras tareas. En tal caso, el host necesita la capacidad de descargar toda la <xref:System.AppDomain> en lugar de riesgo potencial de inestabilidad.  
  
 Un *región no crítica del código*, por otro lado, es una región en el CLR puede garantizar que una anulación o un error afectará únicamente a la tarea en el que se produce el error.  
  
 CLR también distingue entre estables y que no sea estable forzadas. En general, una anulación normal o correcta hace todo lo posible para ejecutar rutinas y los finalizadores de control de excepciones antes de anular una tarea, mientras que una anulación a la fuerza ofrece ninguna garantía de este tipo.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: MSCorEE.h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [EClrFailure (enumeración)](../../../../docs/framework/unmanaged-api/hosting/eclrfailure-enumeration.md)
- [EPolicyAction (enumeración)](../../../../docs/framework/unmanaged-api/hosting/epolicyaction-enumeration.md)
- [ICLRPolicyManager (interfaz)](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-interface.md)
- [IHostPolicyManager (interfaz)](../../../../docs/framework/unmanaged-api/hosting/ihostpolicymanager-interface.md)
- [Enumeraciones para hosts](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
