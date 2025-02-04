---
title: IMetaDataEmit::SetHandler (Método)
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetHandler
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetHandler
helpviewer_keywords:
- IMetaDataEmit::SetHandler method [.NET Framework metadata]
- SetHandler method [.NET Framework metadata]
ms.assetid: c6c1aaaf-e2cd-407c-b73e-fbe6ffd83bb3
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d50198cc6156d5bec8b8302a4624b0b7411a9c2d
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67751093"
---
# <a name="imetadataemitsethandler-method"></a>IMetaDataEmit::SetHandler (Método)
Establece el método al que hace referencia especificado `IUnknown` puntero como una devolución de llamada de notificación para las reasignaciones de token.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT SetHandler (   
    [in]  IUnknown    *pUnk  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `pUnk`  
 [in] Para registrar el controlador.  
  
## <a name="remarks"></a>Comentarios  
 El motor de metadatos envía la notificación mediante el método proporcionado por `SetHandler`, a los compiladores que no generan registros de forma optimizada y que le gustaría optimizar registros guardados.  
  
 Si el método de devolución de llamada no se proporciona a través de `SetHandler`, no se realizará ninguna optimización en Guardar, excepto donde importación varios ámbitos se han combinado mediante `IMapToken` en cada ámbito de replicación de mezcla.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: Cor.h  
  
 **Biblioteca:** Usar como un recurso en MSCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [IMetaDataEmit (interfaz)](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataEmit2 (interfaz)](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
