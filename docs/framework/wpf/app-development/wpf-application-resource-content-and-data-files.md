---
title: Archivos de recursos, contenido y datos de aplicaciones de WPF
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WPF application [WPF], files
- loose resources [WPF]
- content files [WPF]
- Site of Origin files [WPF]
- resource files [WPF]
- remote files [WPF]
- embedded resources [WPF]
- files [WPF]
- referencing application files [WPF]
- application development [WPF], files
- application management [WPF]
ms.assetid: 7ad2943b-3961-41d3-8fc6-1582d43f5d99
ms.openlocfilehash: 57eae5067a72777db2c19331029b6df679a9fdce
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69956187"
---
# <a name="wpf-application-resource-content-and-data-files"></a>Archivos de recursos, contenido y datos de aplicaciones de WPF
[!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)]las aplicaciones a menudo dependen de archivos que contienen datos no ejecutables, como [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]imágenes, vídeo y audio. Windows Presentation Foundation (WPF) ofrece compatibilidad especial para configurar, identificar y usar estos tipos de archivos de datos, que se denominan archivos de datos de la aplicación. Esta compatibilidad gira en torno a un conjunto específico de tipos de archivo de datos de aplicación, entre los que se incluyen:  
  
- **Archivos de recursos**: Archivos de datos que se compilan en un ensamblado [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] de biblioteca o ejecutable.  
  
- **Archivos de contenido**: Archivos de datos independientes que tienen una asociación explícita con un [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] ensamblado ejecutable.  
  
- **Archivos de sitio de origen**: Archivos de datos independientes que no tienen ninguna asociación con un [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] ensamblado ejecutable.  
  
 Una diferencia importante entre estos tres tipos de archivos es que tanto los archivos de recursos como los archivos de contenido se conocen en el momento de la compilación; un ensamblado tiene un conocimiento explícito de ellos. En el caso de los archivos de sitio de origen, sin embargo, es posible que un ensamblado no tenga ningún conocimiento de [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] ellos, o un conocimiento implícito a través de una referencia de paquete; el caso de este último, no hay ninguna garantía de que el archivo del sitio de origen al que se hace referencia realmente exista.  
  
 Para hacer referencia a los archivos de datos de la aplicación, Windows Presentation Foundation [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] (WPF) usa el esquema Pack, que se describe en detalle en [pack uri en WPF](pack-uris-in-wpf.md)).  
  
 En este tema se describe cómo configurar y usar archivos de datos de aplicaciones.  

<a name="Resource_Files"></a>   
## <a name="resource-files"></a>Archivos de recursos  
 Si un archivo de datos de la aplicación debe estar siempre disponible para una aplicación, la única forma de garantizar la disponibilidad es compilarlo en el ensamblado ejecutable principal de una aplicación o en uno de sus ensamblados referenciados. Este tipo de archivo de datos de la aplicación se conoce como *archivo de recursos*.  
  
 Los archivos de recursos se deben usar cuando:  
  
- No es necesario actualizar el contenido del archivo de recursos después de que se compila en un ensamblado.  
  
- Desea simplificar la complejidad de la distribución de una aplicación mediante la reducción del número de dependencias de los archivos.  
  
- El archivo de datos de la aplicación debe ser localizable (consulte [información general sobre la globalización y la localización de WPF](../advanced/wpf-globalization-and-localization-overview.md)).  
  
> [!NOTE]
> Los archivos de recursos que se describen en esta sección son diferentes de los archivos de recursos descritos en [recursos XAML](../advanced/xaml-resources.md) y distintos de los recursos incrustados o vinculados que se describen en [Administración de recursos de aplicación (.net)](/visualstudio/ide/managing-application-resources-dotnet).  
  
### <a name="configuring-resource-files"></a>Configuración de archivos de recursos  
 En [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], un archivo de recursos es un archivo que se incluye en un proyecto de Microsoft Build Engine (MSBuild) `Resource` como un elemento.  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <ItemGroup>  
    <Resource Include="ResourceFile.xaml" />  
  </ItemGroup>  
  ...  
