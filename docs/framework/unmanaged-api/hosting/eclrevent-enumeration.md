---
title: EClrEvent (Enumeración)
ms.date: 03/30/2017
api_name:
- EClrEvent
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EClrEvent
helpviewer_keywords:
- EClrEvent enumeration [.NET Framework hosting]
ms.assetid: 7c36a7c2-75a2-4971-bc23-abf54c812154
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f1e003ba23f680c4a5525a956d758aac6b823eb9
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67769710"
---
# <a name="eclrevent-enumeration"></a>EClrEvent (Enumeración)
Describe los eventos de common language runtime (CLR) para que el host puede registrar devoluciones de llamada.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
typedef enum {  
    Event_ClrDisabled,  
    Event_DomainUnload,  
    Event_MDAFired,  
    Event_StackOverflow  
} EClrEvent;  
```  
  
## <a name="members"></a>Miembros  
  
|Member|DESCRIPCIÓN|  
|------------|-----------------|  
|`Event_ClrDisabled`|Especifica un error grave de CLR.|  
|`Event_DomainUnload`|Especifica la descarga de un determinado <xref:System.AppDomain>.|  
|`Event_MDAFired`|Especifica que se ha generado un mensaje del Asistente para la depuración administrada (MDA).|  
|`Event_StackOverflow`|Especifica que se ha producido un error de desbordamiento de pila.|  
  
## <a name="remarks"></a>Comentarios  
 El host puede registrar devoluciones de llamada para cualquiera de los tipos de eventos descritos por `EClrEvent` llamando a métodos de la [ICLROnEventManager](../../../../docs/framework/unmanaged-api/hosting/iclroneventmanager-interface.md) interfaz. El host obtiene un puntero a esta interfaz mediante una llamada a la [ICLRControl:: GetCLRManager](../../../../docs/framework/unmanaged-api/hosting/iclrcontrol-getclrmanager-method.md) método.  
  
 El `Event_CLRDisabled` y `Event_DomainUnload` se pueden generar eventos más de una vez y desde diferentes subprocesos para indicar una descarga o la deshabilitación de CLR.  
  
 El `Event_MDAFired` evento provoca la creación de un [MDAInfo](../../../../docs/framework/unmanaged-api/hosting/mdainfo-structure.md) instancia que contiene los detalles del mensaje MDA. Para obtener más información sobre los MDA, consulte [Diagnosing Errors with Managed Debugging Assistants](../../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md).  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Consulte [Requisitos del sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Encabezado**: MSCorEE.h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **Versiones de .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vea también

- [IActionOnCLREvent (interfaz)](../../../../docs/framework/unmanaged-api/hosting/iactiononclrevent-interface.md)
- [ICLRControl (interfaz)](../../../../docs/framework/unmanaged-api/hosting/iclrcontrol-interface.md)
- [Enumeraciones para hosts](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
