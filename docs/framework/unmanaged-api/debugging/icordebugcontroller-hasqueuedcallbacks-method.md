---
title: ICorDebugController::HasQueuedCallbacks (Método)
ms.date: 03/30/2017
api_name:
- ICorDebugController.HasQueuedCallbacks
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::HasQueuedCallbacks
helpviewer_keywords:
- HasQueuedCallbacks method [.NET Framework debugging]
- ICorDebugController::HasQueuedCallbacks method [.NET Framework debugging]
ms.assetid: 0d6a1cd9-370b-4462-adbf-e3980e897ea7
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0d17f51867b64780fca9b21c5f48c88db36343af
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67748785"
---
# <a name="icordebugcontrollerhasqueuedcallbacks-method"></a>ICorDebugController::HasQueuedCallbacks (Método)
Obtiene un valor que indica si las devoluciones de llamada administradas actualmente están en cola para el subproceso especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT HasQueuedCallbacks (  
    [in] ICorDebugThread *pThread,  
    [out] BOOL           *pbQueued  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `pThread`  
 [in] Un puntero a un objeto "ICorDebugThread" que representa el subproceso.  
  
 `pbQueued`  
 [out] Un puntero a un valor que es `true` si las devoluciones de llamada administradas actualmente están en cola para el subproceso especificado; de lo contrario, `false`.  
  
 Si se especifica null para el `pThread` parámetro, `HasQueuedCallbacks` devolverá `true` si hay actualmente en cola devoluciones de llamada administradas para cualquier subproceso.  
  
## <a name="remarks"></a>Comentarios  
 Las devoluciones de llamada será enviado a la vez, cada vez [ICorDebugController](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md) se llama. El depurador puede comprobar esta marca si desea informar a varios eventos de depuración que se producen simultáneamente.  
  
 Cuando se ponen en cola los eventos de depuración, ha ya se ha producido, por lo que el depurador debe vaciar la cola completa para asegurarse de que el estado del código depurado. (Llame a `ICorDebugController::Continue` para vaciar la cola.) Por ejemplo, si la cola contiene dos eventos de depuración en el subproceso *X*, y el depurador suspende el subproceso *X* después del primer evento de depuración y, a continuación, llamadas `ICorDebugController::Continue`, el segundo evento de depuración para subproceso *X* se distribuirán aunque el subproceso se ha suspendido.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vea también
