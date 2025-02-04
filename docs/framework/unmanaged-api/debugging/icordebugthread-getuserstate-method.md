---
title: ICorDebugThread::GetUserState (Método)
ms.date: 03/30/2017
api_name:
- ICorDebugThread.GetUserState
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::GetUserState
helpviewer_keywords:
- GetUserState method, ICorDebugThread interface [.NET Framework debugging]
- ICorDebugThread::GetUserState method [.NET Framework debugging]
ms.assetid: ae0cfd73-8ead-4d36-9310-dccaac9db0bd
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f7d3325c8aee44849ff1fb7a6cc06a0ed7c2c6f8
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67769103"
---
# <a name="icordebugthreadgetuserstate-method"></a>ICorDebugThread::GetUserState (Método)
Obtiene el estado de usuario actual de esta instancia de ICorDebugThread.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT GetUserState (  
    [out] CorDebugUserState   *pState  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `pState`  
 [out] Un puntero a una combinación bit a bit de valores de enumeración CorDebugUserState que describen el estado de usuario actual de este subproceso.  
  
## <a name="remarks"></a>Comentarios  
 El estado de usuario del subproceso es el estado del subproceso cuando lo examina el programa que se está depurando. Un subproceso puede tener varios bits de estado establecida.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
