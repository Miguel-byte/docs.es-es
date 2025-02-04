---
title: Selección del sistema operativo de destino con contenedores de .NET
description: Arquitectura de microservicios de .NET para aplicaciones .NET en contenedor | Selección del sistema operativo de destino con contenedores de .NET
ms.date: 01/07/2019
ms.openlocfilehash: 7380889374e69ca4d3c981a401af703c19263de5
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71039689"
---
# <a name="what-os-to-target-with-net-containers"></a>Selección del sistema operativo de destino con contenedores de .NET

Teniendo en cuenta la diversidad de sistemas operativos compatibles con Docker y las diferencias entre .NET Framework y .NET Core, debe escoger un sistema operativo de destino específico y versiones específicas según el marco que utilice.

Para Windows, puede usar Windows Server Core o Nano Server de Windows. Estas versiones de Windows proporcionan diferentes características (IIS en Windows Server Core frente a un servidor web autohospedado, como Kestrel, en Nano Server) que .NET Framework o .NET Core, respectivamente, podrían necesitar.

Para Linux, hay varias distribuciones disponibles y compatibles en imágenes oficiales del Docker de .NET (por ejemplo, Debian).

En la Figura 3-1 se puede ver la posible versión de sistema operativo en función de la versión de .NET Framework que se utilice.

![Al implementar aplicaciones heredadas de .NET Framework que tienen como destino Windows Server Core, compatible con aplicaciones heredadas e IIS, tiene una imagen más grande. Al implementar aplicaciones de .NET Core, puede tener como destino Windows Nano Server, que está optimizado para la nube, usa Kestrel y es más pequeño y se inicia más rápido. También puede tener como destino Linux, con compatibilidad con Debian, Alpine y otros. También usa Kestrel y es más pequeño y se inicia más rápido.](./media/image1.png)

**Figura 3-1.** Sistemas operativos de destino en función de las versiones de .NET Framework

También puede crear su propia imagen de Docker en los casos en que quiera utilizar una distribución de Linux diferente o que quiera una imagen con las versiones no proporcionadas por Microsoft. Por ejemplo, puede crear una imagen con ASP.NET Core ejecutándose en los tradicionales .NET Framework y Windows Server Core, que no sería un escenario tan habitual para Docker.

Al agregar el nombre de imagen al archivo Dockerfile, puede seleccionar el sistema operativo y la versión dependiendo de la etiqueta que utilice, como en los ejemplos siguientes:

| Imagen | Comentarios |
|-------|----------|
| mcr.microsoft.com/dotnet/core/runtime:2.2 | Arquitectura múltiple de .NET Core 2.2: es compatible con Linux y Windows Nano Server en función del host de Docker. |
| mcr.microsoft.com/dotnet/core/aspnet:2.2 | Arquitectura múltiple de .NET Core 2.2: es compatible con Linux y Windows Nano Server en función del host de Docker. <br/> La imagen de aspnetcore tiene algunas optimizaciones para ASP.NET Core. |
| mcr.microsoft.com/dotnet/core/aspnet:2.2-alpine | .NET Core 2.2 solo en tiempo de ejecución en una distribución de Alpine Linux |
| mcr.microsoft.com/dotnet/core/aspnet:2.2-nanoserver-1803 | .NET Core 2.2 solo en tiempo de ejecución en Windows Nano Server (Windows Server 1803) |

> [!div class="step-by-step"]
> [Anterior](container-framework-choice-factors.md)
> [Siguiente](official-net-docker-images.md)
