---
title: <security> de <netHttpBinding>
ms.date: 03/30/2017
ms.assetid: dc41f6f7-cabc-4a64-9fa0-ceabf861b348
ms.openlocfilehash: 890cee3271c410a921b3a88f78d0705ba8718252
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70399855"
---
# <a name="security-of-nethttpbinding"></a>\<> de seguridad \<de netHttpBinding >

Define las capacidades de seguridad de la [ \<> netHttpBinding](nethttpbinding.md).

[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<> System. serviceModel**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<> de enlaces**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<> netHttpBinding**](nethttpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<> de enlace**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<> de seguridad**  

## <a name="syntax"></a>Sintaxis

```xml
<security mode="Message/None/Transport/TransportWithCredential">
  <transport clientCredentialType="Basic/Certificate/Digest/None/Ntlm/Windows"
             proxyCredentialType="Basic/Digest/None/Ntlm/Windows"
             realm="string" />
  <message algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"
           clientCredentialType="Certificate/IssuedToken/None/UserName/Windows" />
</security>
```

## <a name="attributes-and-elements"></a>Atributos y elementos

En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.

### <a name="attributes"></a>Atributos

|Atributo|DESCRIPCIÓN|
|---------------|-----------------|
|modo|Opcional. Especifica el tipo de seguridad que se utiliza. El valor predeterminado es `None`. Este atributo es del tipo <xref:System.ServiceModel.BasicHttpSecurityMode>.|

## <a name="mode-attribute"></a>atributo de modo

|Valor|DESCRIPCIÓN|
|-----------|-----------------|
|None|: Los mensajes no están protegidos durante la transferencia.|
|Transporte|La seguridad se proporciona utilizando transporte HTTPS. Los mensajes SOAP se protegen utilizando HTTPS. El servicio se autentica al cliente utilizando el certificado X.509 del servicio. El cliente se autentica utilizando el ClientCredentialType proporcionado.|
|Message|La seguridad se proporciona mediante la seguridad del mensaje SOAP. De forma predeterminada, el cuerpo se cifra y firma. Para este enlace, el sistema requiere que el certificado de servidor se proporcione al cliente fuera de la banda. El único `ClientCredentialType` válido para este enlace es `Certificate`.|
|TransportWithMessageCredential|La seguridad de transporte proporciona integridad, confidencialidad y autenticación del servidor. La autenticación del cliente se proporciona por medio de la seguridad del mensaje SOAP. Este modo es pertinente cuando el usuario está autenticando utilizando el nombre de usuario/contraseña y existe una implementación del HTTP existente para proteger la transferencia del mensaje.|
|TransportCredentialOnly|Este modo no proporciona integridad del mensaje y confidencialidad. Proporciona la autenticación del cliente basada en http. Este modo se debe utilizar con precaución. Se debe usar en entornos en los que la seguridad de transporte se proporciona por otros medios (como IPSec) y la infraestructura de WCF proporciona únicamente la autenticación del cliente.|

### <a name="child-elements"></a>Elementos secundarios

|Elemento|DESCRIPCIÓN|
|-------------|-----------------|
|[\<> de transporte](transport-of-nethttpbinding.md)|Define los valores de seguridad de transporte para un servicio HTTP básico. Este elemento corresponde a <xref:System.ServiceModel.HttpTransportSecurity>.|
|[\<message>](message-of-nethttpbinding.md)|Define los valores de modo de seguridad para un servicio HTTP básico. Este elemento corresponde a <xref:System.ServiceModel.BasicHttpMessageSecurity>.|

### <a name="parent-elements"></a>Elementos primarios

|Elemento|DESCRIPCIÓN|
|-------------|-----------------|
|enlace|Elemento de enlace del [ \<> basicHttpBinding](basichttpbinding.md).|

## <a name="remarks"></a>Comentarios

 De forma predeterminada, no se protege el mensaje SOAP y no se autentica el cliente. Este elemento le permite establecer la configuración de seguridad adicional para el elemento `netHttpBinding`.

## <a name="see-also"></a>Vea también

- <xref:System.ServiceModel.NetHttpBinding.Security%2A>
- <xref:System.ServiceModel.Configuration.NetHttpBindingElement.Security%2A>  
- [Protección de servicios y clientes](../../../wcf/feature-details/securing-services-and-clients.md)
- [Selección de tipos de credenciales](../../../wcf/feature-details/selecting-a-credential-type.md)
- [Enlaces](../../../wcf/bindings.md)
- [Configuración de enlaces proporcionados por el sistema](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [Utilización de enlaces para configurar servicios y clientes](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](../../../misc/binding.md)
