---
title: Estructura DacpReJitData
ms.date: 02/01/2019
api.name:
- DacpReJitData Structure
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- DacpReJitData Structure
helpviewer.keywords:
- DacpReJitData Structure [.NET Framework debugging]
topic_type:
- apiref
author: hoyosjs
ms.author: juhoyosa
ms.openlocfilehash: 77ef2c65157df4a033700bb8d0295875ede46554
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67739113"
---
# <a name="dacprejitdata-structure"></a>Estructura DacpReJitData

Define la información básica sobre un determinado método del generador de perfiles instrumentada.

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>Sintaxis

```cpp
struct MSLAYOUT DacpReJitData
{
    enum Flags
    {
        kUnknown,
        kRequested,
        kActive,
        kReverted,
    };

    CLRDATA_ADDRESS                 rejitID;
    Flags                           flags;
    CLRDATA_ADDRESS                 NativeCodeAddr;
};
```

## <a name="members"></a>Miembros

| Member           | DESCRIPCIÓN                                                                                      |
| ---------------- | ------------------------------------------------------------------------------------------------ |
| `rejitID`        | El número de revisión ReJit para un método.                                                          |
| `flags`          | Una marca que indica el estado actual de la instrumentación ReJit del método para la versión especificada. |
| `NativeCodeAddr` | La dirección base de la implementación del método rejitted.                                         |

## <a name="remarks"></a>Comentarios

Esta estructura reside en el tiempo de ejecución y no se expone a través de los encabezados o archivos de biblioteca. Para ello, defina la estructura según lo especificado anteriormente. La estructura también debe definirse mediante `ms_struct` empaquetado si no se usan los compiladores de Microsoft.

## <a name="requirements"></a>Requisitos
**Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
**Encabezado**: None  
**Biblioteca:** None  
**Versiones de .NET Framework:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>Vea también

- [Depuración](../../../../docs/framework/unmanaged-api/debugging/index.md)
- [Estructuras de depuración](../../../../docs/framework/unmanaged-api/debugging/debugging-structures.md)
