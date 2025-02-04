---
title: GetVersionFromProcess (Función)
ms.date: 03/30/2017
api_name:
- GetVersionFromProcess
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- GetVersionFromProcess
helpviewer_keywords:
- GetVersionFromProcess function [.NET Framework hosting]
ms.assetid: a9f7f824-64a1-408d-8607-91c7f19d21fe
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4015ecec38466650488a653641f5af93c4680f22
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67779593"
---
# <a name="getversionfromprocess-function"></a>GetVersionFromProcess (Función)
Obtiene el número de versión de common language runtime (CLR) que está asociado con el identificador de proceso especificado.  
  
 Esta función está desusada en .NET Framework 4.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT GetVersionFromProcess (  
    [in]  HANDLE  hProcess,   
    [out] LPWSTR  pVersion,   
    [in]  DWORD   cchBuffer,   
    [out] DWORD  *dwLength  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 `hProcess`  
 [in] Un identificador de proceso.  
  
 `pVersion`  
 [out] Un búfer que contiene la cadena de número de versión tras la finalización correcta del método.  
  
 `cchBuffer`  
 [in] La longitud del búfer de versión.  
  
 `pdwLength`  
 [out] Un puntero a la longitud de la cadena de número de versión.  
  
## <a name="return-value"></a>Valor devuelto  
 Este método devuelve códigos de error de modelo de objetos componentes (COM) estándar, tal como se define en WinError.h, además de los valores siguientes.  
  
|Código devuelto|DESCRIPCIÓN|  
|-----------------|-----------------|  
|S_OK|El método se completó correctamente.|  
|E_INVALIDARG|`pVersion` es null y `cchBuffer` no es null, o viceversa.<br /><br /> -o bien-<br /><br /> `hProcess` no es un identificador válido para un proceso.<br /><br /> -o bien-<br /><br /> No se carga el CLR.|  
|ERROR_INSUFFICIENT_BUFFER|`cchBuffer` es nulo o menor que la longitud de la cadena de versión.|  
|E_NOTIMPL|Este método no está disponible en el sistema operativo Microsoft Windows 95, Microsoft Windows 98 o Windows Millennium Edition de Microsoft.|  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: MSCorEE.h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [GetRequestedRuntimeInfo (Función)](../../../../docs/framework/unmanaged-api/hosting/getrequestedruntimeinfo-function.md)
- [GetRequestedRuntimeVersion (Función)](../../../../docs/framework/unmanaged-api/hosting/getrequestedruntimeversion-function.md)
- [Funciones de hospedaje de CLR en desuso](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
