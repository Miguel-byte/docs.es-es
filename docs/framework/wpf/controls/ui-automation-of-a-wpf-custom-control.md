---
title: Automatización de la interfaz de usuario de un control personalizado de WPF
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- custom controls [WPF], applying UI automation
- accessibility [WPF], applying to custom controls
- custom controls [WPF], improving accessibility
- UI Automation [WPF], using with custom controls
ms.assetid: 47b310fc-fbd5-4ce2-a606-22d04c6d4911
ms.openlocfilehash: ef045ffaac47c6cb196d821c25d96c4d2cd7bf88
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2019
ms.locfileid: "70254247"
---
# <a name="ui-automation-of-a-wpf-custom-control"></a>Automatización de la interfaz de usuario de un control personalizado de WPF
[!INCLUDE[TLA#tla_uiautomation](../../../../includes/tlasharptla-uiautomation-md.md)] proporciona una única interfaz generalizada que los clientes de automatización pueden utilizar para examinar o utilizar las interfaces de usuario de una variedad de plataformas y entornos. [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] permite al código de control de calidad (prueba) y a las aplicaciones de accesibilidad, tales como lectores de pantalla, examinar los elementos de la interfaz de usuario y simular la interacción del usuario con ellos desde otro código. Para más información acerca de [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] en todas las plataformas, consulte Accesibilidad.  
  
 En este tema se describe cómo implementar un proveedor de automatización de la interfaz de usuario del lado servidor para un control personalizado que se ejecuta en una aplicación de WPF. WPF admite [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] mediante un árbol de objetos de automatización del mismo nivel que se corresponde con el árbol de elementos de la interfaz de usuario. El código de prueba y las aplicaciones que proporcionan características de accesibilidad pueden usar objetos de automatización del mismo nivel directamente (para código en proceso) o mediante la interfaz generalizada proporcionada por [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)].  

<a name="AutomationPeerClasses"></a>   
## <a name="automation-peer-classes"></a>Clases de automatización del mismo nivel  
 Los controles de [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] WPF admiten a través de un árbol de <xref:System.Windows.Automation.Peers.AutomationPeer>clases del mismo nivel que derivan de. Por convención, los nombres de clase del mismo nivel empiezan por el nombre de clase del control y terminan por "AutomationPeer". Por ejemplo, <xref:System.Windows.Automation.Peers.ButtonAutomationPeer> es la clase del mismo nivel <xref:System.Windows.Controls.Button> para la clase del control. Las clases del mismo nivel equivalen a los tipos de control de [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)], pero son específicas de los elementos de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]. El código de automatización que tiene acceso a las aplicaciones de WPF mediante la interfaz [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] no utiliza directamente elementos de automatización del mismo nivel; sin embargo, el código de automatización en el mismo espacio de proceso puede utilizar directamente elementos de automatización del mismo nivel.  
  
<a name="BuiltInAutomationPeerClasses"></a>   
## <a name="built-in-automation-peer-classes"></a>Clases de automatización del mismo nivel integradas  
 Los elementos implementan una clase de automatización del mismo nivel si aceptan la actividad de la interfaz de usuario o si contienen la información necesaria para los usuarios de aplicaciones de lector de pantalla. No todos los elementos visuales de WPF tienen elementos de automatización del mismo nivel. Ejemplos de clases que implementan elementos de automatización <xref:System.Windows.Controls.Button>del <xref:System.Windows.Controls.TextBox>mismo nivel <xref:System.Windows.Controls.Label>son, y. Ejemplos de clases que no implementan elementos de automatización del mismo nivel son clases <xref:System.Windows.Controls.Decorator>que derivan <xref:System.Windows.Controls.Border>de, como, y <xref:System.Windows.Controls.Panel>clases <xref:System.Windows.Controls.Grid> basadas en, <xref:System.Windows.Controls.Canvas>como y.  
  
 La clase <xref:System.Windows.Controls.Control> base no tiene una clase del mismo nivel correspondiente. Si necesita que una clase del mismo nivel se corresponda con un control personalizado que <xref:System.Windows.Controls.Control>deriva de, debe derivar la clase personalizada <xref:System.Windows.Automation.Peers.FrameworkElementAutomationPeer>del mismo nivel de.  
  
