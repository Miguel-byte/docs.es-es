---
title: COR_PRF_HIGH_MONITOR (Enumeración)
ms.date: 04/10/2018
ms.assetid: 3ba543d8-15e5-4322-b6e7-1ebfc92ed7dd
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8cbc66ef1eb5048d2c708a615a99ea363d29540f
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67752177"
---
# <a name="corprfhighmonitor-enumeration"></a>COR_PRF_HIGH_MONITOR (Enumeración)
[Compatible con .NET Framework 4.5.2 y versiones posteriores]  
  
 Proporciona marcas, además de los que se encuentran en el [COR_PRF_MONITOR](../../../../docs/framework/unmanaged-api/profiling/cor-prf-monitor-enumeration.md) enumeración que el generador de perfiles puede especificar para el [icorprofilerinfo5:: Seteventmask2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo5-seteventmask2-method.md) método cuando se está cargando.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp
typedef enum {  
    COR_PRF_HIGH_MONITOR_NONE                     = 0x00000000,  
    COR_PRF_HIGH_ADD_ASSEMBLY_REFERENCES          = 0x00000001,  
    COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED        = 0x00000002,
    COR_PRF_HIGH_MONITOR_DYNAMIC_FUNCTION_UNLOADS = 0x00000004,
    COR_PRF_HIGH_DISABLE_TIERED_COMPILATION       = 0x00000008,
    COR_PRF_HIGH_BASIC_GC                         = 0x00000010,
    COR_PRF_HIGH_MONITOR_GC_MOVED_OBJECTS         = 0x00000020,
    COR_PRF_HIGH_MONITOR_LARGEOBJECT_ALLOCATED    = 0x00000040,
    COR_PRF_HIGH_REQUIRE_PROFILE_IMAGE            = 0,  
    COR_PRF_HIGH_ALLOWABLE_AFTER_ATTACH           = COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED | 
                                                    COR_PRF_HIGH_MONITOR_DYNAMIC_FUNCTION_UNLOADS |
                                                    COR_PRF_HIGH_BASIC_GC |
                                                    COR_PRF_HIGH_MONITOR_GC_MOVED_OBJECTS |
                                                    COR_PRF_HIGH_MONITOR_LARGEOBJECT_ALLOCATED,  
    COR_PRF_HIGH_MONITOR_IMMUTABLE                = COR_PRF_HIGH_DISABLE_TIERED_COMPILATION  
} COR_PRF_HIGH_MONITOR;  
```  
  
## <a name="members"></a>Miembros  
  
|Member|DESCRIPCIÓN|  
|------------|-----------------|  
|`COR_PRF_HIGH_MONITOR_NONE`|No se establecen marcas.|  
|`COR_PRF_HIGH_ADD_ASSEMBLY_REFERENCES`|Los controles de la [icorprofilercallback6:: Getassemblyreference](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback6-getassemblyreferences-method.md) devolución de llamada para agregar referencias de ensamblado durante el rastreo de cierre de referencias de ensamblado CLR.|  
|`COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED`|Los controles de la [ICorProfilerCallback7::ModuleInMemorySymbolsUpdated](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback7-moduleinmemorysymbolsupdated-method.md) devolución de llamada para las actualizaciones de la secuencia de símbolos asociada a un módulo en memoria.|  
|`COR_PRF_HIGH_MONITOR_DYNAMIC_FUNCTION_UNLOADS`|Los controles de la [ICorProfilerCallback9::DynamicMethodUnloaded](icorprofilercallback9-dynamicmethodunloaded-method.md) devolución de llamada para indicar cuando un método dinámico ha sido elementos no utilizados se recopilan y se descargan. <br/> [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]|
|`COR_PRF_HIGH_DISABLE_TIERED_COMPILATION`|.NET core 3.0 y versiones posteriores: Deshabilita [en capas compilación](../../../core/whats-new/dotnet-core-3-0.md) para los generadores de perfiles.|
|`COR_PRF_HIGH_BASIC_GC`|.NET core 3.0 y versiones posteriores: Proporciona una ligera en comparación con opción de generación de perfiles de GC [ `COR_PRF_MONITOR_GC` ](cor-prf-monitor-enumeration.md). Solo controla la [GarbageCollectionStarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-garbagecollectionstarted-method.md), [GarbageCollectionFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-garbagecollectionfinished-method.md), y [GetGenerationBounds](icorprofilerinfo2-getgenerationbounds-method.md) devoluciones de llamada. A diferencia de la `COR_PRF_MONITOR_GC` marca, `COR_PRF_HIGH_BASIC_GC` no deshabilitar la recolección de elementos no utilizados simultánea.|
|`COR_PRF_HIGH_MONITOR_GC_MOVED_OBJECTS`|.NET core 3.0 y versiones posteriores: Habilita la [MovedReferences](icorprofilercallback-movedreferences-method.md) y [MovedReferences2](icorprofilercallback4-movedreferences2-method.md) devoluciones de llamada para solo GC con compactación.|
|`COR_PRF_HIGH_MONITOR_LARGEOBJECT_ALLOCATED`|.NET core 3.0 y versiones posteriores: Similar a [ `COR_PRF_MONITOR_OBJECT_ALLOCATED` ](cor-prf-monitor-enumeration.md), pero se proporciona información sobre las asignaciones de objetos para el gran montón de objetos (LOH) solo.|
|`COR_PRF_HIGH_REQUIRE_PROFILE_IMAGE`|Representa todas las marcas `COR_PRF_HIGH_MONITOR` que requieren imágenes mejoradas para el perfil. Se corresponde con el `COR_PRF_REQUIRE_PROFILE_IMAGE` marca en el [COR_PRF_MONITOR](../../../../docs/framework/unmanaged-api/profiling/cor-prf-monitor-enumeration.md) enumeración.|  
|`COR_PRF_HIGH_ALLOWABLE_AFTER_ATTACH`|Representa todas las marcas `COR_PRF_HIGH_MONITOR` que se pueden establecer después de que el generador de perfiles se asocie a una aplicación en ejecución.|  
|`COR_PRF_HIGH_MONITOR_IMMUTABLE`|Representa todas las marcas `COR_PRF_HIGH_MONITOR` que se pueden establecer solo durante la inicialización. Al intentar cambiar cualquiera de estas marcas en otro lugar se genera un valor `HRESULT` que indica error.|  
  
## <a name="remarks"></a>Comentarios  
 El `COR_PRF_HIGH_MONITOR` marcas se usan con el `pdwEventsHigh` parámetro de la [icorprofilerinfo5:: Geteventmask2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo5-geteventmask2-method.md) y [icorprofilerinfo5:: Seteventmask2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo5-seteventmask2-method.md) métodos.  
  
A partir de .NET Framework 4.6.1, el valor de la `COR_PRF_HIGH_ALLOWABLE_AFTER_ATTACH` cambia de 0 a `COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED` (0 x 00000002). A partir de .NET Framework 4.7.2, puede cambiar su valor desde `COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED` a `COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED | COR_PRF_HIGH_MONITOR_DYNAMIC_FUNCTION_UNLOADS`.   

`COR_PRF_HIGH_MONITOR_IMMUTABLE` debe ser una máscara de bits que representa todos los marcadores que solo pueden establecerse durante la inicialización. Al intentar cambiar cualquiera de estas marcas en otro lugar da como resultado un error `HRESULT`.

## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: CorProf.idl, CorProf.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Enumeraciones para generación de perfiles](../../../../docs/framework/unmanaged-api/profiling/profiling-enumerations.md)
- [COR_PRF_MONITOR (enumeración)](../../../../docs/framework/unmanaged-api/profiling/cor-prf-monitor-enumeration.md)
- [ICorProfilerInfo5 (interfaz)](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo5-interface.md)
