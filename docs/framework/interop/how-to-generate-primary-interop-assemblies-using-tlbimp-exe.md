---
title: Procedimiento para generar ensamblados de interoperabilidad primarios mediante Tlbimp.exe
ms.date: 03/30/2017
helpviewer_keywords:
- primary interop assemblies, generating
- Tlbimp.exe
- Type Library Importer
ms.assetid: 5419011c-6e57-40f6-8c65-386db8f7a651
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ac60fa96b7c9ce6991f89e8c6a37ff5da4a34a50
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71051778"
---
# <a name="how-to-generate-primary-interop-assemblies-using-tlbimpexe"></a>Procedimiento para generar ensamblados de interoperabilidad primarios mediante Tlbimp.exe

Hay dos maneras de generar un ensamblado de interoperabilidad primario:

- Mediante el [importador de la biblioteca de tipos (Tlbimp.exe)](../tools/tlbimp-exe-type-library-importer.md) proporcionado por Windows SDK.

  La manera más sencilla de generar ensamblados de interoperabilidad primarios es usar el [importador de la biblioteca de tipos (Tlbimp.exe)](../tools/tlbimp-exe-type-library-importer.md). Tlbimp.exe ofrece las siguientes medidas de protección:

  - Busca otros ensamblados de interoperabilidad primarios registrados antes de crear nuevos ensamblados de interoperabilidad para las referencias de biblioteca de tipos anidadas.

  - No emite el ensamblado de interoperabilidad primario si no se especifica el contenedor o el nombre de archivo para asignar un nombre seguro al ensamblado de interoperabilidad primario.

  - No emite un ensamblado de interoperabilidad primario si se omiten las referencias a los ensamblados dependientes.

  - No emite un ensamblado de interoperabilidad primario si se agregan referencias a ensamblados dependientes que no son ensamblados de interoperabilidad primarios.

- Creando ensamblados de interoperabilidad primarios manualmente en el código fuente usando un lenguaje compatible con Common Language Specification (CLS), como C#. Este enfoque es útil cuando no hay una biblioteca de tipos disponible.

Es necesario disponer de un par de claves criptográficas para firmar un ensamblado con un nombre seguro. Para más información, vea [Crear un par de claves](../../standard/assembly/create-public-private-key-pair.md).

### <a name="to-generate-a-primary-interop-assembly-using-tlbimpexe"></a>Para generar ensamblados de interoperabilidad primarios mediante Tlbimp.exe

1. En el símbolo del sistema, escriba:

    **tlbimp** *archivo_tlb*  **/primary /keyfile:** *nombre_de_archivo* **/out:** *nombre_de_ensamblado*

    En este comando, *archivo_tlb* es el archivo que contiene la biblioteca de tipos COM, *nombre_de_archivo* es el nombre del contenedor o archivo que contiene el par de claves y *nombre_de_ensamblado* es el nombre del ensamblado que se va a firmar con un nombre seguro.

Los ensamblados de interoperabilidad primarios solo pueden hacer referencia a otros ensamblados de interoperabilidad primarios. Si el ensamblado hace referencia a tipos de una biblioteca de tipos COM de terceros, debe obtener un ensamblado de interoperabilidad primario desde el publicador antes de poder generar el ensamblado de interoperabilidad primario. Si usted es el publicador, debe generar un ensamblado de interoperabilidad primario para la biblioteca de tipos dependiente antes de generar el ensamblado de interoperabilidad primario que hace la referencia.

Si un ensamblado de interoperabilidad primario dependiente tiene un número de versión distinto del de la biblioteca de tipos original, no se reconoce cuando se instala en el directorio actual. Debe registrar el ensamblado de interoperabilidad primario dependiente en el Registro de Windows o usar la opción **/reference** para asegurarse de que Tlbimp.exe encuentre el archivo DLL dependiente.

También puede encapsular varias versiones de una biblioteca de tipos. Para obtener instrucciones, vea [Cómo: Incluir varias versiones de bibliotecas de tipos](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/1565h6hc(v=vs.100)).

## <a name="example"></a>Ejemplo

En el siguiente ejemplo se importa la biblioteca de tipos COM `LibUtil.tlb` y se firma el ensamblado `LibUtil.dll` con un nombre seguro usando el archivo de clave `CompanyA.snk`. Si se omite un nombre de espacio de nombres específico, este ejemplo genera el espacio de nombres predeterminado `LibUtil`.

```console
tlbimp LibUtil.tlb /primary /keyfile:CompanyA.snk /out:LibUtil.dll
```

Para lograr un nombre más descriptivo (siguiendo las directrices de nomenclatura *NombreProveedor*.*NombreBiblioteca*), en el ejemplo siguiente se invalida el nombre predeterminado del archivo de ensamblado y el nombre de espacio de nombres.

```console
tlbimp LibUtil.tlb /primary /keyfile:CompanyA.snk /namespace:CompanyA.LibUtil /out:CompanyA.LibUtil.dll
```

En el siguiente ejemplo se importa `MyLib.tlb`, que hace referencia al ensamblado `CompanyA.LibUtil.dll`, y se firma el ensamblado `CompanyB.MyLib.dll` con un nombre seguro usando el archivo de clave `CompanyB.snk`. El espacio de nombres `CompanyB.MyLib` invalida el nombre de espacio de nombres predeterminado.

```console
tlbimp MyLib.tlb /primary /keyfile:CompanyB.snk /namespace:CompanyB.MyLib /reference:CompanyA.LibUtil.dll /out:CompanyB.MyLib.dll
```

## <a name="see-also"></a>Vea también

- [Cómo: Registrar ensamblados de interoperabilidad primarios](how-to-register-primary-interop-assemblies.md)
