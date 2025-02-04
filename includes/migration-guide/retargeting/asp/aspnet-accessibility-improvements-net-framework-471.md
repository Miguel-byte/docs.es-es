---
ms.openlocfilehash: a58ea1a16824cf4a1407221dfb0123efa79e48f9
ms.sourcegitcommit: 4d8efe00f2e5ab42e598aff298d13b8c052d9593
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68235681"
---
### <a name="aspnet-accessibility-improvements-in-net-framework-471"></a>Mejoras de accesibilidad de ASP.NET en .NET Framework 4.7.1

|   |   |
|---|---|
|Detalles|A partir de .NET Framework 4.7.1, ASP.NET ha mejorado el funcionamiento de los controles web de ASP.NET con la tecnología de accesibilidad en Visual Studio para una mejor compatibilidad con los clientes de ASP.NET.  Entre otros, se incluyen los cambios siguientes:<ul><li>Cambios para implementar patrones de accesibilidad de interfaz de usuario que faltan en los controles, como el cuadro de diálogo Agregar campo en el Asistente para vistas de detalles o el cuadro de diálogo Configurar ListView del Asistente de ListView.</li><li>Cambios para mejorar la presentación en el modo Contraste alto, como el Editor de campos del elemento de paginación de datos.</li><li>Cambios para mejorar las experiencias de navegación del teclado para los controles, como el cuadro de diálogo Campos del Asistente para editar campos del elemento de paginación del control DataPager, el cuadro de diálogo Configurar ObjectContext o el cuadro de diálogo Configurar selección de datos del Asistente para configurar origen de datos.</li></ul>|
|Sugerencia|<strong>Cómo participar o no en estos cambios</strong> Para que el diseñador de Visual Studio se beneficie de estos cambios, se debe ejecutar en .NET Framework 4.7.1 o una versión posterior. La aplicación web se puede beneficiar de estos cambios de cualquiera de las maneras siguientes:<ul><li>Instalar Visual Studio 2017 15.3 o una versión posterior, que es compatible con las nuevas características de accesibilidad con el modificador siguiente de AppContext de forma predeterminada.</li><li>No participar en los comportamientos de accesibilidad heredados agregando el modificador de AppContext <code>Switch.UseLegacyAccessibilityFeatures</code> a la sección <code>&lt;runtime&gt;</code> del archivo devenv.exe.config y estableciéndolo en <code>false</code>, como se muestra en el ejemplo siguiente.</li></ul><pre><code class="lang-xml">&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;&#13;&#10;&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;...&#13;&#10;&lt;!-- AppContextSwitchOverrides value attribute is in the form of &#39;key1=true/false;key2=true/false&#39;  --&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.UseLegacyAccessibilityFeatures=false&quot; /&gt;&#13;&#10;...&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>En las aplicaciones destinadas a .NET Framework 4.7.1 o una versión posterior, y en las que se quiere conservar el comportamiento de accesibilidad heredado, se puede participar en el uso de las características de accesibilidad heredadas si se establece explícitamente este modificador de AppContext en <code>true</code>.|
|Ámbito|Secundaria|
|Versión|4.7.1|
|Tipo|Redestinación|
