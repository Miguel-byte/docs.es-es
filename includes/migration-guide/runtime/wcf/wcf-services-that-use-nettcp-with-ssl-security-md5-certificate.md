---
ms.openlocfilehash: ae3766e2045b5834fbf6ea20415942413b1590c0
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67858477"
---
### <a name="wcf-services-that-use-nettcp-with-ssl-security-and-md5-certificate-authentication"></a>Servicios de WCF que usan NETTCP con seguridad SSL y autenticación de certificados MD5

|   |   |
|---|---|
|Detalles|.NET Framework 4.6 añade TLS 1.1 y TLS 1.2 a la lista de protocolos predeterminados de SSL de WCF. Cuando los equipos cliente y servidor tienen .NET Framework 4.6 o una versión posterior instalada, se usa TLS 1.2 para la negociación. TLS 1.2 no admite la autenticación de certificados MD5. Como consecuencia, si un cliente utiliza un certificado MD5, el cliente de WCF no se podrá conectar al servicio WCF.|
|Sugerencia|Puede evitar este problema para que el cliente WCF pueda conectarse a un servidor WCF realizando alguno de los siguientes procedimientos:<ul><li>Actualizar el certificado para que no use el algoritmo MD5. Esta es la solución recomendada.</li><li>Si la vinculación no se configura dinámicamente en el código fuente, actualice el archivo de configuración de la aplicación para usar TLS 1.1 o una versión anterior del protocolo. Esto le permite seguir usando un certificado con el algoritmo hash MD5.</li></ul> <blockquote> [!WARNING] Esta solución no es recomendable, puesto que se considera que el algoritmo hash MD5 no es seguro.</blockquote> El archivo de configuración siguiente realiza esta tarea:<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;system.serviceModel&gt;&#13;&#10;&lt;bindings&gt;&#13;&#10;&lt;netTcpBinding&gt;&#13;&#10;&lt;binding&gt;&#13;&#10;&lt;security mode= &quot;None/Transport/Message/TransportWithMessageCredential&quot; &gt;&#13;&#10;&lt;transport clientCredentialType=&quot;None/Windows/Certificate&quot;&#13;&#10;protectionLevel=&quot;None/Sign/EncryptAndSign&quot;&#13;&#10;sslProtocols=&quot;Ssl3/Tls1/Tls11&quot;&gt;&#13;&#10;&lt;/transport&gt;&#13;&#10;&lt;/security&gt;&#13;&#10;&lt;/binding&gt;&#13;&#10;&lt;/netTcpBinding&gt;&#13;&#10;&lt;/bindings&gt;&#13;&#10;&lt;/system.ServiceModel&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre><ul><li>Si la vinculación se configura dinámicamente en el código fuente, actualice la propiedad <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols?displayProperty=nameWithType> para usar TLS 1.1 (<xref:System.Security.Authentication.SslProtocols.Tls11?displayProperty=nameWithType>) o una versión anterior del protocolo en el código fuente.</li></ul> <blockquote> [!WARNING] Esta solución no es recomendable, puesto que se considera que el algoritmo hash MD5 no es seguro.</blockquote> |
|Ámbito|Secundaria|
|Versión|4.6|
|Tipo|Tiempo de ejecución|

