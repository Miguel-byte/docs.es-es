---
title: Interfaz ICorDebugVariableSymbol
ms.date: 03/30/2017
ms.assetid: 0e58b85e-69bd-41ff-bedb-8cdc8be6a7a2
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3fb2538894184c19bc107ce52cbef3ac86a97345
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69967977"
---
# <a name="icordebugvariablesymbol-interface"></a>Interfaz ICorDebugVariableSymbol
Recupera la información de símbolos de depuración para una variable.  
  
## <a name="methods"></a>Métodos  
  
|Método|DESCRIPCIÓN|  
|------------|-----------------|  
|[GetName (método)](../../../../docs/framework/unmanaged-api/debugging/icordebugvariablesymbol-getname-method.md)|Obtiene el nombre de una variable.|  
|[GetSize (método)](../../../../docs/framework/unmanaged-api/debugging/icordebugvariablesymbol-getsize-method.md)|Obtiene el tamaño de una variable en bytes.|  
|[GetSlotIndex (método)](../../../../docs/framework/unmanaged-api/debugging/icordebugvariablesymbol-getslotindex-method.md)|Obtiene el índice de ranura administrado de una variable local.|  
|[GetValue (método)](../../../../docs/framework/unmanaged-api/debugging/icordebugvariablesymbol-getvalue-method.md)|Obtiene el valor de una variable como una matriz de bytes.|  
|[SetValue (método)](../../../../docs/framework/unmanaged-api/debugging/icordebugvariablesymbol-setvalue-method.md)|Asigna el valor de una matriz de bytes a una variable.|  
  
## <a name="remarks"></a>Comentarios  
  
> [!NOTE]
> Esta interfaz solo está disponible con .NET Native. Si implementa esta interfaz para escenarios de ICorDebug fuera de .NET Native, Common Language Runtime ignorará esta interfaz.  
  
## <a name="requirements"></a>Requisitos  
 **Select** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: Cordebug. idl, Cordebug. h  
  
 **Biblioteca** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Interfaces de depuración](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [Depuración](../../../../docs/framework/unmanaged-api/debugging/index.md)
