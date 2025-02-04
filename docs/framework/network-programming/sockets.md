---
title: sockets
ms.date: 03/30/2017
helpviewer_keywords:
- application protocols, sockets
- sending data, sockets
- data requests, sockets
- Windows Sockets
- sockets, about sockets
- Socket class, about Socket class
- sockets
- requesting data from Internet, sockets
- network, sockets
- receiving data, sockets
- protocols, sockets
- Internet, sockets
ms.assetid: 10d22735-bd37-42c1-a2be-c1932f979a7d
ms.openlocfilehash: cffad6b4677a880bd63f5ae0232c639f7a262c59
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71047255"
---
# <a name="sockets"></a>sockets
El espacio de nombres <xref:System.Net.Sockets> contiene una implementación administrada de la interfaz de Windows Sockets. Las demás clases de acceso a la red del espacio de nombres <xref:System.Net> se basan en esta implementación de sockets.  
  
 La clase <xref:System.Net.Sockets.Socket> de .NET Framework es una versión de código administrado de los servicios de socket proporcionados por la API de Winsock32. En la mayoría de los casos, los métodos de la clase **Socket** solo serializan los datos en sus equivalentes nativos de Win32 y controlan las comprobaciones de seguridad necesarias.  
  
 La clase **Socket** admite dos modos básicos, el modo sincrónico y el modo asincrónico. En el modo sincrónico, las llamadas a funciones que efectúan operaciones de red (como <xref:System.Net.Sockets.Socket.Send%2A> y <xref:System.Net.Sockets.Socket.Receive%2A>) esperan a que finalice la operación antes de devolver el control al programa que realiza la llamada. En el modo asincrónico, estas llamadas vuelven inmediatamente.  
  
## <a name="see-also"></a>Vea también

- [Cómo: Crear un socket](how-to-create-a-socket.md)

- [Usar protocolos de aplicaciones](using-application-protocols.md)
