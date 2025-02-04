---
title: ICLRRuntimeInfo::GetRuntimeDirectory (Método)
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.GetRuntimeDirectory
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::GetRuntimeDirectory
helpviewer_keywords:
- GetRuntimeDirectory method [.NET Framework hosting]
- ICLRRuntimeInfo::GetRuntimeDirectory method [.NET Framework hosting]
ms.assetid: 4401546e-4d48-453f-a1fb-b2ebda54df5c
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2455c896ebdc12f2bb92a30d55745f7bd5bc308a
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67765522"
---
# <a name="iclrruntimeinfogetruntimedirectory-method"></a>ICLRRuntimeInfo::GetRuntimeDirectory (Método)
Obtiene el directorio de instalación de common language runtime (CLR) asociado a esta interfaz.  
  
 Este método reemplaza el [GetCORSystemDirectory](../../../../docs/framework/unmanaged-api/hosting/getcorsystemdirectory-function.md) función incluida en las versiones de .NET Framework 2.0, 3.0 y 3.5.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT GetRuntimeDirectory(  
[out, size_is(*pcchBuffer)] LPWSTR pwzBuffer,  
[in, out]  DWORD *pcchBuffer);  
```  
  
## <a name="parameters"></a>Parámetros  
 `pwzBuffer`  
 [out] Devuelve el directorio de instalación de CLR. La ruta de instalación está completa; Por ejemplo, "c:\windows\microsoft.net\framework\v1.0.3705\\".  
  
 `pchBuffer`  
 [in, out] Especifica el tamaño de `pwzBuffer` para evitar saturaciones de búfer. Si `pwzBuffer` es null, `pchBuffer` devuelve el tamaño necesario de `pwzBuffer`.  
  
## <a name="return-value"></a>Valor devuelto  
 Este método devuelve los siguientes HRESULT específicos y los errores HRESULT que indican un error del método.  
  
|HRESULT|DESCRIPCIÓN|  
|-------------|-----------------|  
|S_OK|El método se completó correctamente.|  
|E_POINTER|`pwzBuffer` o `pchBuffer` es null.|  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: MetaHost.h  
  
 **Biblioteca:** Incluye como recurso en MSCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [ICLRRuntimeInfo (interfaz)](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md)
- [Hospedar aplicaciones de WPF](../../../../docs/framework/unmanaged-api/hosting/index.md)