<a name="SecurityConsiderations"></a>   
## <a name="security-considerations-for-derived-peers"></a>Consideraciones de seguridad para elementos del mismo nivel derivados  
 Los elementos de automatización del mismo nivel deben ejecutarse en un entorno de confianza parcial. El código del ensamblado UIAutomationClient no está configurado para ejecutarse en un entorno de confianza parcial y el código de automatización del mismo nivel no debe hacer referencia a dicho ensamblado. En su lugar, debe usar las clases del ensamblado UIAutomationTypes. Por ejemplo, debe usar la <xref:System.Windows.Automation.AutomationElementIdentifiers> clase del ensamblado UIAutomationTypes, que corresponde a la <xref:System.Windows.Automation.AutomationElement> clase en el ensamblado UIAutomationClient. Es seguro hacer referencia al ensamblado UIAutomationTypes en el código de automatización del mismo nivel.  
  
<a name="PeerNavigation"></a>   
## <a name="peer-navigation"></a>Navegación entre elementos del mismo nivel  
 Después de encontrar un elemento de automatización del mismo nivel, el código en proceso puede navegar por el árbol del <xref:System.Windows.Automation.Peers.AutomationPeer.GetChildren%2A> mismo <xref:System.Windows.Automation.Peers.AutomationPeer.GetParent%2A> nivel llamando a los métodos y del objeto. La navegación [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] entre los elementos de un control es compatible con la implementación <xref:System.Windows.Automation.Peers.AutomationPeer.GetChildrenCore%2A> del método del mismo nivel. El sistema de automatización de la interfaz de usuario llama a este método para crear un árbol de subelementos incluidos dentro de un control; por ejemplo, los elementos de lista de un cuadro de lista. El método <xref:System.Windows.Automation.Peers.UIElementAutomationPeer.GetChildrenCore%2A?displayProperty=nameWithType> predeterminado atraviesa el árbol visual de elementos para compilar el árbol de elementos de automatización del mismo nivel. Los controles personalizados invalidan este método para exponer los elementos secundarios a los clientes de automatización, y devuelven aquellos elementos de automatización del mismo nivel que transmiten información o permiten la interacción del usuario.  
  
<a name="Customizations"></a>   
## <a name="customizations-in-a-derived-peer"></a>Personalizaciones en un elemento del mismo nivel derivado  
 Todas las clases que derivan <xref:System.Windows.ContentElement> de <xref:System.Windows.UIElement> y contienen el método <xref:System.Windows.UIElement.OnCreateAutomationPeer%2A>virtual protegido. WPF llama <xref:System.Windows.UIElement.OnCreateAutomationPeer%2A> a para obtener el objeto de automatización del mismo nivel para cada control. El código de automatización puede utilizar el elemento del mismo nivel para obtener información sobre las características y funciones de un control, y simular el uso interactivo. Un control personalizado que admite Automation debe reemplazar <xref:System.Windows.UIElement.OnCreateAutomationPeer%2A> y devolver una instancia de una clase que deriva de. <xref:System.Windows.Automation.Peers.AutomationPeer> Por ejemplo, si un control personalizado se deriva de la <xref:System.Windows.Controls.Primitives.ButtonBase> clase, el objeto devuelto por <xref:System.Windows.UIElement.OnCreateAutomationPeer%2A> debe derivar <xref:System.Windows.Automation.Peers.ButtonBaseAutomationPeer>de.  
  
 Al implementar un control personalizado, se deben invalidar los métodos "Core" de la clase base de automatización del mismo nivel, que describen el comportamiento único y específico del control personalizado.  
  
### <a name="override-oncreateautomationpeer"></a>Invalidar OnCreateAutomationPeer  
 Invalide el <xref:System.Windows.UIElement.OnCreateAutomationPeer%2A> método para el control personalizado de modo que devuelva el objeto de proveedor, que debe derivarse directa o indirectamente de <xref:System.Windows.Automation.Peers.AutomationPeer>.  
  
