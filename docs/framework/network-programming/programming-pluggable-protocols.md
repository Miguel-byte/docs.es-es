---
title: programar protocolos acoplables
ms.date: 03/30/2017
helpviewer_keywords:
- downloading Internet resources, pluggable protocols
- WebRequest class, pluggable protocols
- response to Internet request, pluggable protocols
- WebResponse class, pluggable protocols
- sending data, pluggable protocols
- network resources, pluggable protocols
- Internet, pluggable protocols
- programming pluggable protocols
- pluggable protocols, programming
- requesting data from Internet, pluggable protocols
- receiving data, pluggable protocols
- protocols, pluggable
ms.assetid: 66ef8456-7576-4e97-8956-959b216373db
ms.openlocfilehash: 94dfedd317782b9e518df02c84d9af55b1ef2b69
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71047401"
---
# <a name="programming-pluggable-protocols"></a>programar protocolos acoplables
Las clases abstractas <xref:System.Net.WebRequest> y <xref:System.Net.WebResponse> proporcionan la base para los protocolos conectables. Al derivar clases específicas del protocolo de <xref:System.Net.WebRequest> y <xref:System.Net.WebResponse>, una aplicación puede solicitar datos desde un recurso de Internet y leer la respuesta sin especificar el protocolo que se está usando.  
  
 Para poder crear una <xref:System.Net.WebRequest> específica del protocolo, debe registrar su método Create. Use el método estático <xref:System.Net.WebRequest.RegisterPrefix%28System.String%2CSystem.Net.IWebRequestCreate%29> de <xref:System.Net.WebRequest> para registrar una <xref:System.Net.WebRequest> descendiente para controlar un conjunto de solicitudes a un esquema concreto de Internet, a un servidor y un esquema, o a un esquema, servidor y ruta de acceso.  
  
 En la mayoría de los casos podrá enviar y recibir datos mediante los métodos y propiedades de la clase <xref:System.Net.WebRequest>. Pero si necesita tener acceso a propiedades específicas del protocolo, puede convertir el tipo de una <xref:System.Net.WebRequest> a una instancia específica de la clase derivada.  
  
 Para aprovechar las ventajas de los protocolos conectables, los descendientes de <xref:System.Net.WebRequest> deben proporcionar una transacción predeterminada de solicitud y respuesta que no requiera establecer propiedades específicas del protocolo. Por ejemplo, la clase <xref:System.Net.HttpWebRequest>, que implementa la clase <xref:System.Net.WebRequest> para HTTP, proporciona una solicitud `GET` de forma predeterminada y devuelve una <xref:System.Net.HttpWebResponse> que contiene la secuencia devuelta desde el servidor web.  
  
## <a name="see-also"></a>Vea también

- [Derivar de WebRequest](deriving-from-webrequest.md)
- [Derivar de WebResponse](deriving-from-webresponse.md)
- [Programación para redes en .NET Framework](index.md)
- [Cómo: Convertir un elemento WebRequest a propiedades específicas del protocolo de acceso](how-to-typecast-a-webrequest-to-access-protocol-specific-properties.md)
