---
title: Especificar un juego de caracteres
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- platform invoke, attribute fields
- attribute fields in platform invoke, CharSet
- CharSet field
ms.assetid: a8347eb1-295f-46b9-8a78-63331f9ecc50
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9ee68d0da3b7f23d4de0192da076ef6f71d6d222
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71051636"
---
# <a name="specifying-a-character-set"></a>Especificar un juego de caracteres
El campo <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=nameWithType> controla la serialización de cadenas y determina cómo la invocación de plataforma busca nombres de función en un archivo DLL. En este tema se describen ambos comportamientos.  
  
 Algunas API exportan dos versiones de las funciones que toman argumentos de cadena: la versión estrecha (ANSI) y la versión ancha (Unicode). La API de Windows, por ejemplo, incluye los siguientes nombres de punto de entrada para la función **MessageBox**:  
  
- **MessageBoxA**  
  
     Proporciona el formato ANSI de caracteres de 1 byte, que se distingue por una "A" anexada al nombre del punto de entrada. Las llamadas a **MessageBoxA** siempre serializan las cadenas en formato ANSI.  
  
- **MessageBoxW**  
  
     Proporciona el formato Unicode de caracteres de 2 bytes, que se distingue por una "W" anexada al nombre del punto de entrada. Las llamadas a **MessageBoxW** siempre serializan las cadenas en formato Unicode.  
  
## <a name="string-marshaling-and-name-matching"></a>Serialización de cadenas y coincidencia de nombres  
 El campo `CharSet` acepta los valores siguientes:  
  
 <xref:System.Runtime.InteropServices.CharSet.Ansi> (valor predeterminado)  
  
- Serialización de cadenas  
  
     La invocación de plataforma serializa las cadenas del formato administrado (Unicode) al formato ANSI.  
  
- Coincidencia de nombres  
  
     Cuando el campo <xref:System.Runtime.InteropServices.DllImportAttribute.ExactSpelling?displayProperty=nameWithType> es `true`, como sucede de forma predeterminada en Visual Basic, la invocación de plataforma solo busca el nombre que se especifique. Por ejemplo, si especifica **MessageBox**, la invocación de plataforma busca **MessageBox** y se produce un error si no encuentra el término exacto.  
  
     Si el campo `ExactSpelling` es `false`, como sucede de forma predeterminada en C++ y C#, la invocación de plataforma busca primero el alias no alterado (**MessageBox**) y, luego, el nombre alterado (**MessageBoxA**) en el caso de que no se encuentre el alias no alterado. Tenga en cuenta que el comportamiento de la coincidencia de nombres en formato ANSI difiere del comportamiento de la coincidencia de nombres en formato Unicode.  
  
 <xref:System.Runtime.InteropServices.CharSet.Unicode>  
  
- Serialización de cadenas  
  
     La invocación de plataforma copia las cadenas del formato administrado (Unicode) al formato Unicode.  
  
- Coincidencia de nombres  
  
     Cuando el campo `ExactSpelling` es `true`, como sucede de forma predeterminada en Visual Basic, la invocación de plataforma solo busca el nombre que se especifique. Por ejemplo, si especifica **MessageBox**, la invocación de plataforma busca **MessageBox** y se produce un error si no encuentra el término exacto.  
  
     Si el campo `ExactSpelling` es `false`, como sucede de forma predeterminada en C++ y C#, la invocación de plataforma busca primero el alias alterado (**MessageBoxW**) y, luego, el nombre no alterado (**MessageBox**) en el caso de que no se encuentre el alias alterado. Tenga en cuenta que el comportamiento de la coincidencia de nombres en formato Unicode difiere del comportamiento de la coincidencia de nombres en formato ANSI.  
  
 <xref:System.Runtime.InteropServices.CharSet.Auto>  
  
- La invocación de plataforma elige entre los formatos ANSI y Unicode en tiempo de ejecución en función de la plataforma de destino.  
  
