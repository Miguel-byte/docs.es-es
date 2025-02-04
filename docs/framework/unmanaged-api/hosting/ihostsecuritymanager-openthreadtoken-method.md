---
title: IHostSecurityManager::OpenThreadToken (Método)
ms.date: 03/30/2017
api_name:
- IHostSecurityManager.OpenThreadToken
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostSecurityManager::OpenThreadToken
helpviewer_keywords:
- IHostSecurityManager::OpenThreadToken method [.NET Framework hosting]
- OpenThreadToken method [.NET Framework hosting]
ms.assetid: d5999052-8bf0-4a9e-8621-da6284406b18
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c1beeb0ff6b2e3493f0814fc3371f189bd4d485d
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67778013"
---
# <a name="ihostsecuritymanageropenthreadtoken-method"></a>IHostSecurityManager::OpenThreadToken (Método)
Se abre el token de acceso discrecional asociado con el subproceso actualmente en ejecución.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT OpenThreadToken (  
    [in]  DWORD    dwDesiredAccess,   
    [in]  BOOL     bOpenAsSelf,   
    [out] HANDLE   *phThreadToken  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `dwDesiredAccess`  
 [in] Una máscara de valores de acceso que especifican los tipos de acceso para el token de subproceso solicitados. Estos valores se definen en Win32 `OpenThreadToken` función. Los tipos de acceso solicitados se reconcilian con la lista de control de acceso discrecional (DACL) para determinar qué tipos de acceso para conceder o denegar del token.  
  
 `bOpenAsSelf`  
 [in] `true` para especificar que se debe realizar la comprobación de acceso utilizando el contexto de seguridad del proceso para el subproceso que realiza la llamada; `false` para especificar que la comprobación de acceso debe realizarse utilizando el contexto de seguridad para el subproceso de llamada. Si el subproceso está suplantando a un cliente, el contexto de seguridad puede ser de un proceso de cliente.  
  
 `phThreadToken`  
 [out] Un puntero al token de acceso recién abierto.  
  
## <a name="return-value"></a>Valor devuelto  
  
|HRESULT|DESCRIPCIÓN|  
|-------------|-----------------|  
|S_OK|`OpenThreadToken` se devolvió correctamente.|  
|HOST_E_CLRNOTAVAILABLE|Common language runtime (CLR) no se ha cargado en un proceso o el CLR se encuentra en un estado en el que no se puede ejecutar código administrado o procesar la llamada correctamente.|  
|HOST_E_TIMEOUT|La llamada ha agotado el tiempo de espera.|  
|HOST_E_NOT_OWNER|El llamador no posee el bloqueo.|  
|HOST_E_ABANDONED|Se canceló un evento mientras un subproceso bloqueado o fibra estaba esperando en ella.|  
|E_FAIL|Se ha producido un error irrecuperable desconocido. Cuando un método devuelve E_FAIL, CLR ya no es utilizable dentro del proceso. Las llamadas posteriores a métodos de hospedaje devuelven HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentarios  
 `IHostSecurityManager::OpenThreadToken` se comporta de manera similar a la función de Win32 correspondiente del mismo nombre, salvo que la función de Win32 permite que el llamador pase un identificador a un subproceso arbitrario, mientras `IHostSecurityManager::OpenThreadToken` sólo abre el token asociado al subproceso que realiza la llamada.  
  
 El `HANDLE` tipo no es compatible con COM, es decir, su tamaño es específico para el sistema operativo y requiere cálculo de referencias personalizado. Por lo tanto, este token es para su uso solo dentro del proceso, entre CLR y el host.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: MSCorEE.h  
  
 **Biblioteca:** Incluye como recurso en MSCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [IHostSecurityContext (interfaz)](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritycontext-interface.md)
- [IHostSecurityManager (interfaz)](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritymanager-interface.md)
