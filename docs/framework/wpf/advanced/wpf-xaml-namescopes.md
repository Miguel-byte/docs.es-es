---
title: Ámbitos de nombres XAML de WPF
ms.date: 03/30/2017
helpviewer_keywords:
- namescopes [WPF]
- styles [WPF], namescopes in
- templates [WPF], namescopes in
- APIs [WPF], name-related
- name-related APIs
- XAML [WPF], namescopes
- classes [WPF], FrameworkContentElement
ms.assetid: 52bbf4f2-15fc-40d4-837b-bb4c21ead7d4
ms.openlocfilehash: edf5c8a828bea182cd87542276fb7eb2df1908be
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69917339"
---
# <a name="wpf-xaml-namescopes"></a>Ámbitos de nombres XAML de WPF
Los ámbitos de nombres XAML son un concepto que identifica objetos que se definen en XAML. Los nombres de un ámbito de nombres XAML se pueden usar para establecer relaciones entre los nombres de objetos definidos por XAML y sus equivalentes de instancia en un árbol de objetos. Normalmente, los ámbitos de nombres XAML del código administrado de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] se crean al cargar las distintas raíces de página XAML de una aplicación XAML. Los ámbitos de código XAML como el objeto de programación <xref:System.Windows.Markup.INameScope> se definen mediante la interfaz y también se implementan mediante la clase <xref:System.Windows.NameScope>práctica.  

<a name="Namescopes_in_Loaded_XAML_Applications"></a>   
## <a name="namescopes-in-loaded-xaml-applications"></a>Ámbitos de nombres en las aplicaciones XAML cargadas  
 En un contexto de programación o de informática más amplio, los conceptos de programación suelen incluir el principio de un identificador o nombre único que se puede usar para obtener acceso a un objeto. Para los sistemas que usan identificadores o nombres, el ámbito de nombres define los límites en los que buscará un proceso o técnica si se solicita un objeto con ese nombre, o bien los límites en los que se aplica la unicidad de la identificación de nombres. En los ámbitos de nombres XAML se aplican los siguientes principios generales. En WPF, los ámbitos de nombres XAML se crean en el elemento raíz de una página XAML cuando esta se carga. Todos los nombres especificados dentro de la página XAML a partir de la raíz de la página se agregan a un ámbito de nombres XAML pertinente.  
  
 En XAML de WPF, los elementos que son elementos raíz comunes ( <xref:System.Windows.Controls.Page>como y <xref:System.Windows.Window>) controlan siempre un ámbito de nombres XAML. Si un elemento como <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement> es el elemento raíz de la página en el marcado, un [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] procesador <xref:System.Windows.Controls.Page> agrega implícitamente una <xref:System.Windows.Controls.Page> raíz para que pueda proporcionar un ámbito de nombres XAML funcional.  
  