</Project>  
```  
  
> [!NOTE]
> En [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)], se crea un archivo de recursos agregando un archivo a un proyecto y estableciendo `Build Action` su `Resource`en.  
  
 Cuando se compila el proyecto, MSBuild compila el recurso en el ensamblado.  
  
### <a name="using-resource-files"></a>Uso de archivos de recursos  
 Para cargar un archivo de recursos, puede llamar al <xref:System.Windows.Application.GetResourceStream%2A> método de la <xref:System.Windows.Application> clase, pasando un pack [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] que identifique el archivo de recursos deseado. <xref:System.Windows.Application.GetResourceStream%2A>Devuelve un <xref:System.Windows.Resources.StreamResourceInfo> objeto, que expone el archivo de recursos <xref:System.IO.Stream> como y describe su tipo de contenido.  
  
 Como ejemplo, el código <xref:System.Windows.Application.GetResourceStream%2A> siguiente muestra cómo usar para cargar un <xref:System.Windows.Controls.Page> archivo de recursos y establecerlo como el contenido de un <xref:System.Windows.Controls.Frame> (`pageFrame`):  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadAPageResourceFileManuallyCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.cs#loadapageresourcefilemanuallycode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadAPageResourceFileManuallyCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.vb#loadapageresourcefilemanuallycode)]  
  
 Aunque llamar <xref:System.Windows.Application.GetResourceStream%2A> a proporciona acceso <xref:System.IO.Stream>a, debe realizar el trabajo adicional de convertirlo al tipo de la propiedad con la que se va a establecer. En su lugar, puede dejar [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] que se ocupe de abrir y convertir <xref:System.IO.Stream> mediante la carga de un archivo de recursos directamente en la propiedad de un tipo mediante el código.  
  
 En el ejemplo siguiente se muestra cómo cargar <xref:System.Windows.Controls.Page> un directamente en <xref:System.Windows.Controls.Frame> un`pageFrame`() mediante código.  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadPageResourceFileFromCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.cs#loadpageresourcefilefromcode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadPageResourceFileFromCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.vb#loadpageresourcefilefromcode)]  
  
 El ejemplo siguiente es el equivalente de marcación del ejemplo anterior.  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#LoadPageResourceFileFromXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml#loadpageresourcefilefromxaml)]  
  
### <a name="application-code-files-as-resource-files"></a>Archivos de código de aplicación como archivos de recursos  
 Se puede hacer referencia [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] A un conjunto especial de archivos de código de [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)]aplicación mediante Pack, como ventanas, páginas, documentos dinámicos y diccionarios de recursos. Por ejemplo, puede establecer la <xref:System.Windows.Application.StartupUri%2A?displayProperty=nameWithType> propiedad con un paquete [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] que haga referencia a la ventana o la página que desea cargar cuando se inicia una aplicación.  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#SetApplicationStartupURI](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/App.xaml#setapplicationstartupuri)]  
  
 Puede hacerlo cuando un archivo XAML se incluye en un proyecto de MSBuild como un `Page` elemento.  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <ItemGroup>  
    <Page Include="MainWindow.xaml" />  
  </ItemGroup>  
  ...  
</Project>  
```  
  
> [!NOTE]
> En [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)], se agrega un nuevo <xref:System.Windows.Window>, <xref:System.Windows.Navigation.NavigationWindow> <xref:System.Windows.Controls.Page> `Build Action` ,, `Page`o <xref:System.Windows.ResourceDictionary> a un proyecto de, para que el archivo de marcado tenga como valor predeterminado. <xref:System.Windows.Documents.FlowDocument>  
  
 Cuando se compila un `Page` proyecto con elementos, los [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] elementos se convierten al formato binario y se compilan en el ensamblado asociado. Por consiguiente, estos archivos se pueden utilizar de la misma forma que los archivos de recursos típicos.  
  
