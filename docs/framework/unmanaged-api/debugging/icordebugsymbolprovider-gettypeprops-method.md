---
title: 'ICorDebugSymbolProvider:: Gettypeprops ((método)'
ms.date: 03/30/2017
ms.assetid: 35ac4140-91ea-4c77-b1c4-1daf41986ca5
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8c8ea3a201cc94ef7bdf679371ef43ab2641b791
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69955550"
---
# <a name="icordebugsymbolprovidergettypeprops-method"></a>ICorDebugSymbolProvider:: Gettypeprops ((método)
Devuelve información acerca de las propiedades de un tipo, como el número de firmas de sus parámetros genéricos, dada una dirección virtual relativa (RVA) en una tabla virtual.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT GetTypeProps(  
   [in]  ULONG32 vtableRva,  
   [in]  ULONG32 cbSignature,  
   [out] ULONG32 *pcbSignature,  
   [out, size_is(cbSignature), length_is(*pcbSignature)] BYTE signature[]  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `tableRva`  
 [in] Dirección virtual relativa (RVA) en una tabla virtual.  
  
 `cbSignature`  
 [in] Tamaño de la matriz `signature`. Vea la sección Comentarios.  
  
 `pcbSignature`  
 [out] [out] Puntero al tamaño de la matriz `signature` devuelta.  
  
 `signature`  
 [out] Búfer que contiene las firmas de Typespec de todos los parámetros genéricos.  
  
## <a name="remarks"></a>Comentarios  
 Para obtener el tamaño necesario de la matriz del `signature` tipo, establezca el `cbSignature` argumento en 0 y `signature` en **null**. Con la devolución del método, `pcbSignature` contendrá el número de bytes necesarios para la matriz `signature`.  
  
> [!NOTE]
> Este método solo está disponible con .NET Native.  
  
## <a name="requirements"></a>Requisitos  
 **Select** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: Cordebug. idl, Cordebug. h  
  
 **Biblioteca** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Vea también

- [GetMethodProps (método)](../../../../docs/framework/unmanaged-api/debugging/icordebugsymbolprovider-getmethodprops-method.md)
- [ICorDebugSymbolProvider (interfaz)](../../../../docs/framework/unmanaged-api/debugging/icordebugsymbolprovider-interface.md)
- [Interfaces de depuración](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
