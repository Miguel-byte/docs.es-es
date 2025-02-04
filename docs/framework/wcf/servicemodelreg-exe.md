---
title: Herramienta de registro de ServiceModel (ServiceModelReg.exe)
ms.date: 03/30/2017
ms.assetid: 396ec5ae-e34f-4c64-a164-fcf50e86b6ac
ms.openlocfilehash: 519f303507ed873266cc05a7556073887b66ba6f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69923029"
---
# <a name="servicemodel-registration-tool-servicemodelregexe"></a>Herramienta de registro de ServiceModel (ServiceModelReg.exe)
Esta herramienta de la línea de comandos proporciona la capacidad de administrar el registro de componentes de WCF y de WF en un único equipo. En circunstancias normales no debería ser necesario usar esta herramienta mientras se configuran e instalan los componentes de WCF y de WF. Pero si experimenta problemas con la activación del servicio, puede intentar registrar los componentes mediante esta herramienta.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
ServiceModelReg.exe[(-ia|-ua|-r)|((-i|-u) -c:<command>)] [-v|-q] [-nologo] [-?]  
```  
  
## <a name="remarks"></a>Comentarios  
 La herramienta se puede encontrar en la ubicación siguiente:  
  
 %SystemRoot%\Microsoft.Net\Framework\v3.0\Windows Communication Foundation\  
  
> [!NOTE]
> Cuando se ejecuta la herramienta de registro de [!INCLUDE[wv](../../../includes/wv-md.md)]ServiceModel, es posible que el cuadro de diálogo **características de Windows** no refleje que está activada la opción de **activación http Windows Communication Foundation** en **Microsoft .NET Framework 3,0** . Para obtener acceso al cuadro de diálogo **características de Windows** , haga clic en **Inicio**, luego en **Ejecutar** y, a continuación, escriba **OptionalFeatures**.  
  
 Las tablas siguientes describen las opciones que se pueden utilizar con ServiceModelReg.exe.  
  
|Opción|DESCRIPCIÓN|  
|------------|-----------------|  
|`-ia`|Instala todos los componentes de WCF y de WF.|  
|`-ua`|Desinstala todos los componentes de WCF y de WF.|  
|`-r`|Repara todos los componentes de WCF y de WF.|  
|`-i`|Instala los componentes de WCF y de WF especificados con –c.|  
|`-u`|Desinstala los componentes de WCF y de WF especificados con –c.|  
|`-c`|Instala o desinstala un componente:<br /><br /> -httpnamespace: Reserva de espacio de nombres HTTP<br />-tcpportsharing: servicio de uso compartido de puertos TCP<br />-tcpactivation: servicio de activación TCP (no compatible con .NET 4 Client Profile)<br />-namedpipeactivation: servicio de activación de canalizaciones con nombre (no compatible con .NET 4 Client Profile<br />-msmqactivation: servicio de activación de MSMQ (no compatible con .NET 4 Client Profile<br />-ETW: manifiestos de seguimiento de eventos ETW (Windows Vista o posterior)|  
|`-q`|Modo silencioso (solo se muestra el registro de errores)|  
|`-v`|Modo detallado.|  
|`-nologo`|Suprime el mensaje del banner y el copyright.|  
|`-?`|Muestra texto de ayuda.|  
  
## <a name="fixing-the-fileloadexception-error"></a>Corregir el error FileLoadException  
 Si instaló versiones anteriores de WCF en el equipo, es posible que reciba un `FileLoadFoundException` error al ejecutar la herramienta ServiceModelReg para registrar una nueva instalación. Esto puede pasar aun cuando ha quitado manualmente los archivos de la instalación anterior, pero ha dejado intactos los valores machine.config.  
  
 El mensaje de error es similar al siguiente.  
  
```  
Error: System.IO.FileLoadException: Could not load file or assembly 'System.ServiceModel, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089' or one of its dependencies. The located assembly's manifest definition does not match the assembly reference. (Exception from HRESULT: 0x80131040)  
File name: 'System.ServiceModel, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089'  
```  
  
 Debería observar en el mensaje de error que el ensamblado de la versión 2.0.0.0 de System.ServiceModel fue instalado por un lanzamiento anterior de Customer Technology Preview (CTP). La versión actual del ensamblado System.ServiceModel que se ha lanzado es 3.0.0.0. Por lo tanto, este problema se produce cuando se desea instalar la versión oficial de WCF en un equipo en el que se ha instalado una versión de CTP temprana, pero no se ha desinstalado por completo.  
  
 ServiceModelReg.exe no puede limpiar las entradas de versión anteriores, ni puede registrar las entradas de la nueva versión. La única solución alternativa es modificar manualmente machine.config. Encontrará este archivo en la ubicación siguiente.  
  
```  
%windir%\Microsoft.NET\Framework\v2.0.50727\config\machine.config   
```  
  
 Si está ejecutando WCF en un equipo de 64 bits, también debe editar el mismo archivo en esta ubicación.  
  
```  
%windir%\Microsoft.NET\Framework64\v2.0.50727\config\machine.config   
```  
  
 Busque los nodos XML de este archivo que hagan referencia a "System. ServiceModel, version = 2.0.0.0", elimínelos y los nodos secundarios. Guarde el archivo y el problema se resolverá volviendo a ejecutar ServiceModelReg.exe.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes muestran cómo usar las opciones más comunes de la herramienta ServiceModelReg.exe.  
  
```  
ServiceModelReg.exe -ia  
  Installs all components  
ServiceModelReg.exe -i -c:httpnamespace -c:etw  
  Installs HTTP namespace reservation and ETW manifests  
ServiceModelReg.exe -u -c:etw  
  Uninstalls ETW manifests  
ServiceModelReg.exe -r  
  Repairs an extended install  
```
