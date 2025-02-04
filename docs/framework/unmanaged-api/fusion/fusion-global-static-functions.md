---
title: Funciones estáticas globales de la fusión
ms.date: 03/30/2017
helpviewer_keywords:
- unmanaged global static functions [.NET Framework], fusion
- fusion global static functions [.NET Framework]
- global static functions [.NET Framework fusion]
ms.assetid: 229b2188-9168-4b44-a987-e1f515494688
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6a8f15bc862c0486311960f7567c49424859846e
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795314"
---
# <a name="fusion-global-static-functions"></a>Funciones estáticas globales de la fusión
En esta sección se describen las funciones estáticas globales no administradas que utiliza la API de fusión.  
  
## <a name="in-this-section"></a>En esta sección  
 [ClearDownloadCache (Función)](cleardownloadcache-function.md)  
 Borra la caché global de ensamblados de los ensamblados descargados.  
  
 [CompareAssemblyIdentity (Función)](compareassemblyidentity-function.md)  
 Compara dos identidades de ensamblado para determinar si son equivalentes.  
  
 [CreateApplicationContext (Función)](createapplicationcontext-function.md)  
 Solo para uso interno. (Esta función admite la infraestructura de .NET Framework y no está diseñada para utilizarse directamente desde el código).  
  
 [CreateAssemblyCache (Función)](createassemblycache-function.md)  
 Obtiene un puntero a una nueva instancia de [IAssemblyCache](iassemblycache-interface.md) que representa la caché global de ensamblados.  
  
 [CreateAssemblyEnum (Función)](createassemblyenum-function.md)  
 Obtiene un puntero a una instancia de [IAssemblyEnum](iassemblyenum-interface.md) que representa una lista de objetos que existen en el ensamblado especificado.  
  
 [CreateAssemblyNameObject (Función)](createassemblynameobject-function.md)  
 Obtiene un puntero a una instancia de [IAssemblyName](iassemblyname-interface.md) que representa la identidad única del ensamblado con el nombre especificado.  
  
 [CreateHistoryReader (Función)](createhistoryreader-function.md)  
 Crea un lector del historial para el archivo especificado.  
  
 [CreateInstallReferenceEnum (Función)](createinstallreferenceenum-function.md)  
 Obtiene un puntero a una instancia de [IInstallReferenceEnum (](iinstallreferenceenum-interface.md) que representa una lista de referencias de una aplicación al ensamblado especificado.  
  
 [GetAppIdAuthority (Función)](getappidauthority-function.md)  
 Obtiene un puntero a una instancia de [iappidauthority (](iappidauthority-interface.md) que administra las claves de las identidades y referencias de la aplicación.  
  
 [GetAssemblyIdentityFromFile (Función)](getassemblyidentityfromfile-function.md)  
 Obtiene un puntero a un `IUnknown` objeto con el especificado `IID` en el ensamblado en la ruta de acceso de archivo especificada.  
  
 [GetCachePath (Función)](getcachepath-function.md)  
 Obtiene la ruta de acceso al ensamblado almacenado en memoria caché, usando las marcas especificadas.  
  
 [GetHistoryFileDirectory (Función)](gethistoryfiledirectory-function.md)  
 Recupera la ruta de acceso del directorio del historial de la aplicación.  
  
 [GetIdentityAuthority (Función)](getidentityauthority-function.md)  
 Obtiene un puntero a una instancia de [iidentityauthority (](iidentityauthority-interface.md) que administra las claves de los objetos de código.  
  
 [IsFrameworkAssembly (Función)](isframeworkassembly-function.md)  
 Obtiene un valor que indica si el ensamblado especificado está administrado.  
  
 [NukeDownloadedCache (Función)](nukedownloadedcache-function.md)  
 Elimina la memoria caché de descarga de Common Language Runtime.  
  
 [PreBindAssemblyEx (Función)](prebindassemblyex-function.md)  
 Obtiene el nombre para mostrar de la Directiva posterior de un ensamblado.  
  
## <a name="related-sections"></a>Secciones relacionadas  
 [Interfaces de Fusion](fusion-interfaces.md)  
  
 [Enumeraciones de fusión](fusion-enumerations.md)  
  
 [Estructuras de fusión](fusion-structures.md)  
  
 [Caché global de ensamblados](../../app-domains/gac.md)
