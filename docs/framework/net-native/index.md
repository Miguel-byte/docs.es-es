---
title: Compilar aplicaciones con .NET Native
ms.date: 03/30/2017
helpviewer_keywords:
- native compilation
- .NET and native code
- compilation with .NET Native
- .NET Native
- C# and native compilation
ms.assetid: 47cd5648-9469-4b1d-804c-43cc04384045
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5993cfdb0f50d8e474a4f18280d181d9ec2fdfa4
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049655"
---
# <a name="compiling-apps-with-net-native"></a>Compilar aplicaciones con .NET Native

.NET Native es una tecnología de precompilación para compilar e implementar aplicaciones de Windows que se incluyen con Visual Studio 2015 y versiones posteriores. Su función es compilar automáticamente, a código nativo, aquellas versiones de lanzamiento de las aplicaciones escritas en código administrado (C# o Visual Basic) y que tienen como destino .NET Framework y Windows 10.

Normalmente, las aplicaciones que tienen como destino .NET Framework se compilan en lenguaje intermedio (IL). En tiempo de ejecución, el compilador Just-In-Time (JIT) convierte el IL en código nativo. En cambio, .NET Native compila aplicaciones de Windows directamente en código nativo. Para los desarrolladores, esto significa:

- Las aplicaciones incluyen el rendimiento del código nativo. Normalmente, el rendimiento será superior al código que se compila primero en IL y que, a continuación, se compila en código nativo mediante el compilador JIT.

- Puede seguir programando en C# o Visual Basic.

- Puede continuar beneficiándose de los recursos proporcionados por .NET Framework, incluida su biblioteca de clases, la administración automática de memoria, la recolección de elementos no utilizados y el control de excepciones.

En el caso de los usuarios de las aplicaciones, .NET Native ofrece estas ventajas:

- Tiempos de ejecución más rápidos para la mayoría de las aplicaciones y los escenarios.

- Tiempos de inicio más rápidos para la mayoría de las aplicaciones y los escenarios.

- Pocos costos de implementación y actualización.

- Uso optimizado de la memoria de la aplicación.

> [!IMPORTANT]
> En la gran mayoría de las aplicaciones y los escenarios, .NET Native ofrece tiempos de inicio significativamente más rápidos y un rendimiento superior en comparación con una aplicación compilada en IL o en una imagen de NGEN. Sin embargo, los resultados pueden variar. Para asegurarse de que la aplicación se ha beneficiado de las mejoras de rendimiento de .NET Native, debe comparar su rendimiento con el de la versión nativa de non-.NET de la aplicación. Para obtener más información, vea [información general sobre la sesión de rendimiento](https://docs.microsoft.com/visualstudio/profiling/performance-session-overview).

Pero .NET Native implica más que una compilación en código nativo. Transforma la manera en que se compilan y ejecutan las aplicaciones de .NET Framework. En particular:

- Durante la precompilación, las partes necesarias de .NET Framework se vinculan estáticamente en la aplicación. Esto permite que la aplicación se ejecute con bibliotecas locales de aplicación de .NET Framework y que el compilador realice un análisis global para ofrecer un gran rendimiento. Como resultado, las aplicaciones se inician sistemáticamente más rápido después de las actualizaciones de.NET Framework.

- El tiempo de ejecución de .NET Native está optimizado para la precompilación estática y, en la mayoría de los casos, ofrece un rendimiento superior. Al mismo tiempo, conserva las características de reflexión principales que los desarrolladores encuentran tan productivas.

- .NET Native usa el mismo back-end que C++ el compilador, que está optimizado para escenarios de precompilación estáticos.

.NET Native es capaz de aportar las ventajas de rendimiento C++ de a los desarrolladores de código administrado, ya que utiliza las mismas C++ herramientas o similares que se muestran en esta tabla.

||.NET Native|C++|
|-|----------------------------------------------------------------|-----------|
|Bibliotecas|.NET Framework + Windows en tiempo de ejecución|Win32 + Windows en tiempo de ejecución|
|Compilador|Compilador de optimización de UTC|Compilador de optimización de UTC|
|Implementado|Archivos binarios listos para ejecutarse|Archivos binarios listos para ejecutarse (ASM)|
|Tiempo de ejecución|MRT.dll (tiempo de ejecución de CLR mínimo)|CRT.dll (tiempo de ejecución de C)|

Para aplicaciones de Windows 10, cargue los archivos binarios de compilación de código con .NET Native en paquetes de aplicación (archivos .appx) en la Tienda Windows.

## <a name="in-this-section"></a>En esta sección

Para obtener más información sobre el desarrollo de aplicaciones con la compilación de código con .NET Native, vea estos temas:

- [Introducción con la compilación de código de .NET Native: Tutorial de experiencia del desarrollador](getting-started-with-net-native.md)

- [.NET Native y compilación:](net-native-and-compilation.md) Cómo .NET Native compila el proyecto en código nativo.

- [Reflection and .NET Native](reflection-and-net-native.md) (Reflexión y .NET Native)

  - [APIs That Rely on Reflection](apis-that-rely-on-reflection.md) (API basadas en Reflection)

  - [Referencia de la API de reflexión](net-native-reflection-api-reference.md)

  - [Runtime Directives (rd.xml) Configuration File Reference (Referencia del archivo de configuración de directivas en tiempo de ejecución (rd.xml))](runtime-directives-rd-xml-configuration-file-reference.md)

- [Serialización y metadatos](serialization-and-metadata.md)

- [Migrar la aplicación de la Tienda Windows a .NET Native](migrating-your-windows-store-app-to-net-native.md)

- [Solución de problemas generales de .NET Native](net-native-general-troubleshooting.md)
