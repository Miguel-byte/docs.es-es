---
title: Proteger WCF Data Services
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- securing application [WCF Data Services]
- WCF Data Services, security
ms.assetid: 99fc2baa-a040-4549-bc4d-f683d60298af
ms.openlocfilehash: 642ff5fe3427509a4d4782fb8640f4b755d58459
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2019
ms.locfileid: "70790344"
---
# <a name="securing-wcf-data-services"></a>Proteger WCF Data Services
En este tema se describen las consideraciones de seguridad específicas para el desarrollo, la implementación y la ejecución de WCF Data Services y aplicaciones que tienen acceso a los servicios que admiten el Open Data Protocol (OData). También debe seguir las recomendaciones para crear aplicaciones de .NET Framework seguras.  
  
Al planear cómo proteger un servicio de OData basado en WCF Data Services, debe abordar la autenticación, el proceso de detección y comprobación de la identidad de una entidad de seguridad y la autorización, el proceso de determinar si una entidad de seguridad autenticada es se permite el acceso a los recursos solicitados. También debe plantearse si va a cifrar el mensaje mediante SSL.  
  
## <a name="authenticating-client-requests"></a>Autenticar las solicitudes de clientes  
WCF Data Services no implementa ningún tipo de autenticación propia, sino que se basa en las disposiciones de autenticación del host del servicio de datos. Esto significa que el servicio supone que cualquier solicitud que reciba ya se ha autenticado por el host de red y que el host ha identificado correctamente el principio de la solicitud adecuadamente a través de las interfaces proporcionadas por WCF Data Services. Estas opciones y enfoques de autenticación se detallan en la [serie de autenticación y OData](https://devblogs.microsoft.com/odata/?s=%22OData+and+authentication%22)de varias partes.  
  
### <a name="authentication-options-for-a-wcf-data-service"></a>Opciones de autenticación para un servicio de datos de WCF  
 En la siguiente tabla se enumeran algunos de los mecanismos de autenticación disponibles para ayudar al usuario a autenticar solicitudes en el servicio de datos de WCF.  
  
|Opciones de autenticación|DESCRIPCIÓN|  
|----------------------------|-----------------|  
|Autenticación anónima|Cuando está habilitada la autenticación HTTP anónima, cualquier entidad de seguridad puede conectarse al servicio de datos. No se necesitan credenciales para el acceso anónimo. Use esta opción solo cuando desee permitir a alguien el acceso al servicio de datos.|  
|Autenticación básica e implícita|Se necesitan credenciales formadas por un nombre de usuario y una contraseña para la autenticación. Admite autenticación de clientes que no sean de Windows. **Nota sobre la seguridad:**  Se envían credenciales de autenticación básica (nombre de usuario y contraseña) sin cifrado y se pueden interceptar. La autenticación implícita envía un hash basado en las credenciales proporcionadas. De esta forma, la protección es mayor que la de la autenticación básica. Ambas son susceptibles de sufrir ataques de tipo " Man in the middle". Cuando se usan estos métodos de autenticación, debe plantearse la comunicación cifrada entre el cliente y el servicio de datos mediante el uso de la Capa de sockets seguros (SSL). <br /><br /> Microsoft Internet Information Services (IIS) proporciona una implementación de autenticación básica e implícita para solicitudes HTTP en una aplicación ASP.NET. Esta implementación del proveedor de autenticación de Windows permite que una aplicación cliente de .NET Framework proporcione credenciales en el encabezado HTTP de la solicitud al servicio de datos para negociar sin ningún problema la autenticación de un usuario de Windows. Para obtener más información, consulte [referencia técnica de autenticación implícita](https://go.microsoft.com/fwlink/?LinkId=200408).<br /><br /> Si desea que el servicio de datos use la autenticación básica basada en algún servicio de autenticación personalizado y no en las credenciales de Windows, debe implementar un módulo HTTP ADP.NET personalizado para la autenticación.<br /><br /> Para ver un ejemplo de cómo usar un esquema de autenticación básica personalizado con WCF Data Services, consulte la entrada de blog [OData and Authentication (parte 6): autenticación básica personalizada](https://devblogs.microsoft.com/odata/odata-and-authentication-part-6-custom-basic-authentication/).|  
|Autenticación de Windows|Las credenciales basadas en Windows se intercambian mediante el uso de NTLM o Kerberos. Este mecanismo es más seguro que la autenticación básica o implícita, pero requiere que el cliente sea una aplicación basada en Windows. IIS también proporciona una implementación de autenticación de Windows para las solicitudes HTTP en una aplicación ASP.NET. Para obtener más información, consulte [Introducción a la autenticación de formularios ASP.net](https://docs.microsoft.com/previous-versions/aspnet/7t6b43z4(v=vs.100)).<br /><br /> Para ver un ejemplo de cómo usar la autenticación de Windows con WCF Data Services, consulte la entrada de blog sobre [OData y autenticación, parte 2, autenticación de Windows](https://devblogs.microsoft.com/odata/odata-and-authentication-part-2-windows-authentication/).|  
|Autenticación de formularios ASP.NET|La autenticación de formularios permite autenticar a los usuarios mediante su propio código y, a continuación, conservar un token de autenticación en una cookie o en la dirección URL de la página. Autentique el nombre de usuario y la contraseña de los usuarios que usen un formulario de inicio de sesión que cree. Las solicitudes no autenticadas se redirigen a una página de inicio de sesión, en la que el usuario proporciona las credenciales y envía el formulario. Si la aplicación autentica la solicitud, el sistema emite un vale que contiene una clave con el fin de restablecer la identidad para posteriores solicitudes. Para obtener más información, vea [proveedor de autenticación de formularios](https://docs.microsoft.com/previous-versions/aspnet/9wff0kyh(v=vs.100)). **Nota sobre la seguridad:**  De forma predeterminada, la cookie que contiene el vale de autenticación de formularios no se protege cuando se usa la autenticación de formularios en una aplicación Web ASP.NET. Debe plantearse exigir SSL para proteger tanto el vale de autenticación como las credenciales de inicio de sesión iniciales. <br /><br /> Para obtener un ejemplo de cómo usar la autenticación de formularios con WCF Data Services, vea la entrada de blog [OData and Authentication – parte 7: autenticación de formularios](https://devblogs.microsoft.com/odata/odata-and-authentication-part-7-forms-authentication/).|  
|Autenticación basada en notificaciones|En la autenticación basada en notificaciones, el servicio de datos se basa en un servicio de proveedor de identidad "de terceros" de confianza para autenticar al usuario. El proveedor de identidad autentica positivamente al usuario que solicita acceso a los recursos del servicio de datos y emite un token que concede acceso a los recursos solicitados. A continuación, este token se presenta en el servicio de datos, que concede acceso al usuario basándose en la relación de confianza con el servicio de identidad que emitió el token de acceso.<br /><br /> La ventaja de usar un proveedor de autenticación basado en notificaciones es que se pueden usar para autenticar distintos tipos de clientes en dominios de confianza. Si se usan tales proveedores de terceros, un servicio de datos puede descargar los requisitos de mantenimiento y autenticación de usuarios. OAuth 2.0 es un protocolo de autenticación basado en notificaciones compatible con Access Control de AppFabric de Microsoft Azure para autorización federada como servicio. Este protocolo admite servicios basados en REST. Para ver un ejemplo de cómo usar OAuth 2,0 con WCF Data Services, consulte la entrada de blog [OData and Authentication – Part 8 – OAUTH Wrap](https://devblogs.microsoft.com/odata/odata-and-authentication-part-8-oauth-wrap/).|  
  
<a name="clientAuthentication"></a>   
### <a name="authentication-in-the-client-library"></a>Autenticación de la biblioteca cliente  
 De forma predeterminada, la biblioteca de cliente de WCF Data Services no proporciona credenciales cuando se realiza una solicitud a un servicio de OData. Cuando el servicio de datos necesita credenciales de inicio de sesión para autenticar a un usuario, estas credenciales se puedan proporcionar en una clase <xref:System.Net.NetworkCredential> a la que se accede desde la propiedad <xref:System.Data.Services.Client.DataServiceContext.Credentials%2A> de la clase <xref:System.Data.Services.Client.DataServiceContext>, como en el ejemplo siguiente:  
  
```csharp  
// Set the client authentication credentials.  
context.Credentials =  
    new NetworkCredential(userName, password, domain);  
```  
  
```vb  
' Set the client authentication credentials.  
context.Credentials = _  
    New NetworkCredential(userName, password, domain)  
```  
  
 Para obtener más información, consulte [Cómo Especifique las credenciales de cliente para una](specify-client-creds-for-a-data-service-request-wcf.md)solicitud de servicio de datos.  
  
 Cuando el servicio de datos necesite credenciales de inicio de sesión que no se puedan especificar mediante el uso de un objeto <xref:System.Net.NetworkCredential>, como un token basado en notificaciones o una cookie, debe establecer manualmente los encabezados en la solicitud HTTP, que suelen ser los encabezados `Authorization` y `Cookie`. Para obtener más información sobre este tipo de escenario de autenticación, vea la entrada de blog sobre [OData y autenticación, parte 3, enlaces de cliente](https://devblogs.microsoft.com/odata/odata-and-authentication-part-3-clientside-hooks/). Para obtener un ejemplo de cómo establecer encabezados HTTP en un mensaje de solicitud, consulte [cómo: Establezca los encabezados en la solicitud](how-to-set-headers-in-the-client-request-wcf-data-services.md)de cliente.  
  
## <a name="impersonation"></a>Suplantación  
 Por lo general, el servicio de datos accede a los recursos necesarios, como los archivos del servidor o de la base de datos, mediante el uso de las credenciales del proceso de trabajo que hospeda el servicio de datos. Al usar la suplantación, las aplicaciones de ASP.NET pueden ejecutarse con la identidad de Windows (cuenta de usuario) del usuario que realiza la solicitud. La suplantación se suele usar en aplicaciones que confían en IIS para autenticar al usuario y las credenciales de esta entidad de seguridad se usan para obtener acceso a los recursos necesarios. Para obtener más información, vea [suplantación de ASP.net](https://docs.microsoft.com/previous-versions/aspnet/xh507fc5(v=vs.100)).  
  
## <a name="configuring-data-service-authorization"></a>Configurar la autorización del servicio de datos  
 La autorización es la concesión de acceso a los recursos de la aplicación a una entidad de seguridad o a un proceso que se identifique basándose en una autenticación correcta previa. Como regla general, solo debe conceder los derechos estrictamente necesarios a los usuarios del servicio de datos para realizar las operaciones que necesiten las aplicaciones cliente.  
  
### <a name="restrict-access-to-data-service-resources"></a>Restringir el acceso a los recursos del servicio de datos  
 De forma predeterminada, WCF Data Services le permite conceder acceso de lectura y escritura común a los recursos del servicio de datos (conjunto de entidades y operaciones de servicio) a cualquier usuario que pueda tener acceso al servicio de datos. Las reglas que definen el acceso de lectura y escritura se pueden definir por separado para cada conjunto de entidades expuesto por el servicio de datos, así como a las operaciones de servicio. Se recomienda limitar el acceso tanto de lectura como de escritura a solo los recursos que necesite la aplicación cliente. Para obtener más información, vea [requisitos mínimos de acceso a recursos](configuring-the-data-service-wcf-data-services.md#accessRequirements).  
  
### <a name="implement-role-based-interceptors"></a>Implementar interceptores basados en roles  
 Los interceptores permiten interceptar solicitudes en los recursos del servicio de datos antes de que actúe en ellos dicho servicio. Para obtener más información, vea [interceptores](interceptors-wcf-data-services.md). Los interceptores le permiten tomar decisiones de autorización basadas el usuario autenticado que está realizando la solicitud. Para obtener un ejemplo de cómo restringir el acceso a los recursos del servicio de datos en función de una [identidad de usuario autenticada, consulte How to: Interceptar mensajes](how-to-intercept-data-service-messages-wcf-data-services.md)del servicio de datos.  
  
### <a name="restrict-access-to-the-persisted-data-store-and-local-resources"></a>Restringir el acceso al almacén de datos persistentes y a los recursos locales  
 A las cuentas que se usan para acceder al almacén persistente se les deben conceder solo los derechos estrictamente necesarios en una base de datos o en el sistema de archivos para admitir los requisitos del servicio de datos. Cuando se usa la autenticación anónima, se trata de la cuenta usada para ejecutar la aplicación de hospedaje. Para obtener más información, consulte [Cómo Desarrolle un servicio de datos de WCF](how-to-develop-a-wcf-data-service-running-on-iis.md)que se ejecute en IIS. Cuando se usa la suplantación, a los usuarios autenticados se les debe conceder acceso a estos recursos, normalmente como parte de un grupo de Windows.  
  
## <a name="other-security-considerations"></a>Otras consideraciones de seguridad  
  
### <a name="secure-the-data-in-the-payload"></a>Proteger los datos de la carga  
OData se basa en el protocolo HTTP. En un mensaje HTTP, el encabezado puede contener valiosas credenciales de usuario, en función de la autenticación implementada por el servicio de datos. El cuerpo del mensaje también puede contener datos valiosos de clientes que se deben proteger. En ambos casos, se recomienda que use SSL para proteger esta información a través de la conexión.  
  
### <a name="ignored-message-headers-and-cookies"></a>Cookies y encabezados del mensaje ignorados  
 Los encabezados de solicitudes HTTP, que no sean los que declaran los tipos de contenido y las ubicaciones de los recursos, se ignoran y nunca los establece el servicio de datos.  
  
 Las cookies se pueden usar como parte de un esquema de autenticación, por ejemplo, con la autenticación de formularios ASP.NET. Sin embargo, las cookies HTTP establecidas en una solicitud entrante se omiten en los servicios de servicio de WCF. El host de un servicio de datos puede procesar la cookie, pero el tiempo de ejecución de WCF Data Services nunca analiza o devuelve cookies. La biblioteca de cliente de WCF Data Services tampoco procesa cookies enviadas en la respuesta.  
  
### <a name="custom-hosting-requirements"></a>Requisitos personalizados de hospedaje  
 De forma predeterminada, WCF Data Services se crea como una aplicación ASP.NET hospedada en IIS. De esta forma, el servicio de datos puede sacar provecho de los comportamientos seguros de esta plataforma. Puede definir WCF Data Services que se hospedan en un host personalizado. Para obtener más información, vea [hospedar el servicio de datos](hosting-the-data-service-wcf-data-services.md). Los componentes y la plataforma que hospedan un servicio de datos deben asegurar los siguientes comportamientos de seguridad para impedir ataques contra el servicio de datos:  
  
- Limitar la longitud del URI aceptada en una solicitud del servicio de datos para todas las operaciones posibles.  
  
- Limitar el tamaño de los mensajes HTTP tanto entrantes como salientes.  
  
- Limitar el número total de solicitudes pendientes en cualquier momento dado.  
  
- Limite el tamaño de los encabezados HTTP y sus valores, y proporcione WCF Data Services acceso a los datos de encabezado.  
  
- Detectar y contraatacar los ataques conocidos, como ataques SYN de TCP y de reproducción de mensajes.  
  
### <a name="values-are-not-further-encoded"></a>Los valores ya no se codifican  
 Los valores de propiedad enviados al servicio de datos no se codifican en tiempo de ejecución de WCF Data Services. Por ejemplo, cuando una propiedad de cadena de una entidad contiene contenido HTML con formato, el servicio de datos no codifica las etiquetas en HTML. Además, el servicio de datos ya no codifica los valores de propiedad de la respuesta. Asimismo, la biblioteca cliente ya no efectúa ningún tipo de codificación adicional.  
  
### <a name="considerations-for-client-applications"></a>Consideraciones sobre aplicaciones cliente  
 Las siguientes consideraciones de seguridad se aplican a las aplicaciones que utilizan el cliente de WCF Data Services para tener acceso a los servicios de OData:  
  
- La biblioteca cliente asume que los protocolos usados para acceder al servicio de datos proporcionan un nivel de seguridad adecuado.  
  
- La biblioteca cliente usa todos los valores predeterminados para las opciones de tiempos de espera y de análisis de las pilas de transporte proporcionadas por la plataforma subyacente.  
  
- La biblioteca cliente no lee la configuración a partir de los archivos de configuración de la aplicación.  
  
- La biblioteca cliente no implementa los mecanismos de acceso entre dominios. En su lugar, confía en los mecanismos proporcionados por la pila HTTP subyacente.  
  
- La biblioteca cliente no dispone de elementos de interfaz de usuario y nunca intenta mostrar o presentar los datos que recibe o envía.  
  
- Se recomienda que las aplicaciones cliente siempre validen la entrada del usuario, así como los datos aceptados de servicios que no sean de confianza.  
  
## <a name="see-also"></a>Vea también

- [Definir Servicios de datos de WCF](defining-wcf-data-services.md)
- [Biblioteca cliente de Servicios de datos de WCF](wcf-data-services-client-library.md)
