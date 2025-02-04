---
title: Introducción F# a las herramientas de línea de comandos
description: Obtenga información sobre cómo crear una solución sencilla de varios proyectos F# en el uso de la CLI de .net Core en cualquier sistema operativo (Windows, MacOS o Linux).
ms.date: 03/26/2018
ms.openlocfilehash: f9177e653273e5a2191407c4fb22343ded11fece
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117930"
---
# <a name="get-started-with-f-with-the-net-core-cli"></a>Comience con F# el CLI de .net Core

En este artículo se explica cómo puede empezar a F# trabajar con en cualquier sistema operativo (Windows, MacOS o Linux) con el CLI de .net Core. Pasa por la creación de una solución de varios proyectos con una biblioteca de clases a la que llama una aplicación de consola.

## <a name="prerequisites"></a>Requisitos previos

Para empezar, debe instalar la [SDK de .net Core](https://dotnet.microsoft.com/download)más reciente.

En este artículo se supone que sabe cómo usar una línea de comandos y tener un editor de texto preferido. Si aún no lo usa, [Visual Studio Code](get-started-vscode.md) es una excelente opción como editor de texto para F#.

## <a name="build-a-simple-multi-project-solution"></a>Compilar una solución sencilla de varios proyectos

Abra un símbolo del sistema o terminal y use el comando [dotnet New](../../core/tools/dotnet-new.md) para crear un nuevo archivo `FSNetCore`de solución denominado:

```dotnetcli
dotnet new sln -o FSNetCore
```

Después de ejecutar el comando anterior, se genera la siguiente estructura de directorios:

```console
FSNetCore
    ├── FSNetCore.sln
```

### <a name="write-a-class-library"></a>Escribir una biblioteca de clases

Cambie los directorios a *FSNetCore*.

Use el `dotnet new` comando, cree un proyecto de biblioteca de clases en la carpeta **src** denominada Library.

```dotnetcli
dotnet new classlib -lang F# -o src/Library
```

Después de ejecutar el comando anterior, se genera la siguiente estructura de directorios:

```console
└── FSNetCore
    ├── FSNetCore.sln
    └── src
        └── Library
            ├── Library.fs
            └── Library.fsproj
```

Reemplace el contenido de `Library.fs` por el código siguiente:

```fsharp
module Library

open Newtonsoft.Json

let getJsonNetJson value =
    sprintf "I used to be %s but now I'm %s thanks to JSON.NET!" value (JsonConvert.SerializeObject(value))
```

Agregue el paquete NuGet Newtonsoft. JSON al proyecto de biblioteca.

```dotnetcli
dotnet add src/Library/Library.fsproj package Newtonsoft.Json
```

Agregue el `Library` proyecto a la `FSNetCore` solución mediante el comando [dotnet sln Add](../../core/tools/dotnet-sln.md) :

```dotnetcli
dotnet sln add src/Library/Library.fsproj
```

Ejecute `dotnet build` para compilar el proyecto. Las dependencias no resueltas se restaurarán al compilar.

### <a name="write-a-console-application-that-consumes-the-class-library"></a>Escribir una aplicación de consola que consuma la biblioteca de clases

Use el `dotnet new` comando para crear una aplicación de consola en la carpeta **src** denominada app.

```dotnetcli
dotnet new console -lang F# -o src/App
```

Después de ejecutar el comando anterior, se genera la siguiente estructura de directorios:

```console
└── FSNetCore
    ├── FSNetCore.sln
    └── src
        ├── App
        │   ├── App.fsproj
        │   ├── Program.fs
        └── Library
            ├── Library.fs
            └── Library.fsproj
```

Reemplace el contenido del `Program.fs` archivo por el código siguiente:

```fsharp
open System
open Library

[<EntryPoint>]
let main argv =
    printfn "Nice command-line arguments! Here's what JSON.NET has to say about them:"

    argv
    |> Array.map getJsonNetJson
    |> Array.iter (printfn "%s")

    0 // return an integer exit code
```

Agregue una referencia al `Library` proyecto mediante [dotnet Add Reference](../../core/tools/dotnet-add-reference.md).

```dotnetcli
dotnet add src/App/App.fsproj reference src/Library/Library.fsproj
```

Agregue el `App` proyecto a la `FSNetCore` solución mediante el `dotnet sln add` comando:

```dotnetcli
dotnet sln add src/App/App.fsproj
```

Restaure las dependencias `dotnet restore` de NuGet y `dotnet build` ejecute para compilar el proyecto.

Cambie el directorio al `src/App` proyecto de consola y ejecute el proyecto `Hello World` pasando como argumentos:

```console
cd src/App
dotnet run Hello World
```

Debería ver los resultados siguientes:

```console
Nice command-line arguments! Here's what JSON.NET has to say about them:

I used to be Hello but now I'm ""Hello"" thanks to JSON.NET!
I used to be World but now I'm ""World"" thanks to JSON.NET!
```

## <a name="next-steps"></a>Pasos siguientes

A continuación, consulte el [paseo F# ](../tour.md) por para obtener más información sobre F# las distintas características.