> [!NOTE]
> Las acciones de compilación de WPF crean un ámbito de nombres XAML para la producción de XAML, aunque no haya ningún atributo `Name` o `x:Name` definido en ningún elemento del marcado de [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
 Si intenta usar el mismo nombre dos veces en cualquier ámbito de nombres XAML, se producirá una excepción. Para el XAML de WPF que tiene código subyacente y forma parte de una aplicación compilada, la excepción se produce en tiempo de compilación mediante acciones de compilación de WPF, al crear la clase generada para la página durante la compilación inicial del marcado. Para el XAML que no está compilado por el marcado mediante ninguna acción de compilación, las excepciones relacionadas con algún error de ámbito de nombres XAML podrían producirse al cargar el XAML. Los diseñadores de XAML también pueden prever los errores de ámbito de nombres XAML en tiempo de diseño.  
  
### <a name="adding-objects-to-runtime-object-trees"></a>Agregar objetos a los árboles de objetos en tiempo de ejecución  
 El momento en que se analiza el XAML representa el momento en el que se crea y se define un ámbito de nombres XAML de WPF. Si agrega un objeto a un árbol de objetos después de haber analizado el XAML que generó el árbol, los valores `Name` o `x:Name` del objeto nuevo no actualizarán automáticamente la información de un ámbito de nombres XAML. Para agregar un nombre a un objeto en un ámbito de nombres XAML de WPF después de cargar XAML, debe llamar a la <xref:System.Windows.Markup.INameScope.RegisterName%2A> implementación adecuada de en el objeto que define el ámbito de nombres XAML, que suele ser la raíz de la página XAML. Si el nombre no está registrado, no se puede hacer referencia al objeto agregado por nombre a través de <xref:System.Windows.FrameworkElement.FindName%2A>métodos como, y no se puede usar ese nombre para el destino de la animación.  
  
 El escenario más común para los desarrolladores de aplicaciones es que <xref:System.Windows.FrameworkElement.RegisterName%2A> usará para registrar nombres en el ámbito de nombres XAML en la raíz actual de la página. <xref:System.Windows.FrameworkElement.RegisterName%2A>forma parte de un escenario importante para los guiones gráficos que tienen como destino objetos para animaciones. Para obtener más información, consulte [Información general sobre objetos Storyboard](../graphics-multimedia/storyboards-overview.md).  
  
 Si llama <xref:System.Windows.FrameworkElement.RegisterName%2A> a en un objeto que no es el objeto que define el ámbito de nombres XAML, el nombre todavía se registra en el ámbito de nombres XAML en el que se mantiene el objeto que <xref:System.Windows.FrameworkElement.RegisterName%2A> realiza la llamada, como si hubiera llamado en el objeto que define el ámbito de nombres XAML.  
  
### <a name="xaml-namescopes-in-code"></a>Ámbitos de nombres XAML en el código  
 Puede crear y usar ámbitos de nombres XAML en el código. Las API y los conceptos implicados en la creación de ámbitos de nombres XAML son los mismos, incluso para un uso de código puro, ya que el procesador XAML de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] usa estas API y estos conceptos cuando procesa el XAML. Los conceptos y las API existen principalmente para poder buscar objetos por nombre dentro de un árbol de objetos que se suele definir parcial o completamente en XAML.  
  
 En el caso de las aplicaciones que se crean mediante programación y no desde XAML cargado, el objeto que define un ámbito <xref:System.Windows.Markup.INameScope>de nombres XAML debe <xref:System.Windows.FrameworkElement> implementar <xref:System.Windows.FrameworkContentElement> , o ser una clase derivada, para admitir la creación de un ámbito de nombres XAML en su Stance.  
  
 Además, para cualquier elemento que no se haya cargado y procesado con un procesador XAML, el ámbito de nombres XAML del objeto no se crea ni se inicializa de forma predeterminada. Debe crear explícitamente un ámbito de nombres XAML para cualquier objeto en el que después vaya a registrar nombres. Para crear un ámbito de nombres XAML, se llama <xref:System.Windows.NameScope.SetNameScope%2A> al método estático. Especifique el objeto que lo poseerá como `dependencyObject` parámetro y una nueva <xref:System.Windows.NameScope.%23ctor%2A> llamada de constructor como `value` parámetro.  
  
 Si el objeto proporcionado como `dependencyObject` para <xref:System.Windows.NameScope.SetNameScope%2A> no es una <xref:System.Windows.Markup.INameScope> implementación de <xref:System.Windows.FrameworkElement> , <xref:System.Windows.FrameworkContentElement>o, <xref:System.Windows.FrameworkElement.RegisterName%2A> la llamada a en cualquier elemento secundario no tendrá ningún efecto. Si no se puede crear el nuevo ámbito de nombres XAML explícitamente, <xref:System.Windows.FrameworkElement.RegisterName%2A> las llamadas a producirán una excepción.  
  
 Para ver un ejemplo de cómo usar las API de ámbito de nombres XAML en el código, consulte [Definir un ámbito de nombres](../graphics-multimedia/how-to-define-a-name-scope.md).  
  
