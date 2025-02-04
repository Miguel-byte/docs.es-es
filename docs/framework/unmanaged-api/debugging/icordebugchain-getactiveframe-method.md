---
title: ICorDebugChain::GetActiveFrame (Método)
ms.date: 03/30/2017
api_name:
- ICorDebugChain.GetActiveFrame
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugChain::GetActiveFrame
helpviewer_keywords:
- ICorDebugChain::GetActiveFrame method [.NET Framework debugging]
- GetActiveFrame method, ICorDebugChain interface [.NET Framework debugging]
ms.assetid: 36887017-670b-4f21-b406-8fab956f84a3
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c79f3b3b976b83eb99f8aa26d38a1fe316de471a
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67744997"
---
# <a name="icordebugchaingetactiveframe-method"></a>ICorDebugChain::GetActiveFrame (Método)
Obtiene el activo (es decir, más reciente) marco en la cadena.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT GetActiveFrame (  
    [out] ICorDebugFrame   **ppFrame  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `ppFrame`  
 [out] Un puntero a la dirección de un objeto ICorDebugFrame que representa el activo (es decir, más reciente) marco en la cadena.  
  
## <a name="remarks"></a>Comentarios  
 Si está disponible, ningún marco de pila administrado `ppFrame` se establece en null.  
  
 Si el marco activo no está disponible, la llamada se realizará correctamente y `ppFrame` será null. Marcos activa no estará disponibles para las cadenas iniciadas debido a CHAIN_ENTER_UNMANAGED y para algunas cadenas iniciadas debido a CHAIN_CLASS_INIT. Consulte CorDebugChainReason (enumeración).  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
