---
title: FUSION_INSTALL_REFERENCE (Estructura)
ms.date: 03/30/2017
api_name:
- FUSION_INSTALL_REFERENCE
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- FUSION_INSTALL_REFERENCE
helpviewer_keywords:
- FUSION_INSTALL_REFERENCE structure [.NET Framework fusion]
ms.assetid: ae181ec8-36bf-4ed1-9a02-ca27d417c80b
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9e81fb7c99b9fd03a69456a84f2191770f40121d
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795347"
---
# <a name="fusion_install_reference-structure"></a>FUSION_INSTALL_REFERENCE (Estructura)
Representa una referencia que una aplicación realiza a un ensamblado que la aplicación ha instalado en la caché global de ensamblados.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
typedef struct _FUSION_INSTALL_REFERENCE_ {  
    DWORD    cbSize,  
    DWORD    dwFlags,  
    GUID     guidScheme,  
    LPCWSTR  szIdentifier,  
    LPCWSTR  szNonCanonicalData  
} FUSION_INSTALL_REFERENCE, *LPFUSION_INSTALL_REFERENCE;  
```  
  
## <a name="members"></a>Miembros  
  
|Member|DESCRIPCIÓN|  
|------------|-----------------|  
|`cbSize`|Tamaño de la estructura en bytes.|  
|`dwFlags`|Reservado para extensibilidad futura. Este valor debe ser 0 (cero).|  
|`guidScheme`|Entidad que agrega la referencia. Este campo puede tener uno de los valores siguientes:<br /><br /> - FUSION_REFCOUNT_MSI_GUID: Una aplicación que se instaló mediante el Microsoft Windows Installer hace referencia al ensamblado. El `szIdentifier` campo se establece en `MSI`y el `szNonCanonicalData` campo se establece en `Windows Installer`. Este esquema se utiliza para los ensamblados en paralelo de Windows.<br />-   FUSION_REFCOUNT_UNINSTALL_SUBKEY_GUID: Una aplicación que aparece en la interfaz **Agregar o quitar programas** hace referencia al ensamblado. El `szIdentifier` campo proporciona el token que registra la aplicación con la interfaz **Agregar o quitar programas** .<br />- FUSION_REFCOUNT_FILEPATH_GUID: Una aplicación que representa un archivo en el sistema de archivos hace referencia al ensamblado. El `szIdentifier` campo proporciona la ruta de acceso a este archivo.<br />- FUSION_REFCOUNT_OPAQUE_STRING_GUID: Una aplicación que representa solo una cadena opaca hace referencia al ensamblado. El `szIdentifier` campo proporciona esta cadena opaca. La caché global de ensamblados no comprueba la existencia de referencias opacas al quitar este valor.<br />- FUSION_REFCOUNT_OSINSTALL_GUID: Este valor está reservado.|  
|`szIdentifier`|Cadena única que identifica la aplicación que ha instalado el ensamblado en la caché global de ensamblados. Su valor depende del valor del `guidScheme` campo.|  
|`szNonCanonicalData`|Cadena que solo entiende la entidad que agrega la referencia. La caché global de ensamblados almacena esta cadena, pero no la utiliza.|  
  
## <a name="requirements"></a>Requisitos  
 **Select** Consulte [Requisitos del sistema](../../get-started/system-requirements.md).  
  
 **Encabezado**: Fusion. h  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Estructuras de fusión](fusion-structures.md)
- [Caché global de ensamblados](../../app-domains/gac.md)
