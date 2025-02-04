---
title: <security> de <ws2007HttpBinding>
ms.date: 03/30/2017
ms.assetid: fdda0ff7-b462-4e26-af52-e87ddab71945
ms.openlocfilehash: ab5969da6a2d7cb59c057fd5bb909add6b6398a4
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70399785"
---
# <a name="security-of-ws2007httpbinding"></a>\<> de seguridad \<de ws2007HttpBinding >
Representa la configuración de seguridad utilizada con [ \<](ws2007httpbinding.md) el elemento > de ws2007HttpBinding.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<> System. serviceModel**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<> de enlaces**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<> ws2007HttpBinding**](ws2007httpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<> de enlace**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<> de seguridad**  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<system.serviceModel>
  <bindings>
    <ws2007HttpBinding>
      <binding name = "String">
        <security mode="None/Message/Transport/TransportWithMessageCredential">
          <transport>
          </transport>
          <message>
          </message>
        </security>
      </binding>
    </ws2007HttpBinding>
  </bindings>
</system.ServiceModel>
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|DESCRIPCIÓN|  
|---------------|-----------------|  
|`mode`|Opta. Especifica el tipo de seguridad que se aplica. El valor predeterminado es `Message`.<br /><br /> Este atributo es del tipo <xref:System.ServiceModel.SecurityMode>.|  
  
## <a name="mode-attribute"></a>Atributo de modo  
  
|Valor|DESCRIPCIÓN|  
|-----------|-----------------|  
|`None`|La seguridad está deshabilitada.|  
|`Transport`|La seguridad se proporciona utilizando HTTPS. El servicio se debe configurar con certificados de Capa de sockets seguros (SSL). El mensaje se protege completamente utilizando HTTPS y el servicio se autentica por el cliente usando el certificado SSL del servicio. La autenticación del cliente se controla a `ClientCredentials` través del atributo [ \<](transport-of-ws2007httpbinding.md) del elemento > de transporte.|  
|`Message`|La seguridad se proporciona mediante la seguridad del mensaje SOAP. De forma predeterminada, el cuerpo SOAP se cifra y firma. Este modo ofrece diversas características, como si las credenciales del servicio están disponibles para el cliente fuera de la banda, el conjunto de algoritmos que se van a usar y qué nivel de protección se aplica al cuerpo del mensaje a través de <xref:System.ServiceModel.Security.SecurityMessageProperty>. Se realiza la autenticación del cliente una vez por cada sesión y los resultados de autenticación están almacenados en memoria caché durante la duración de la sesión.|  
|`TransportWithMessageCredential`|En este modo, HTTPS proporciona integridad, confidencialidad y autenticación de servidor y la seguridad del mensaje SOAP proporciona la autenticación del cliente. De manera predeterminada, se realiza la autenticación del cliente una vez por cada sesión y los resultados de autenticación están almacenados en la memoria caché durante la duración de la sesión.|  
  
### <a name="child-elements"></a>Elementos secundarios  
  
|Elemento|DESCRIPCIÓN|  
|-------------|-----------------|  
|[\<> de transporte](transport-of-ws2007httpbinding.md)|Define la configuración de seguridad para el transporte. Este elemento corresponde al tipo <xref:System.ServiceModel.Configuration.HttpTransportSecurityElement>. Esta configuración se aplica sólo cuando el modo se establece en Transporte.|  
|[\<message>](message-of-ws2007httpbinding.md)|Define la configuración de seguridad del mensaje. Este elemento corresponde al tipo <xref:System.ServiceModel.Configuration.MessageSecurityOverHttpElement>. Esta configuración no se aplica cuando el modo se establece en Transporte.|  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|DESCRIPCIÓN|  
|-------------|-----------------|  
|[\<ws2007HttpBinding>](ws2007httpbinding.md)|Un enlace seguro para las aplicaciones de transporte HTTP.|  
  
## <a name="remarks"></a>Comentarios  
 Este elemento está diseñado para la interoperación con servicios que implementan las especificaciones de WS-*. La seguridad de transporte para este enlace es Capa de sockets seguros (SSL) sobre HTTP o HTTPS.  
  
## <a name="see-also"></a>Vea también

- <xref:System.ServiceModel.WSHttpSecurity>
- <xref:System.ServiceModel.WSHttpBinding.Security%2A>
- <xref:System.ServiceModel.Configuration.WSHttpBindingElement.Security%2A>
- <xref:System.ServiceModel.Configuration.WSHttpSecurityElement>
- <xref:System.ServiceModel.BasicHttpSecurity>
- [Protección de servicios y clientes](../../../wcf/feature-details/securing-services-and-clients.md)
- [Enlaces](../../../wcf/bindings.md)
- [Configuración de enlaces proporcionados por el sistema](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [Utilización de enlaces para configurar servicios y clientes](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](../../../misc/binding.md)
