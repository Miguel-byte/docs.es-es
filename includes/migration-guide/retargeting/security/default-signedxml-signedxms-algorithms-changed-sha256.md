---
ms.openlocfilehash: 12ba683655319e42368f9f2a6cf7bf70e1dbd77d
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67858995"
---
### <a name="default-signedxml-and-signedxms-algorithms-changed-to-sha256"></a>Los algoritmos SignedXML y SignedXMS predeterminados se han cambiado a SHA256

|   |   |
|---|---|
|Detalles|En .NET Framework 4.7 y versiones anteriores, SignedXML y SignedCMS usaban SHA1 de forma predeterminada para algunas operaciones. A partir de .NET Framework 4.7.1, SHA256 está habilitado de forma predeterminada para estas operaciones. Este cambio es necesario porque SHA1 ya no se considera seguro.|
|Sugerencia|Hay dos valores de modificador de contexto nuevos para controlar si se usa SHA1 (no seguro) o SHA256 de forma predeterminada:<ul><li>Switch.System.Security.Cryptography.Xml.UseInsecureHashAlgorithms</li><li>Switch.System.Security.Cryptography.Pkcs.UseInsecureHashAlgorithms</li></ul>Para las aplicaciones destinadas a .NET Framework 4.7.1 y versiones posteriores, si no se quiere usar SHA256, se puede restaurar el valor predeterminado a SHA1 si se agrega el conmutador de configuración siguiente a la sección [runtime](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) del archivo de configuración de la aplicación:<pre><code class="lang-xml">&lt;AppContextSwitchOverrides value=&quot;Switch.System.Security.Cryptography.Xml.UseInsecureHashAlgorithms=true;Switch.System.Security.Cryptography.Pkcs.UseInsecureHashAlgorithms=true&quot; /&gt;&#13;&#10;</code></pre>Para las aplicaciones destinadas a .NET Framework 4.7 y versiones posteriores, se puede permitir este cambio si se agrega el conmutador de configuración siguiente a la sección [runtime](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) del archivo de configuración de la aplicación:<pre><code class="lang-xml">&lt;AppContextSwitchOverrides value=&quot;Switch.System.Security.Cryptography.Xml.UseInsecureHashAlgorithms=false;Switch.System.Security.Cryptography.Pkcs.UseInsecureHashAlgorithms=false&quot; /&gt;&#13;&#10;</code></pre>|
|Ámbito|Secundaria|
|Versión|4.7.1|
|Tipo|Redestinación|
|API afectadas|<ul><li><xref:System.Security.Cryptography.Pkcs.CmsSigner?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.Xml.SignedXml?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.Xml.Reference?displayProperty=nameWithType></li></ul>|

