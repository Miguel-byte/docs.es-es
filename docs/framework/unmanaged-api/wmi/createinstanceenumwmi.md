---
title: Función CreateInstanceEnumWmi (referencia de la API no administrada)
description: La función CreateInstanceEnumWmi devuelve un enumerador que contiene las instancias de una clase especificada que cumplen los criterios de selección.
ms.date: 11/06/2017
api_name:
- CreateInstanceEnumWmi
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- CreateInstanceEnumWmi
helpviewer_keywords:
- CreateInstanceEnumWmi function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b7709d9c50a494013ece2f91b3acc213278f0e57
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798908"
---
# <a name="createinstanceenumwmi-function"></a>CreateInstanceEnumWmi función)

Devuelve un enumerador que devuelve las instancias de una clase especificada que cumpla los criterios de selección especificados.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>Sintaxis

```cpp
HRESULT CreateInstanceEnumWmi (
   [in] BSTR                    strFilter,
   [in] long                    lFlags,
   [in] IWbemContext*           pCtx,
   [out] IEnumWbemClassObject** ppEnum,
   [in] DWORD                   authLevel,
   [in] DWORD                   impLevel,
   [in] IWbemServices*          pCurrentNamespace,
   [in] BSTR                    strUser,
   [in] BSTR                    strPassword,
   [in] BSTR                    strAuthority
);
```

## <a name="parameters"></a>Parámetros

`strFilter`\
de Nombre de la clase para la que se desean instancias. Este parámetro no puede `null`ser.

`lFlags`\
de Combinación de marcas que afectan al comportamiento de esta función. Los siguientes valores se definen en el archivo de encabezado *WbemCli. h* , o bien se pueden definir como constantes en el código:

|Constante  |Valor  |DESCRIPCIÓN  |
|---------|---------|---------|
| `WBEM_FLAG_USE_AMENDED_QUALIFIERS` | 0x20000 | Si se establece, la función recupera los calificadores modificados almacenados en el espacio de nombres localizado de la configuración regional de la conexión actual. <br/> Si no se establece, la función solo recupera los calificadores almacenados en el espacio de nombres inmediato. |
| `WBEM_FLAG_DEEP` | 0 | La enumeración incluye esta y todas las subclases de la jerarquía. |
| `WBEM_FLAG_SHALLOW` | 1 | La enumeración solo incluye instancias puras de esta clase y excluye todas las instancias de subclases que suministran propiedades que no se encuentran en esta clase. |
| `WBEM_FLAG_RETURN_IMMEDIATELY` | 0x10 | La marca produce una llamada semisincrónica. |
| `WBEM_FLAG_FORWARD_ONLY` | 0x20 | La función devuelve un enumerador de solo avance. Normalmente, los enumeradores de solo avance son más rápidos y usan menos memoria que los enumeradores convencionales, pero no permiten que las llamadas se [clonen](clone.md). |
| `WBEM_FLAG_BIDIRECTIONAL` | 0 | WMI conserva los punteros a objetos en la enumeración hasta que se liberan. |

Las marcas recomendadas `WBEM_FLAG_RETURN_IMMEDIATELY` son `WBEM_FLAG_FORWARD_ONLY` y para obtener el mejor rendimiento.

`pCtx`\
de Normalmente, este valor es `null`. De lo contrario, es un puntero a una instancia de [IWbemContext](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemcontext) que puede ser utilizada por el proveedor que proporciona las instancias solicitadas.

`ppEnum`\
enuncia Recibe el puntero al enumerador.

`authLevel`\
de Nivel de autorización.

`impLevel`\
de Nivel de suplantación.

`pCurrentNamespace`\
de Un puntero a un objeto [IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices) que representa el espacio de nombres actual.

`strUser`\
de El nombre de usuario. Vea la función [ConnectServerWmi](connectserverwmi.md) para obtener más información.

`strPassword`\
de La contraseña. Vea la función [ConnectServerWmi](connectserverwmi.md) para obtener más información.

`strAuthority`\
de El nombre de dominio del usuario. Vea la función [ConnectServerWmi](connectserverwmi.md) para obtener más información.

## <a name="return-value"></a>Valor devuelto

Los siguientes valores devueltos por esta función se definen en el archivo de encabezado *WbemCli. h* , o bien se pueden definir como constantes en el código:

|Constante  |Valor  |DESCRIPCIÓN  |
|---------|---------|---------|
| `WBEM_E_ACCESS_DENIED` | 0x80041003 | El usuario no tiene permiso para ver las instancias de la clase especificada. |
| `WBEM_E_FAILED` | 0x80041001 | Se ha producido un error no especificado. |
| `WBEM_E_INVALID_CLASS` | 0x80041010 | `strFilter` no existe. |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | Un parámetro no es válido. |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | No hay suficiente memoria disponible para completar la operación. |
| `WBEM_E_SHUTTING_DOWN` | 0x80041033 | Es posible que WMI se haya detenido y reiniciado. Vuelva a llamar a [ConnectServerWmi](connectserverwmi.md) . |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | Error en el vínculo de llamada a procedimiento remoto (RPC) entre el proceso actual y WMI. |
|`WBEM_S_NO_ERROR` | 0 | La llamada de función se realizó correctamente.  |

## <a name="remarks"></a>Comentarios

Esta función contiene una llamada al método [IWbemServices:: CreateClassEnum](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemservices-createinstanceenum) .

Tenga en cuenta que el enumerador devuelto puede tener cero elementos.

Si se produce un error en la llamada de función, puede obtener información de error adicional mediante una llamada a la función [GetErrorInfo](geterrorinfo.md) .

## <a name="requirements"></a>Requisitos

**Select** Consulte [Requisitos del sistema](../../get-started/system-requirements.md).

**Encabezado**: WMINet_Utils.idl

**Versiones de .NET Framework:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>Vea también

- [WMI y contadores de rendimiento (referencia de la API no administrada)](index.md)