> [!NOTE]
> Si un [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] archivo está configurado como un `Resource` elemento y no tiene un archivo de código subyacente, el sin formato [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] se compila en un ensamblado en lugar de una versión binaria de [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]la sin formato.  
  
<a name="Content_Files"></a>   
## <a name="content-files"></a>Archivos de contenido  
 Un *archivo de contenido* se distribuye como un archivo suelto junto con un ensamblado ejecutable. Aunque no se compilan en un ensamblado, los ensamblados se compilan con metadatos que establecen una asociación con cada archivo de contenido.  
  
 Los archivos de contenido se deben usar cuando la aplicación requiere un conjunto específico de archivos de datos de aplicación que desee poder actualizar sin volver a compilar el ensamblado que los consume.  
  
### <a name="configuring-content-files"></a>Configuración de archivos de contenido  
 Para agregar un archivo de contenido a un proyecto de, un archivo de datos de la aplicación `Content` debe incluirse como un elemento. Además, dado que un archivo de contenido no se compila directamente en el ensamblado, debe establecer el `CopyToOutputDirectory` elemento de metadatos de MSBuild para especificar que el archivo de contenido se copia en una ubicación relativa al ensamblado compilado. Si desea que el recurso se copie en la carpeta de resultados de compilación cada vez que se compila un proyecto, establezca `CopyToOutputDirectory` el elemento de metadatos con el `Always` valor. De lo contrario, puede asegurarse de que solo la versión más reciente del recurso se copia en la carpeta de salida de `PreserveNewest` la compilación mediante el valor.  
  
 A continuación muestra un archivo que se configura como un archivo de contenido que se copia en la carpeta de salida de compilación solo cuando se agrega al proyecto una nueva versión del recurso.  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <ItemGroup>  
    <Content Include="ContentFile.xaml">  
      <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>  
    </Content>  
  </ItemGroup>  
  ...  