### <a name="override-getpattern"></a>Invalidar GetPattern  
 Los elementos de automatización del mismo nivel simplifican algunos aspectos de la implementación de proveedores de [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] del lado servidor; sin embargo, los elementos de automatización del mismo nivel de un control personalizado deben controlar las interfaces de patrón. Al igual que los proveedores que no son de WPF, los elementos del mismo nivel admiten patrones <xref:System.Windows.Automation.Provider?displayProperty=nameWithType> de control al proporcionar <xref:System.Windows.Automation.Provider.IInvokeProvider>implementaciones de interfaces en el espacio de nombres, como. Las interfaces de patrón de control pueden implementarlas el propio elemento del mismo nivel u otro objeto. La implementación del elemento del <xref:System.Windows.Automation.Peers.AutomationPeer.GetPattern%2A> mismo nivel de devuelve el objeto que admite el patrón especificado. [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]el código llama <xref:System.Windows.Automation.Peers.UIElementAutomationPeer.GetPattern%2A> al método y especifica <xref:System.Windows.Automation.Peers.PatternInterface> un valor de enumeración. La invalidación <xref:System.Windows.Automation.Peers.UIElementAutomationPeer.GetPattern%2A> de debe devolver el objeto que implementa el patrón especificado. Si el control no tiene una implementación personalizada de un patrón, puede llamar a la implementación del tipo base de <xref:System.Windows.Automation.Peers.AutomationPeer.GetPattern%2A> para recuperar su implementación o null si el patrón no se admite para este tipo de control. Por ejemplo, un control NumericUpDown personalizado se puede establecer en un valor dentro de un intervalo, por [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] lo que su elemento <xref:System.Windows.Automation.Provider.IRangeValueProvider> del mismo nivel implementaría la interfaz. En el ejemplo siguiente se muestra cómo se <xref:System.Windows.Automation.Peers.UIElementAutomationPeer.GetPattern%2A> invalida el método del mismo nivel para responder <xref:System.Windows.Automation.Peers.PatternInterface.RangeValue?displayProperty=nameWithType> a un valor.  
  
 [!code-csharp[CustomControlNumericUpDown#GetPattern](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp/CustomControlLibrary/NumericUpDown.cs#getpattern)]
 [!code-vb[CustomControlNumericUpDown#GetPattern](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic/customcontrollibrary/numericupdown.vb#getpattern)]  
  
 Un <xref:System.Windows.Automation.Peers.UIElementAutomationPeer.GetPattern%2A> método también puede especificar un subelemento como proveedor de patrones. En el código siguiente se <xref:System.Windows.Controls.ItemsControl> muestra cómo transfiere el control del patrón de desplazamiento al <xref:System.Windows.Controls.ScrollViewer> elemento del mismo nivel de su control interno.  
  
```csharp  
public override object GetPattern(PatternInterface patternInterface)  
{  
    if (patternInterface == PatternInterface.Scroll)  
    {  
        ItemsControl owner = (ItemsControl) base.Owner;  
  
        // ScrollHost is internal to the ItemsControl class  
        if (owner.ScrollHost != null)  
        {  
            AutomationPeer peer = UIElementAutomationPeer.CreatePeerForElement(owner.ScrollHost);  
            if ((peer != null) && (peer is IScrollProvider))  
            {  
                peer.EventsSource = this;  
                return (IScrollProvider) peer;  
            }  
        }  
    }  
    return base.GetPattern(patternInterface);  
}  
```  
  
```vb  
Public Class Class1  
    Public Overrides Function GetPattern(ByVal patternInterface__1 As PatternInterface) As Object  
        If patternInterface1 = PatternInterface.Scroll Then  
            Dim owner As ItemsControl = DirectCast(MyBase.Owner, ItemsControl)  
  
            ' ScrollHost is internal to the ItemsControl class  
            If owner.ScrollHost IsNot Nothing Then  
                Dim peer As AutomationPeer = UIElementAutomationPeer.CreatePeerForElement(owner.ScrollHost)  
                If (peer IsNot Nothing) AndAlso (TypeOf peer Is IScrollProvider) Then  
                    peer.EventsSource = Me  
                    Return DirectCast(peer, IScrollProvider)  
                End If  
            End If  
        End If  
        Return MyBase.GetPattern(patternInterface1)  
    End Function  
End Class  
```  
  
 Para especificar un subelemento para el control de patrones, este código obtiene el objeto de subelemento, crea un elemento <xref:System.Windows.Automation.Peers.UIElementAutomationPeer.CreatePeerForElement%2A> del mismo nivel mediante <xref:System.Windows.Automation.Peers.AutomationPeer.EventsSource%2A> el método, establece la propiedad del nuevo elemento del mismo nivel en el elemento del mismo nivel actual y devuelve el nuevo elemento del mismo nivel. Establecer <xref:System.Windows.Automation.Peers.AutomationPeer.EventsSource%2A> en un subelemento evita que el subelemento aparezca en el árbol de automatización del mismo nivel y designa todos los eventos generados por el subelemento como originados en <xref:System.Windows.Automation.Peers.AutomationPeer.EventsSource%2A>el control especificado en. El <xref:System.Windows.Controls.ScrollViewer> control no aparece en el árbol de automatización y los eventos de desplazamiento que genera parecen originarse en el <xref:System.Windows.Controls.ItemsControl> objeto.  
  
### <a name="override-core-methods"></a>Invalidar métodos "Core"  
 Para obtener información sobre el control, el código de automatización llama a métodos públicos de la clase del mismo nivel. Para proporcionar información sobre el control, invalide los métodos cuyo nombre termina con "Core" en caso de que la implementación del control sea diferente de la que proporciona la clase base de automatización del mismo nivel. Como mínimo, el control debe implementar los <xref:System.Windows.Automation.Peers.AutomationPeer.GetClassNameCore%2A> métodos y, tal y <xref:System.Windows.Automation.Peers.AutomationPeer.GetAutomationControlTypeCore%2A> como se muestra en el ejemplo siguiente.  
  
 [!code-csharp[CustomControlNumericUpDown#CoreOverrides](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp/CustomControlLibrary/NumericUpDown.cs#coreoverrides)]
 [!code-vb[CustomControlNumericUpDown#CoreOverrides](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic/customcontrollibrary/numericupdown.vb#coreoverrides)]  
  
 La implementación de <xref:System.Windows.Automation.Peers.AutomationPeer.GetAutomationControlTypeCore%2A> describe el control devolviendo un <xref:System.Windows.Automation.ControlType> valor. Aunque puede devolver <xref:System.Windows.Automation.ControlType.Custom?displayProperty=nameWithType>, debe devolver uno de los tipos de control más específicos si describe con precisión el control. Un valor devuelto <xref:System.Windows.Automation.ControlType.Custom?displayProperty=nameWithType> de requiere un trabajo adicional para que el [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]proveedor implemente, y [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)] los productos cliente no pueden anticipar la estructura del control, la interacción con el teclado y los posibles patrones de control.  
  
 Implemente <xref:System.Windows.Automation.Peers.AutomationPeer.IsContentElementCore%2A> los <xref:System.Windows.Automation.Peers.AutomationPeer.IsControlElementCore%2A> métodos y para indicar si el control contiene contenido de datos o si cumple un rol interactivo en la interfaz de usuario (o ambos). De forma predeterminada, ambos métodos devuelven `true`. Esta configuración aumenta la facilidad de uso de herramientas de automatización, como lectores de pantalla, que pueden utilizar estos métodos para filtrar el árbol de automatización. Si el <xref:System.Windows.Automation.Peers.AutomationPeer.GetPattern%2A> método transfiere el control del patrón a un subelemento del mismo nivel, el <xref:System.Windows.Automation.Peers.AutomationPeer.IsControlElementCore%2A> método del subelemento del mismo nivel puede devolver false para ocultar el subelemento del mismo nivel del árbol de automatización. Por ejemplo <xref:System.Windows.Controls.ListBox> , el <xref:System.Windows.Automation.Peers.PatternInterface.Scroll?displayProperty=nameWithType> <xref:System.Windows.Controls.ScrollViewer> <xref:System.Windows.Automation.Peers.ListBoxAutomationPeer> <xref:System.Windows.Automation.Peers.ScrollViewerAutomationPeer> desplazamiento en se controla mediante y el método de la clase que está asociada a la clase de automatización del mismo nivel para. <xref:System.Windows.Automation.Peers.AutomationPeer.GetPattern%2A> Por lo tanto <xref:System.Windows.Automation.Peers.AutomationPeer.IsControlElementCore%2A> , el método <xref:System.Windows.Automation.Peers.ScrollViewerAutomationPeer> de `false` <xref:System.Windows.Automation.Peers.ScrollViewerAutomationPeer> devuelve, de modo que no aparece en el árbol de automatización.  
  
 El elemento de automatización del mismo nivel debe proporcionar los valores predeterminados adecuados para el control. Tenga en cuenta que el código XAML que hace referencia al control puede invalidar las implementaciones <xref:System.Windows.Automation.AutomationProperties> del mismo nivel de los métodos principales mediante la inclusión de atributos. Por ejemplo, el código XAML siguiente crea un botón que tiene dos propiedades personalizadas [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)].  
  
```xaml  
<Button AutomationProperties.Name="Special"   
    AutomationProperties.HelpText="This is a special button."/>  
```  
  
### <a name="implement-pattern-providers"></a>Implementar proveedores de patrón  
 Las interfaces implementadas por un proveedor personalizado se declaran explícitamente si el elemento propietario <xref:System.Windows.Controls.Control>deriva directamente de. Por ejemplo, el código siguiente declara un elemento del mismo nivel <xref:System.Windows.Controls.Control> para un que implementa un valor de intervalo.  
  
```csharp  
public class RangePeer1 : FrameworkElementAutomationPeer, IRangeValueProvider { }  
```  
  
```vb  
Public Class RangePeer1  
    Inherits FrameworkElementAutomationPeer  
    Implements IRangeValueProvider  
End Class  
```  
  
 Si el control propietario se deriva de un tipo de control específico, <xref:System.Windows.Controls.Primitives.RangeBase>como, el elemento del mismo nivel se puede derivar de una clase derivada equivalente equivalente. En este caso, el elemento del mismo nivel <xref:System.Windows.Automation.Peers.RangeBaseAutomationPeer>derivaría de, que proporciona una <xref:System.Windows.Automation.Provider.IRangeValueProvider>implementación base de. El código siguiente muestra la declaración de un elemento del mismo nivel como este.  
  
```csharp  
public class RangePeer2 : RangeBaseAutomationPeer { }  
```  
  
```vb  
Public Class RangePeer2  
    Inherits RangeBaseAutomationPeer  
End Class  
```  
  
Para ver una implementación de ejemplo, [C#](https://github.com/dotnet/samples/tree/master/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp) vea el código fuente o [Visual Basic](https://github.com/dotnet/samples/tree/master/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic) que implementa y usa un control personalizado NumericUpDown.  
  
### <a name="raise-events"></a>Generar eventos  
 Los clientes de automatización pueden suscribirse a eventos de automatización. Los controles personalizados deben notificar los cambios en el estado <xref:System.Windows.Automation.Peers.AutomationPeer.RaiseAutomationEvent%2A> del control llamando al método. Del mismo modo, cuando cambia el valor de una <xref:System.Windows.Automation.Peers.AutomationPeer.RaisePropertyChangedEvent%2A> propiedad, llame al método. El código siguiente muestra cómo obtener el objeto del mismo nivel desde el código del control, y cómo llamar a un método para generar un evento. Como optimización, el código determina si hay agentes de escucha para este tipo de evento. Generar el evento únicamente cuando hay agentes de escucha evita una sobrecarga innecesaria y ayuda a que el control siga respondiendo.  
  
 [!code-csharp[CustomControlNumericUpDown#RaiseEventFromControl](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp/CustomControlLibrary/NumericUpDown.cs#raiseeventfromcontrol)]
 [!code-vb[CustomControlNumericUpDown#RaiseEventFromControl](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic/customcontrollibrary/numericupdown.vb#raiseeventfromcontrol)]  
  
## <a name="see-also"></a>Vea también

- [Información general sobre la Automatización de la interfaz de usuario](../../ui-automation/ui-automation-overview.md)
- [Implementación del proveedor de automatización de la interfaz de usuario en el servidor](../../ui-automation/server-side-ui-automation-provider-implementation.md)
- [Control personalizado NumericUpDown (C#) en github](https://github.com/dotnet/samples/tree/master/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp)  
- [Control personalizado NumericUpDown (Visual Basic) en GitHub](https://github.com/dotnet/samples/tree/master/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic)
