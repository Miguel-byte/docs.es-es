---
title: ICorDebugSymbolProvider::GetMethodProps (método)
ms.date: 03/30/2017
ms.assetid: 8f836b80-b7a5-460b-bf76-5f0e45652aea
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 95610bc527b8f5b90df906b6260eb636d61dbcd8
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69957302"
---
# <a name="icordebugsymbolprovidergetmethodprops-method"></a>ICorDebugSymbolProvider::GetMethodProps (método)
Devuelve información acerca de las propiedades del método, como el token de metadatos del método e información acerca de sus parámetros genéricos, a partir de una dirección virtual relativa (RVA) en ese método.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT GetMethodProps(  
   [in]  ULONG32 codeRva,  
   [out] mdToken *pMethodToken,  
   [out] ULONG32 *pcGenericParams,  
   [in]  ULONG32 cbSignature,  
   [out] ULONG32 *pcbSignature,  
   [out, size_is(cbSignature), length_is(*pcbSignature)] BYTE signature[]  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `codeRVA`  
 [in] Dirección virtual relativa del método acerca de qué información se va a recuperar.  
  
 `pMethodToken`  
 [out] Puntero al token de metadatos del método.  
  
 `pcGenericParams`  
 [out] Puntero al número de parámetros genéricos asociados a este método.  
  
 `cbSignature`  
 [in] Tamaño de la matriz `signature`. Vea la sección Comentarios.  
  
 `pcbSignature`  
 [out] Puntero al tamaño de la matriz `signature` devuelta.  
  
 `signature`  
 [out] Búfer que contiene las firmas de Typespec de todos los parámetros genéricos.  
  
## <a name="remarks"></a>Comentarios  
 Para obtener el tamaño necesario de la matriz del `signature` método, establezca el `cbSignature` argumento en 0 y `signature` en **null**. Con la devolución del método, `pcbSignature` contendrá el número de bytes necesarios para la matriz `signature`.  
  
> [!NOTE]
> Este método solo está disponible con .NET Native.  
  
## <a name="requirements"></a>Requisitos  
 **Select** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: Cordebug. idl, Cordebug. h  
  
 **Biblioteca** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Vea también

- [GetTypeProps (método)](../../../../docs/framework/unmanaged-api/debugging/icordebugsymbolprovider-gettypeprops-method.md)
- [ICorDebugSymbolProvider (interfaz)](../../../../docs/framework/unmanaged-api/debugging/icordebugsymbolprovider-interface.md)
- [Interfaces de depuración](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
