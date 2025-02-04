---
title: Esquema de la configuración de red
ms.date: 03/30/2017
helpviewer_keywords:
- elements [.NET Framework], network configuration elements
- sending data, network configuration elements
- receiving data, network configuration elements
- configuration settings [.NET Framework], networks
- Internet, network configuration elements
- network configuration elements
- network settings
- connections [.NET Framework], network configuration elements
- network resources, network configuration elements
ms.assetid: f1de5a0f-76c5-4833-819f-5222b8146340
ms.openlocfilehash: 5e3bd1b1734fc7fba50b72785531a8b001d6d741
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2019
ms.locfileid: "71698153"
---
# <a name="network-settings-schema"></a>Esquema de la configuración de red
La configuración de red especifica cómo se conecta .NET Framework a Internet.

La configuración @no__t -0SYSTEM. net > especifica cómo se conecta el .NET Framework a la red. En la tabla siguiente se describe la función de cada elemento de configuración secundario bajo el [elemento \<system.Net> (configuración de red)](system-net-element-network-settings.md).  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[Elemento \<authenticationModules> (configuración de red)](authenticationmodules-element-network-settings.md)|Especifica los módulos usados para autenticar solicitudes de Internet.|  
|[Elemento \<connectionManagement> (configuración de red)](connectionmanagement-element-network-settings.md)|Especifica el número máximo de conexiones a hosts de Internet.|  
|[Elemento \<defaultProxy> (configuración de red)](defaultproxy-element-network-settings.md)|Especifica el servidor proxy usado para las solicitudes HTTP a Internet.|  
|[Elemento \<mailSettings> (configuración de red)](mailsettings-element-network-settings.md)|Contiene la configuración de opciones de envío de correo.|  
|[Elemento \<requestCaching> (configuración de red)](requestcaching-element-network-settings.md)|Controla el mecanismo de almacenamiento en caché para las solicitudes de red.|  
|[Elemento \<webRequestModules> (configuración de red)](webrequestmodules-element-network-settings.md)|Especifica los módulos usados para solicitar información de hosts de Internet.|  
  
La configuración de > de \<uri especifica cómo el .NET Framework controla las direcciones web expresadas mediante identificadores uniformes de recursos (URI). En la tabla siguiente se describe la función de cada elemento de configuración secundario en el [elemento de > \<uri (configuración de URI)](uri-element-uri-settings.md).  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[Elemento \<idn> (Configuración de URI)](idn-element-uri-settings.md)|Especifica si se aplica el análisis de nombres de dominio internacionalizados (IDN) a los nombres de dominio.|  
|[Elemento \<iriParsing> (Configuración de URI)](iriparsing-element-uri-settings.md)|Especifica si se aplica el análisis de identificadores de recursos internacionales (IRI) a un <xref:System.Uri> y si se deben aplicar reglas de análisis de IRI.|  
|[Elemento \<schemeSettings> (configuración de URI)](schemesettings-element-uri-settings.md)|Especifica cómo se analizará un <xref:System.Uri> para esquemas concretos.|  
  
## <a name="see-also"></a>Vea también

- [Configuración de aplicaciones de Internet](../../../network-programming/configuring-internet-applications.md)
- [Esquema de los archivos de configuración](../index.md)