<a name="Namescopes_in_Styles_and_Templates"></a>   
## <a name="xaml-namescopes-in-styles-and-templates"></a>Ámbitos de nombres XAML en estilos y plantillas  
 Los estilos y las plantillas de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ofrecen la posibilidad de reutilizar y volver a aplicar el contenido de una manera sencilla, aunque también pueden incluir elementos con nombres XAML definidos en el nivel de la plantilla. Esa misma plantilla se puede usar varias veces en una página. Por este motivo, tanto los estilos como las plantillas definen sus propios ámbitos de nombres XAML, independientemente de la ubicación en un árbol de objetos en la que se aplique el estilo o plantilla.  
  
 Considere el ejemplo siguiente:  
  
 [!code-xaml[XamlOvwSupport#NameScopeTemplates](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page6.xaml#namescopetemplates)]  
  
 En este caso, se aplica la misma plantilla a dos botones diferentes. Si las plantillas no tuvieran ámbitos de nombres XAML discretos, el nombre `TheBorder` usado en la plantilla provocaría un conflicto de nombres en el ámbito de nombres XAML. Todas las instancias de la plantilla tienen su propio ámbito de nombres XAML, por lo que, en este ejemplo, el ámbito de nombres XAML de todas las plantillas de instancia contendrían exactamente un nombre.  
  
 Los estilos también definen su propio ámbito de nombres XAML, sobre todo para que las partes de los guiones gráficos puedan tener asignados nombres concretos. Estos nombres permiten que haya comportamientos específicos de controles destinados a elementos con ese nombre, incluso si la plantilla se ha vuelto a definir como parte de la personalización de controles.  
  
 Debido a los ámbitos de nombres XAML independientes, resulta más difícil buscar elementos con nombre en una plantilla que buscar un elemento con nombre y sin plantilla en una página. En primer lugar, debe determinar la plantilla aplicada, obteniendo el <xref:System.Windows.Controls.Control.Template%2A> valor de propiedad del control al que se aplica la plantilla. A continuación, se llama a la versión <xref:System.Windows.FrameworkTemplate.FindName%2A>de plantilla de, pasando el control en el que se aplicó la plantilla como segundo parámetro.  
  
 Si es un autor de controles y está generando una Convención en la que un elemento con nombre determinado en una plantilla aplicada es el destino de un comportamiento definido por el propio control, puede usar el <xref:System.Windows.FrameworkElement.GetTemplateChild%2A> método desde el código de implementación del control. El <xref:System.Windows.FrameworkElement.GetTemplateChild%2A> método está protegido, por lo que solo el autor del control tiene acceso a él.  
  
 Si está trabajando desde dentro de una plantilla, y necesita obtener acceso al ámbito de nombres XAML donde se aplica la plantilla, obtenga el valor <xref:System.Windows.FrameworkElement.TemplatedParent%2A>de y, a <xref:System.Windows.FrameworkElement.FindName%2A> continuación, llame a ahí. Un ejemplo de trabajo dentro de la plantilla sería escribir la implementación del controlador de eventos donde se generará el evento desde un elemento de una plantilla aplicada.  
  
<a name="Namescopes_and_Name_related_APIs"></a>   
## <a name="xaml-namescopes-and-name-related-apis"></a>Ámbitos de nombres XAML y API relacionadas con nombres  
 <xref:System.Windows.FrameworkElement>tiene <xref:System.Windows.FrameworkElement.FindName%2A>los <xref:System.Windows.FrameworkElement.RegisterName%2A> métodos <xref:System.Windows.FrameworkElement.UnregisterName%2A> , y. Si el objeto en el que llama a estos métodos tiene un ámbito de nombres XAML, los métodos llaman a los métodos del ámbito de nombres XAML relevante. De lo contrario, se comprueba el elemento primario para ver si tiene un ámbito de nombres XAML. Este proceso continúa de forma recursiva hasta que se encuentra un ámbito de nombres XAML (debido al comportamiento del procesador XAML, se garantiza que haya un ámbito de nombres XAML en la raíz). <xref:System.Windows.FrameworkContentElement>tiene comportamientos análogos, con la excepción de <xref:System.Windows.FrameworkContentElement> que nunca tendrá un ámbito de nombres XAML. Los métodos existen en <xref:System.Windows.FrameworkContentElement> para que las llamadas se puedan reenviar finalmente a un <xref:System.Windows.FrameworkElement> elemento primario.  
  
 <xref:System.Windows.NameScope.SetNameScope%2A>se utiliza para asignar un nuevo ámbito de nombres XAML a un objeto existente. Puede llamar <xref:System.Windows.NameScope.SetNameScope%2A> a más de una vez para restablecer o borrar el ámbito de nombres XAML, pero esto no es un uso común. Además, <xref:System.Windows.NameScope.GetNameScope%2A> no se suele usar desde el código.  
  
### <a name="xaml-namescope-implementations"></a>Implementaciones de ámbito de nombres XAML  
 Las clases siguientes implementan <xref:System.Windows.Markup.INameScope> directamente:  
  
- <xref:System.Windows.NameScope>  
  
- <xref:System.Windows.Style>  
  
- <xref:System.Windows.ResourceDictionary>  
  
- <xref:System.Windows.FrameworkTemplate>  
  
 <xref:System.Windows.ResourceDictionary>no utiliza nombres o ámbitos de nombres XAML. en su lugar, utiliza claves, ya que es una implementación de diccionario. El único motivo por <xref:System.Windows.ResourceDictionary> el que <xref:System.Windows.Markup.INameScope> implementa es que puede generar excepciones al código de usuario que ayuden a clarificar la distinción entre un ámbito de <xref:System.Windows.ResourceDictionary> nombres XAML verdadero y cómo controla las claves, además de garantizar que los ámbitos de nombres XAML no se aplican a un <xref:System.Windows.ResourceDictionary> por elementos primarios.  
  
 <xref:System.Windows.FrameworkTemplate>e <xref:System.Windows.Style> implementan <xref:System.Windows.Markup.INameScope> a través de definiciones de interfaz explícitas. Las implementaciones explícitas permiten que estos ámbitos de código XAML se comporten de forma convencional <xref:System.Windows.Markup.INameScope> cuando se accede a ellos a través de la interfaz, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] que es la forma en que los procesos internos comunican los ámbitos de código XAML. Sin embargo, las definiciones de interfaz explícitas no forman parte de la <xref:System.Windows.FrameworkTemplate> superficie <xref:System.Windows.Style>de la API convencional de y, porque <xref:System.Windows.Markup.INameScope> rara vez es <xref:System.Windows.Style> necesario llamar a los métodos en <xref:System.Windows.FrameworkTemplate> y directamente, y en su lugar usaría otra API <xref:System.Windows.FrameworkElement.GetTemplateChild%2A>como.  
  
 Las siguientes clases definen su propio ámbito de nombres XAML, mediante <xref:System.Windows.NameScope?displayProperty=nameWithType> el uso de la clase auxiliar y la conexión a su implementación <xref:System.Windows.NameScope.NameScope%2A?displayProperty=nameWithType> del ámbito de nombres XAML a través de la propiedad adjunta:  
  
- <xref:System.Windows.FrameworkElement>  
  
- <xref:System.Windows.FrameworkContentElement>  
  
## <a name="see-also"></a>Vea también

- [Espacios de nombres y asignación de espacios de nombres XAML para WPF](xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)
- [x:Name (Directiva)](../../xaml-services/x-name-directive.md)
