---
title: ICLRMetaHost::RequestRuntimeLoadedNotification (Método)
ms.date: 03/30/2017
api_name:
- ICLRMetaHost.RequestRuntimeLoadedNotification
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRMetaHost::RequestRuntimeLoadedNotification
helpviewer_keywords:
- RequestRuntimeLoadedNotification method [.NET Framework hosting]
- ICLRMetaHost::RequestRuntimeLoadedNotification method [.NET Framework hosting]
ms.assetid: 0d5ccc4d-0193-41f5-af54-45d7b70d5321
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 539f69c33b67ad1a8a514062c5d777deaced1599
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965005"
---
# <a name="iclrmetahostrequestruntimeloadednotification-method"></a>ICLRMetaHost::RequestRuntimeLoadedNotification (Método)
Proporciona una función de devolución de llamada que se garantiza que se llamará cuando una versión de Common Language Runtime (CLR) se cargue por primera vez, pero no se haya iniciado todavía. Este método reemplaza a la función [LockClrVersion](../../../../docs/framework/unmanaged-api/hosting/lockclrversion-function.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT RequestRuntimeLoadedNotification (  
    [in] RuntimeLoadedCallbackFnPtr pCallbackFunction);  
```  
  
## <a name="parameters"></a>Parámetros  
 `pCallbackFunction`  
 de Función de devolución de llamada que se invoca cuando se ha cargado un nuevo tiempo de ejecución.  
  
## <a name="return-value"></a>Valor devuelto  
 Este método devuelve los siguientes HRESULT específicos y los errores HRESULT que indican un error del método.  
  
|HRESULT|DESCRIPCIÓN|  
|-------------|-----------------|  
|S_OK|El método se completó correctamente.|  
|E_POINTER|`pCallbackFunction` es null.|  
  
## <a name="remarks"></a>Comentarios  
 La devolución de llamada funciona de la siguiente manera:  
  
- La devolución de llamada se invoca solo cuando se carga por primera vez un tiempo de ejecución.  
  
- No se invoca la devolución de llamada para las cargas reentrantes del mismo tiempo de ejecución.  
  
- En el caso de las cargas de tiempo de ejecución no reentrantes, se serializan las llamadas a la función de devolución de llamada.  
  
 La función de devolución de llamada tiene el prototipo siguiente:  
  
```cpp  
typedef void (__stdcall *RuntimeLoadedCallbackFnPtr)(  
                     ICLRRuntimeInfo *pRuntimeInfo,  
                     CallbackThreadSetFnPtr pfnCallbackThreadSet,  
                     CallbackThreadUnsetFnPtr pfnCallbackThreadUnset);  
```  
  
 Los prototipos de función de devolución de llamada son los siguientes:  
  
- `pfnCallbackThreadSet`:  
  
    ```cpp  
    typedef HRESULT (__stdcall *CallbackThreadSetFnPtr)();  
    ```  
  
- `pfnCallbackThreadUnset`:  
  
    ```cpp  
    typedef HRESULT (__stdcall *CallbackThreadUnsetFnPtr)();  
    ```  
  
 Si el host intenta cargar o hacer que otro Runtime se cargue de forma reentrante, los `pfnCallbackThreadSet` parámetros y `pfnCallbackThreadUnset` que se proporcionan en la función de devolución de llamada deben usarse de la siguiente manera:  
  
- `pfnCallbackThreadSet`debe ser invocado por el subproceso que puede producir una carga en tiempo de ejecución antes de que se intente una carga de este tipo.  
  
- `pfnCallbackThreadUnset`se debe llamar a cuando el subproceso ya no producirá una carga de este tipo en tiempo de ejecución (y antes de devolver desde la devolución de llamada inicial).  
  
- `pfnCallbackThreadSet`y `pfnCallbackThreadUnset` son no reentrantes.  
  
> [!NOTE]
> Las aplicaciones host no deben `pfnCallbackThreadSet` llamar `pfnCallbackThreadUnset` a y `pCallbackFunction` fuera del ámbito del parámetro.  
  
## <a name="requirements"></a>Requisitos  
 **Select** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: Metahost. h  
  
 **Biblioteca** Se incluye como recurso en MSCorEE. dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [ICLRMetaHost (interfaz)](../../../../docs/framework/unmanaged-api/hosting/iclrmetahost-interface.md)
- [Hospedar aplicaciones de WPF](../../../../docs/framework/unmanaged-api/hosting/index.md)
