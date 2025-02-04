---
title: Información general de enlaces de Windows Communication Foundation
ms.date: 03/30/2017
helpviewer_keywords:
- bindings [WCF], overview
ms.assetid: cfb5842f-e0f9-4c56-a015-f2b33f258232
ms.openlocfilehash: 8449fe048cc9149e8e8cf02f27f131c0d90d6984
ms.sourcegitcommit: 127343afce8422bfa944c8b0c4ecc8f79f653255
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2019
ms.locfileid: "67348195"
---
# <a name="windows-communication-foundation-bindings-overview"></a>Información general de enlaces de Windows Communication Foundation
Los enlaces son objetos que se usan para especificar los detalles de comunicación que son necesarias para conectarse al punto de conexión de un servicio de Windows Communication Foundation (WCF). Cada punto de conexión en un servicio WCF requiere un enlace esté bien especificado. En este tema se describe los tipos de datos de comunicación que definen los enlaces, los elementos de un enlace, qué enlaces están incluidos en WCF y cómo se puede especificar un enlace para un punto de conexión.  
  
## <a name="what-a-binding-defines"></a>Qué define un enlace  
 La información de un enlace puede ser muy básica o muy compleja. El enlace más básico especifica solo el protocolo de transporte (como HTTP) que se debe utilizar para conectar al extremo. Por lo general, la información que contiene un enlace sobre cómo conectarse a un punto de conexión queda incluida en una de las siguientes categorías:  
  
 **Protocolos**  
 Determina el mecanismo de seguridad utilizado: función de la mensajería de confianza o configuración de flujo de contexto de transacción.  
  
 **Codificación**  
 Determina la codificación del mensaje (por ejemplo, texto o binario).  
  
 **Transporte**  
 Determina el protocolo de transporte subyacente que se utilizará (por ejemplo, TCP o HTTP).  
  
## <a name="the-elements-of-a-binding"></a>Los elementos de un enlace  
 Un enlace está básicamente compuesto de una pila ordenada de elementos de enlace, cada uno de los cuales especifica parte de la información de la comunicación requerida para conectar a un punto de conexión de servicio. Las dos capas más bajas de la pila son necesarias. En la base de la pila se encuentra el elemento de enlace de transporte y justo antes que éste se encuentra el elemento que contiene las especificaciones de la codificación del mensaje. Los elementos de enlace opcionales que especifican los demás protocolos de comunicación se superponen a estos dos elementos necesarios. Para obtener más información acerca de estos elementos de enlace y su orden correcto, consulte [enlaces personalizados](../../../docs/framework/wcf/extending/custom-bindings.md).  
  
## <a name="system-provided-bindings"></a>Enlaces proporcionados por el sistema  
 La información de un enlace puede ser compleja y puede que parte de su configuración no sea compatible con otros. Por este motivo, WCF incluye un conjunto de enlaces proporcionados por el sistema. Estos enlaces están diseñados para cubrir la mayoría de los requisitos de aplicación. Las clases siguientes representan algunos ejemplos de enlaces proporcionados por el sistema:  
  
- <xref:System.ServiceModel.BasicHttpBinding>: Un protocolo HTTP enlace adecuado para conectarse a servicios Web que se ajusta a WS-I especificación del perfil básico (por ejemplo, a servicios basados en servicios Web de ASP.NET).  
  
- <xref:System.ServiceModel.WSHttpBinding>: Un enlace interoperable adecuado para conectar a los puntos de conexión que cumplen con WS-* protocolos.  
  
- <xref:System.ServiceModel.NetNamedPipeBinding>: Usa .NET Framework para conectarse a otros extremos WCF en el mismo equipo.  
  
- <xref:System.ServiceModel.NetMsmqBinding>: Usos en .NET Framework para crear la cola de mensajes conexiones con otros extremos WCF.  

- <xref:System.ServiceModel.NetTcpBinding>: Este enlace ofrece un mayor rendimiento respecto enlaces HTTP y es ideal para su uso en una red local.
  
 Para obtener una lista completa, con descripciones de todos los enlaces proporcionados por WCF, vea [System-provided Bindings](../../../docs/framework/wcf/system-provided-bindings.md).  
  
## <a name="using-your-own-bindings"></a>Utilizar sus propios enlaces  
 Si ninguno de los enlaces proporcionados por el sistema incluidos tiene la combinación correcta de características que requiere una aplicación de servicio, puede crear su propio enlace. Hay dos formas de hacerlo. Puede crear un nuevo enlace a partir de elementos de enlace ya existentes mediante un objeto <xref:System.ServiceModel.Channels.CustomBinding> o puede crear un enlace completamente definido por el usuario derivando del enlace <xref:System.ServiceModel.Channels.Binding>. Para obtener más información acerca de cómo crear su propio enlace mediante estos dos enfoques, vea [enlaces personalizados](../../../docs/framework/wcf/extending/custom-bindings.md) y [crear enlaces](../../../docs/framework/wcf/extending/creating-user-defined-bindings.md).  
  
## <a name="using-bindings"></a>Utilizar los enlaces  
 El uso de enlaces conlleva dos pasos básicos:  
  
1. Seleccione o defina un enlace. El método más fácil es elegir uno de los enlaces proporcionados por el sistema incluidos con WCF y su uso con sus valores predeterminados. Puede elegir también un enlace proporcionado por el sistema y restablecer sus valores de propiedad para satisfacer sus necesidades Otra manera es crear un enlace personalizado o un enlace definido por el usuario para tener grados de control y personalización más altos.  
  
2. Cree un punto de conexión que utilice el enlace seleccionado o definido.  
  
## <a name="code-and-configuration"></a>Código y configuración  
 Puede definir los enlaces de dos maneras: a través del código o a través de la configuración. Estos dos enfoques no dependen de si está utilizando un enlace proporcionado por el sistema o un enlace personalizado. En general, utilizar el código le proporciona un control total sobre la definición de un enlace y el tiempo de diseño. Con la configuración, por otro lado, permite que un administrador del sistema o el usuario de un servicio WCF o cliente cambiar los parámetros de un enlace sin tener que volver a compilar la aplicación de servicio. Esta flexibilidad es a menudo deseable porque no hay ninguna manera de predecir los requisitos específicos del equipo en el que es implementar una aplicación de WCF. Dejar fuera la información de enlace (y el direccionamiento) del código les permite cambiar sin requerir recopilación o nueva implementación de la aplicación. Tenga en cuenta que se crean enlaces definidos en código después de los enlaces especificados en la configuración, de modo que se permite a los enlaces definidos por código sobrescribir los enlaces definidos por la configuración.  
  
## <a name="see-also"></a>Vea también

- [Utilización de enlaces para configurar servicios y clientes](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)
