---
title: IHostTaskManager::LeaveRuntime (Método)
ms.date: 03/30/2017
api_name:
- IHostTaskManager.LeaveRuntime
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTaskManager::LeaveRuntime
helpviewer_keywords:
- IHostTaskManager::LeaveRuntime method [.NET Framework hosting]
- LeaveRuntime method [.NET Framework hosting]
ms.assetid: 43689cc4-e48e-46e5-a22d-bafd768b8759
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8b2e8e636915b3921fcd727fc78a3fb18fc69104
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69959033"
---
# <a name="ihosttaskmanagerleaveruntime-method"></a>IHostTaskManager::LeaveRuntime (Método)
Notifica al host que la tarea que se está ejecutando actualmente está a punto de abandonar el Common Language Runtime (CLR) y especificar código no administrado.  
  
> [!IMPORTANT]
> Una llamada correspondiente a [IHostTaskManager:: EnterRuntime (](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-enterruntime-method.md) notifica al host que la tarea que se está ejecutando actualmente está reentrando el código administrado.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT LeaveRuntime (  
    [in] SIZE_T target  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `target`  
 de Dirección dentro del archivo ejecutable portable asignado de la función no administrada a la que se va a llamar.  
  
## <a name="return-value"></a>Valor devuelto  
  
|HRESULT|DESCRIPCIÓN|  
|-------------|-----------------|  
|S_OK|`LeaveRuntime`se devolvió correctamente.|  
|HOST_E_CLRNOTAVAILABLE|CLR no se ha cargado en un proceso o CLR está en un estado en el que no puede ejecutar código administrado ni procesar la llamada correctamente.|  
|HOST_E_TIMEOUT|Se agotó el tiempo de espera de la llamada.|  
|HOST_E_NOT_OWNER|El autor de la llamada no posee el bloqueo.|  
|HOST_E_ABANDONED|Se canceló un evento mientras un subproceso o fibra bloqueados estaba esperando en él.|  
|E_FAIL|Se produjo un error grave desconocido. Cuando un método devuelve E_FAIL, el CLR ya no se puede usar en el proceso. Las llamadas subsiguientes a métodos de hospedaje devuelven HOST_E_CLRNOTAVAILABLE.|  
|E_OUTOFMEMORY|No hay suficiente memoria disponible para completar la asignación solicitada.|  
  
## <a name="remarks"></a>Comentarios  
 Las secuencias de llamadas a y desde código no administrado se pueden anidar. Por ejemplo, en la lista siguiente se describe una situación hipotética en la que la secuencia `LeaveRuntime`de llamadas a, [IHostTaskManager:: ReverseEnterRuntime](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-reverseenterruntime-method.md), [IHostTaskManager:: ReverseLeaveRuntime](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-reverseleaveruntime-method.md), y `IHostTaskManager::EnterRuntime` permite al host Identifique las capas anidadas.  
  
|.|Llamada al método correspondiente|  
|------------|-------------------------------|  
|Un ejecutable de Visual Basic administrado llama a una función no administrada escrita en C mediante la invocación de plataforma.|`IHostTaskManager::LeaveRuntime`|  
|La función de C no administrada llama a un método en un archivo DLL C#administrado escrito en.|`IHostTaskManager::ReverseEnterRuntime`|  
|La función C# administrada llama a otra función no administrada escrita en C, también mediante la invocación de plataforma.|`IHostTaskManager::LeaveRuntime`|  
|La segunda función no administrada devuelve la ejecución a C# la función.|`IHostTaskManager::EnterRuntime`|  
|La C# función devuelve la ejecución a la primera función no administrada.|`IHostTaskManager::ReverseLeaveRuntime`|  
|La primera función no administrada devuelve la ejecución al programa Visual Basic.|`IHostTaskManager::EnterRuntime`|  
  
## <a name="requirements"></a>Requisitos  
 **Select** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: MSCorEE.h  
  
 **Biblioteca** Se incluye como recurso en MSCorEE. dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [ICLRTask (interfaz)](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)
- [ICLRTaskManager (interfaz)](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-interface.md)
- [IHostTask (interfaz)](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)
- [IHostTaskManager (interfaz)](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-interface.md)