</Project>  
```  
  
> [!NOTE]
> En [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)], se crea un archivo de contenido agregando un archivo a un proyecto y estableciendo `Build Action` su `Content` `Copy to Output Directory` en y se establece en `Copy always` (igual que `Always`) y `Copy if newer` (igual que `PreserveNewest`).  
  
 Cuando se compila el proyecto, se <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> compila un atributo en los metadatos del ensamblado para cada archivo de contenido.  
  
 `[assembly: AssemblyAssociatedContentFile("ContentFile.xaml")]`  
  
 El valor de <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> implica la ruta de acceso al archivo de contenido con respecto a su posición en el proyecto. Por ejemplo, si un archivo de contenido se encuentra en una subcarpeta del proyecto, la información adicional de la ruta de acceso <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> se incorporará en el valor.  
  
 `[assembly: AssemblyAssociatedContentFile("Resources/ContentFile.xaml")]`  
  
 El <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> valor también es el valor de la ruta de acceso al archivo de contenido en la carpeta de salida de la compilación.  
  
### <a name="using-content-files"></a>Uso de archivos de contenido  
 Para cargar un archivo de contenido, puede llamar al <xref:System.Windows.Application.GetContentStream%2A> método de la <xref:System.Windows.Application> clase, pasando un pack [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] que identifique el archivo de contenido deseado. <xref:System.Windows.Application.GetContentStream%2A>Devuelve un <xref:System.Windows.Resources.StreamResourceInfo> objeto, que expone el archivo de contenido <xref:System.IO.Stream> como y describe su tipo de contenido.  
  
 Como ejemplo, el código <xref:System.Windows.Application.GetContentStream%2A> siguiente muestra cómo utilizar para cargar un <xref:System.Windows.Controls.Page> archivo de contenido y establecerlo como el contenido de un <xref:System.Windows.Controls.Frame> (`pageFrame`).  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadAPageContentFileManuallyCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.cs#loadapagecontentfilemanuallycode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadAPageContentFileManuallyCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.vb#loadapagecontentfilemanuallycode)]  
  
 Aunque llamar <xref:System.Windows.Application.GetContentStream%2A> a proporciona acceso <xref:System.IO.Stream>a, debe realizar el trabajo adicional de convertirlo al tipo de la propiedad con la que se va a establecer. En su lugar, puede dejar [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] que se ocupe de abrir y convertir <xref:System.IO.Stream> mediante la carga de un archivo de recursos directamente en la propiedad de un tipo mediante el código.  
  
 En el ejemplo siguiente se muestra cómo cargar <xref:System.Windows.Controls.Page> un directamente en <xref:System.Windows.Controls.Frame> un`pageFrame`() mediante código.  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadPageContentFileFromCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.cs#loadpagecontentfilefromcode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadPageContentFileFromCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.vb#loadpagecontentfilefromcode)]  
  
 El ejemplo siguiente es el equivalente de marcación del ejemplo anterior.  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#LoadPageContentFileFromXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml#loadpagecontentfilefromxaml)]  
  
<a name="Site_of_Origin_Files"></a>   
## <a name="site-of-origin-files"></a>Sitio de archivos de origen  
 Los archivos de recursos tienen una relación explícita con los ensamblados a los que se distribuyen, <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute>tal y como se define en. Sin embargo, hay veces en las que puede desear establecer una relación implícita o inexistente entre un ensamblado y un archivo de datos de aplicación, incluyendo cuándo:  
  
- No existe un archivo en tiempo de compilación.  
  
- No sabe qué archivos requerirá el ensamblado hasta el tiempo de ejecución.  
  
- Desea poder actualizar los archivos sin volver a compilar el ensamblado al que están asociados.  
  
- La aplicación utiliza archivos de datos grandes, como audio y vídeo, y solo desea que los usuarios los descarguen si eligen hacerlo.  
  
 Es posible cargar estos tipos de archivos mediante esquemas tradicionales [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] , como los esquemas File:///y http://.  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#AbsolutePackUriFileHttpReferenceXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/AbsolutePackUriPage.xaml#absolutepackurifilehttpreferencexaml)]  
  
 Sin embargo, los esquemas file:/// y http:// requieren que la aplicación tenga plena confianza. Si la aplicación es un [!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)] que se inició desde Internet o una intranet y solicita solo el conjunto de permisos que se permiten para las aplicaciones iniciadas desde esas ubicaciones, los archivos sueltos solo se pueden cargar desde el sitio de origen de la aplicación ( Ubicación de inicio). Estos archivos se denominan archivos *de sitio de origen* .  
  
 Los archivos del sitio de origen son la única opción para las aplicaciones de confianza parcial, aunque no se limitan a ese tipo de aplicaciones. Es posible que las aplicaciones de plena confianza aún necesiten cargar archivos de datos de aplicación que desconocen en tiempo de compilación; mientras que las aplicaciones de plena confianza pueden utilizar file:///, es probable que los archivos de datos de la aplicación se instalarán en la misma carpeta que el ensamblado de la aplicación, o en una subcarpeta de él. En este caso, es más sencillo usar la referencia del sitio de origen que file:///, ya que el uso de file:/// requiere que se determine la ruta de acceso completa del archivo.  
  
> [!NOTE]
> Los archivos de sitio de origen no se almacenan [!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)] en caché con un en un equipo cliente, mientras que los archivos de contenido son. Por consiguiente, sólo se descargan cuando se solicita específicamente. Si una [!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)] aplicación tiene archivos multimedia de gran tamaño, configurarlos como archivos de sitio de origen significa que el inicio de la aplicación inicial es mucho más rápido y los archivos solo se descargan a petición.  
  
### <a name="configuring-site-of-origin-files"></a>Configuración de archivos de sitio de origen  
 Si los archivos de sitio de origen son inexistentes o desconocidos en tiempo de compilación, debe usar mecanismos de implementación tradicionales para asegurarse de que los archivos necesarios están disponibles en tiempo de `XCopy` ejecución, incluido el uso del programa de línea de comandos o el [!INCLUDE[TLA#tla_wininstall](../../../../includes/tlasharptla-wininstall-md.md)].  
  
 Si sabe en tiempo de compilación los archivos que desea que se encuentren en el sitio de origen, pero desea evitar una dependencia explícita, puede agregar esos archivos a un proyecto de MSBuild como `None` elemento. Al igual que con los archivos de contenido, debe establecer `CopyToOutputDirectory` el atributo de MSBuild para especificar que el archivo de sitio de origen se copia en una ubicación relativa al ensamblado compilado, especificando el `Always` valor o el `PreserveNewest` valor.  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <None Include="PageSiteOfOriginFile.xaml">  
    <CopyToOutputDirectory>Always</CopyToOutputDirectory>  
  </None>  
  ...  
</Project>  
```  
  
