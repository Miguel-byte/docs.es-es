---
title: ICorDebugRegisterSet2::GetRegistersAvailable (Método)
ms.date: 03/30/2017
api_name:
- ICorDebugRegisterSet2.GetRegistersAvailable
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugRegisterSet2::GetRegistersAvailable
helpviewer_keywords:
- GetRegistersAvailable method, ICorDebugRegisterSet2 interface [.NET Framework debugging]
- ICorDebugRegisterSet2::GetRegistersAvailable method [.NET Framework debugging]
ms.assetid: f3ed344b-0d3a-44e8-8000-2a97e0805a2c
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5d4ab49aaccd77fac497bd86413915e82c99ed3e
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67744907"
---
# <a name="icordebugregisterset2getregistersavailable-method"></a>ICorDebugRegisterSet2::GetRegistersAvailable (Método)
Obtiene una matriz de bytes que proporciona un mapa de bits de los registros disponibles.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT GetRegistersAvailable (  
    [in] ULONG32 numChunks,  
    [out, size_is(numChunks)] BYTE availableRegChunks[]  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `numChunks`  
 [in] Tamaño de la matriz `availableRegChunks`.  
  
 `availableRegChunks`  
 [out] Una matriz de bytes, cada bit de los cuales corresponde a un registro. Si un registro está disponible, se establece el bit correspondiente del registro.  
  
## <a name="remarks"></a>Comentarios  
 Los valores de la enumeración CorDebugRegister especifican los registros de microprocesadores diferentes. Los cinco bits superiores de cada valor son el índice en el `availableRegChunks` matriz de bytes. Los tres bits inferiores de cada valor identifica la posición de bit dentro del byte indizado. Dado un `CorDebugRegister` valor que especifica un registro determinado, la posición del registro de la máscara se determina como sigue:  
  
1. Extraiga el índice necesario para tener acceso al byte correcto en el `availableRegChunks` matriz:  
  
     `CorDebugRegister` valor >> 3  
  
2. Extraiga la posición de bit dentro del byte indizado, donde bits cero es el bit menos significativo:  
  
     `CorDebugRegister` valor & 7  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [ICorDebugRegisterSet2 (interfaz)](../../../../docs/framework/unmanaged-api/debugging/icordebugregisterset2-interface.md)
- [ICorDebugRegisterSet (interfaz)](../../../../docs/framework/unmanaged-api/debugging/icordebugregisterset-interface.md)