## <a name="specifying-a-character-set-in-visual-basic"></a>Especificar un juego de caracteres en Visual Basic  
 En el ejemplo siguiente se declara la función **MessageBox** tres veces, cada una de ellas con un comportamiento de juego de caracteres diferente. Para especificar un comportamiento de juego de caracteres en Visual Basic, agregue la palabra clave **Ansi**, **Unicode** o **Auto** a la instrucción de declaración.  
  
 Si omite la palabra clave del juego de caracteres, tal y como se hace en la primera instrucción de la declaración, el campo <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=nameWithType> establece como valor predeterminado el juego de caracteres ANSI. En la segunda y tercera instrucciones del ejemplo se especifica explícitamente un juego de caracteres con una palabra clave.  
  
```vb
Friend Class NativeMethods
    Friend Declare Function MessageBoxA Lib "user32.dll" (
        ByVal hWnd As IntPtr,
        ByVal lpText As String,
        ByVal lpCaption As String,
        ByVal uType As UInteger) As Integer

    Friend Declare Unicode Function MessageBoxW Lib "user32.dll" (
        ByVal hWnd As IntPtr,
        ByVal lpText As String,
        ByVal lpCaption As String,
        ByVal uType As UInteger) As Integer

    Friend Declare Auto Function MessageBox Lib "user32.dll" (
        ByVal hWnd As IntPtr,
        ByVal lpText As String,
        ByVal lpCaption As String,
        ByVal uType As UInteger) As Integer
End Class
```
  
## <a name="specifying-a-character-set-in-c-and-c"></a>Especificar un juego de caracteres en C# y C++  
 El campo <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=nameWithType> identifica el juego de caracteres subyacente como ANSI o Unicode. El juego de caracteres controla cómo se deben serializar los argumentos de cadena en un método. Use uno de los formatos siguientes para indicar el juego de caracteres:  
  
```csharp
[DllImport("DllName", CharSet = CharSet.Ansi)]
[DllImport("DllName", CharSet = CharSet.Unicode)]
[DllImport("DllName", CharSet = CharSet.Auto)]
```
  
```cpp
[DllImport("DllName", CharSet = CharSet::Ansi)]
[DllImport("DllName", CharSet = CharSet::Unicode)]
[DllImport("DllName", CharSet = CharSet::Auto)]
```
  
 En el ejemplo siguiente se muestran tres definiciones administradas de la función **MessageBox** con atributos para especificar un juego de caracteres. En la primera definición, debido a su omisión, el campo `CharSet` establece como valor predeterminado el juego de caracteres ANSI.  
  
```csharp  
using System;
using System.Runtime.InteropServices;

internal static class NativeMethods
{
    [DllImport("user32.dll")]
    internal static extern int MessageBoxA(
        IntPtr hWnd, string lpText, string lpCaption, uint uType);

    [DllImport("user32.dll", CharSet = CharSet.Unicode)]
    internal static extern int MessageBoxW(
        IntPtr hWnd, string lpText, string lpCaption, uint uType);

    [DllImport("user32.dll", CharSet = CharSet.Auto)]
    internal static extern int MessageBox(
        IntPtr hWnd, string lpText, string lpCaption, uint uType);
}
```  
  
```cpp
typedef void* HWND;

// Can use MessageBox or MessageBoxA.
[DllImport("user32")]
extern "C" int MessageBox(
    HWND hWnd, String* lpText, String* lpCaption, unsigned int uType);

// Can use MessageBox or MessageBoxW.
[DllImport("user32", CharSet = CharSet::Unicode)]
extern "C" int MessageBoxW(
    HWND hWnd, String* lpText, String* lpCaption, unsigned int uType);

// Must use MessageBox.
[DllImport("user32", CharSet = CharSet::Auto)]
extern "C" int MessageBox(
    HWND hWnd, String* lpText, String* lpCaption, unsigned int uType);
```
  
## <a name="see-also"></a>Vea también

- <xref:System.Runtime.InteropServices.DllImportAttribute>
- [Crear prototipos en código administrado](creating-prototypes-in-managed-code.md)
- [Ejemplos de invocación de plataforma](platform-invoke-examples.md)
- [Serialización de datos con invocación de plataforma](marshaling-data-with-platform-invoke.md)