> [!NOTE]
> En [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)], se crea un archivo de sitio de origen agregando un archivo a un proyecto y estableciendo `Build Action` su `None`en.  
  
 Cuando se compila el proyecto, MSBuild copia los archivos especificados en la carpeta de resultados de la compilación.  
  
### <a name="using-site-of-origin-files"></a>Uso de archivos del sitio de origen  
 Para cargar un archivo de sitio de origen, puede llamar al <xref:System.Windows.Application.GetRemoteStream%2A> método de la <xref:System.Windows.Application> clase, pasando un paquete [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] que identifique el archivo de sitio de origen deseado. <xref:System.Windows.Application.GetRemoteStream%2A>Devuelve un <xref:System.Windows.Resources.StreamResourceInfo> objeto, que expone el archivo del sitio de origen <xref:System.IO.Stream> como y describe su tipo de contenido.  
  
 Como ejemplo, el código <xref:System.Windows.Application.GetRemoteStream%2A> siguiente muestra cómo utilizar para cargar un <xref:System.Windows.Controls.Page> archivo de sitio de origen y establecerlo como el contenido de un <xref:System.Windows.Controls.Frame> (`pageFrame`).  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadAPageSOOFileManuallyCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/SOOPage.xaml.cs#loadapagesoofilemanuallycode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadAPageSOOFileManuallyCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/SOOPage.xaml.vb#loadapagesoofilemanuallycode)]  
  
 Aunque llamar <xref:System.Windows.Application.GetRemoteStream%2A> a proporciona acceso <xref:System.IO.Stream>a, debe realizar el trabajo adicional de convertirlo al tipo de la propiedad con la que se va a establecer. En su lugar, puede dejar [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] que se ocupe de abrir y convertir <xref:System.IO.Stream> mediante la carga de un archivo de recursos directamente en la propiedad de un tipo mediante el código.  
  
 En el ejemplo siguiente se muestra cómo cargar <xref:System.Windows.Controls.Page> un directamente en <xref:System.Windows.Controls.Frame> un`pageFrame`() mediante código.  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadPageSOOFileFromCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/SOOPage.xaml.cs#loadpagesoofilefromcode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadPageSOOFileFromCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/SOOPage.xaml.vb#loadpagesoofilefromcode)]  
  
 El ejemplo siguiente es el equivalente de marcación del ejemplo anterior.  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#LoadPageSOOFileFromXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/SOOPage.xaml#loadpagesoofilefromxaml)]  
  
<a name="Rebuilding_after_Changing_Build_Type"></a>   
## <a name="rebuilding-after-changing-build-type"></a>Nueva compilación después de cambiar el tipo de compilación  
 Después de cambiar el tipo de compilación de un archivo de datos de aplicación, es preciso volver a compilar toda la aplicación para asegurarse de que se aplican los cambios. Si solo compila la aplicación, no se aplican los cambios.  
  
## <a name="see-also"></a>Vea también

- [Identificadores URI de paquete en WPF](pack-uris-in-wpf.md)
