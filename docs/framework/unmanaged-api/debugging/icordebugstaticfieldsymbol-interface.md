---
title: Interfaz ICorDebugStaticFieldSymbol
ms.date: 03/30/2017
ms.assetid: c0b93609-631e-4b15-878a-189ede922631
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7f4e245e96ac9d47db10072e50a5b3c516d5dd27
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962677"
---
# <a name="icordebugstaticfieldsymbol-interface"></a>Interfaz ICorDebugStaticFieldSymbol
Representa la información de símbolos de depuración para un campo estático.  
  
## <a name="methods"></a>Métodos  
  
|Método|DESCRIPCIÓN|  
|------------|-----------------|  
|[GetAddress (método)](../../../../docs/framework/unmanaged-api/debugging/icordebugstaticfieldsymbol-getaddress-method.md)|Obtiene la dirección del campo estático.|  
|[GetName (método)](../../../../docs/framework/unmanaged-api/debugging/icordebugstaticfieldsymbol-getname-method.md)|Obtiene el nombre del campo estático.|  
|[GetSize (método)](../../../../docs/framework/unmanaged-api/debugging/icordebugstaticfieldsymbol-getsize-method.md)|Obtiene el tamaño del campo estático, en bytes.|  
  
## <a name="remarks"></a>Comentarios  
 La interfaz `ICorDebugStaticFieldSymbol` se utiliza para recuperar la información de símbolos de depuración para un campo estático.  
  
> [!NOTE]
> Esta interfaz solo está disponible con .NET Native. Si implementa esta interfaz para escenarios de ICorDebug fuera de .NET Native, Common Language Runtime ignorará esta interfaz.  
  
## <a name="requirements"></a>Requisitos  
 **Select** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: Cordebug. idl, Cordebug. h  
  
 **Biblioteca** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Vea también

- [ICorDebugInstanceFieldSymbol (interfaz)](../../../../docs/framework/unmanaged-api/debugging/icordebuginstancefieldsymbol-interface.md)
- [Interfaces de depuración](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [Depuración](../../../../docs/framework/unmanaged-api/debugging/index.md)
