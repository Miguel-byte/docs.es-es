---
title: GetCORSystemDirectory (Función)
ms.date: 03/30/2017
api_name:
- GetCORSystemDirectory
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- GetCORSystemDirectory
helpviewer_keywords:
- GetCORSystemDirectory function [.NET Framework hosting]
ms.assetid: 3dcd16a7-dafc-4ca8-b5cd-20ffb37db91d
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d30384ea8b9ff4eee41abd43ae39486f770039e7
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2019
ms.locfileid: "70041424"
---
# <a name="getcorsystemdirectory-function"></a>GetCORSystemDirectory (Función)
Devuelve el directorio de instalación del Common Language Runtime (CLR) que se carga en el proceso. El directorio de instalación es completo, por ejemplo, "c:\Windows\Microsoft.NET\Framework\v1.0.3705".  
  
 Esta función está en desuso. Se sustituye por el método [ICLRRuntimeInfo:: GetRuntimeDirectory (](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-getruntimedirectory-method.md) proporcionado en el .NET Framework 4.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
HRESULT GetCORSystemDirectory (   
    [out] LPWSTR  pbuffer,     
    [in]  DWORD   cchBuffer,   
    [out] DWORD*  dwlength  
);   
```  
  
## <a name="parameters"></a>Parámetros  
 `pbuffer`  
 enuncia Búfer en el que el tiempo de ejecución devuelve una cadena que contiene el nombre completo del directorio de instalación para el tiempo de ejecución que se carga en el proceso. Si el tiempo de ejecución aún no se ha cargado en el proceso, la función devuelve la información de directorio adecuada para la versión más reciente del motor en tiempo de ejecución instalada en el equipo.  
  
 `cchBuffer`  
 de Tamaño, en bytes, de `pbuffer`.  
  
 `dwLength`  
 enuncia Número de caracteres devueltos `pbuffer`en.  
  
## <a name="remarks"></a>Comentarios  
  
> [!CAUTION]
> No utilice esta función en los procesos que ejecutan la versión 4 de CLR. Si hay instalada una versión anterior de CLR en el equipo, esta función devuelve el directorio de instalación de esa versión.  
  
## <a name="requirements"></a>Requisitos  
 **Select** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: MSCorEE.h  
  
 **Biblioteca** MSCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Funciones de hospedaje de CLR en desuso](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
