---
title: <peerTransport>
ms.date: 03/30/2017
ms.assetid: c1a5013a-9dd4-4a27-b114-795b8b323177
ms.openlocfilehash: d896953a7ed31fdaf5f357a8721c7d085d50bc56
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70400049"
---
# <a name="peertransport"></a>\<peerTransport>
Define un transporte del mismo nivel para un enlace personalizado.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<> System. serviceModel**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<> de enlaces**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<customBinding >** ](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<> de enlace**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<> peerTransport**  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<peerTransport listenIpAddress="String"
               maxBufferPoolSize="Integer"
               maxReceivedMessageSize="Integer"
               port="Integer">
  <security>
  </security>
</peerTransport>
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|DESCRIPCIÓN|  
|---------------|-----------------|  
|listenIpAddress|Una cadena que especifica una dirección IP en la que el nodo entre pares realizará escuchas para los mensajes del TCP. El valor predeterminado es `null`.|  
|maxBufferPoolSize|Un entero positivo que especifica el tamaño máximo del grupo de búferes. El valor predeterminado es 524288.<br /><br /> Muchas partes de los búferes de uso WCF. Crear y destruir búferes cada vez que se usan es caro, y la recolección de elementos no utilizados para los búferes también es cara. Con grupos de búferes, puede tomar un búfer del grupo, usarlo y devolverlo al grupo una vez haya terminado. Así se evita la sobrecarga al crear y destruir búferes.|  
|maxReceivedMessageSize|Un entero positivo que define el tamaño de mensaje máximo en bytes incluidos los encabezados. El remitente de un mensaje recibe un error SOAP cuando el mensaje es demasiado grande para el receptor. El destinatario quita el mensaje y crea una entrada del evento en el registro de seguimiento. El valor predeterminado es 65536.|  
|port|Un entero que especifica el puerto de la interfaz de red en el que este enlace procesará los mensajes de TCP de canal del mismo nivel. Dicho valor debe encontrarse entre <xref:System.Net.IPEndPoint.MinPort> y <xref:System.Net.IPEndPoint.MaxPort>. El valor predeterminado es 0.|  
  
### <a name="child-elements"></a>Elementos secundarios  
  
|Elemento|DESCRIPCIÓN|  
|-------------|-----------------|  
|[\<security>](security-of-peertransport.md)|Define la configuración de seguridad para este transporte. Este elemento es del tipo <xref:System.ServiceModel.Configuration.PeerSecurityElement>.|  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|DESCRIPCIÓN|  
|-------------|-----------------|  
|[\<binding>](../../../misc/binding.md)|Define todas las funcionalidades de enlace del enlace personalizado.|  
  
## <a name="remarks"></a>Comentarios  
 Este transporte no se puede utilizar con contratos que tengan operaciones respuesta-solicitud.  
  
## <a name="see-also"></a>Vea también

- <xref:System.ServiceModel.Configuration.PeerTransportElement>
- <xref:System.ServiceModel.Channels.PeerTransportBindingElement>
- <xref:System.ServiceModel.Channels.TransportBindingElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [Transportes](../../../wcf/feature-details/transports.md)
- [Elección del transporte](../../../wcf/feature-details/choosing-a-transport.md)
- [Enlaces](../../../wcf/bindings.md)
- [Extensión de enlaces](../../../wcf/extending/extending-bindings.md)
- [Enlaces personalizados](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
