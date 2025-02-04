---
title: Información general sobre pinceles de WPF
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- brushes [WPF], about brushes
ms.assetid: ecea1955-420b-45c6-bf43-c1404c072c41
ms.openlocfilehash: 29f0bc77306df5639c188295f9f5dff7f18b4706
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962843"
---
# <a name="wpf-brushes-overview"></a>Información general sobre pinceles de WPF
Todo lo que está visible en la pantalla es visible porque lo ha pintado un pincel. Por ejemplo, se usa un pincel para describir el fondo de un botón, el primer plano del texto y el relleno de una forma. En este tema se presentan los conceptos del [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] dibujo con pinceles y se proporcionan ejemplos. Los pinceles permiten pintar objetos [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] con cualquier cosa, desde colores simples y sólidos hasta conjuntos complejos de patrones e imágenes.  
  
<a name="paintingwithbrush"></a>   
## <a name="painting-with-a-brush"></a>Pintar con un pincel  
 <xref:System.Windows.Media.Brush> "Pinta" un área con su salida. Los distintos pinceles tienen distintos tipos de resultados. Algunos pinceles pintan un área con un color sólido, otros con un degradado, un patrón, una imagen o un dibujo. En la ilustración siguiente se muestran ejemplos de cada uno <xref:System.Windows.Media.Brush> de los distintos tipos.  
  
 ![Tipos de pincel](./media/graphicsmm-brushtypes.jpg "graphicsmm_brushtypes")  
Ejemplos de pincel  
  
 La mayoría de los objetos visuales le permiten especificar cómo se dibujan. En la tabla siguiente se enumeran algunos objetos y propiedades comunes con los que <xref:System.Windows.Media.Brush>se puede usar.  
  
|Clase|Propiedades de pincel|  
|-----------|----------------------|  
|<xref:System.Windows.Controls.Border>|<xref:System.Windows.Controls.Border.BorderBrush%2A>, <xref:System.Windows.Controls.Border.Background%2A>|  
|<xref:System.Windows.Controls.Control>|<xref:System.Windows.Controls.Control.Background%2A>, <xref:System.Windows.Controls.Control.Foreground%2A>|  
|<xref:System.Windows.Controls.Panel>|<xref:System.Windows.Controls.Panel.Background%2A>|  
|<xref:System.Windows.Media.Pen>|<xref:System.Windows.Media.Pen.Brush%2A>|  
|<xref:System.Windows.Shapes.Shape>|<xref:System.Windows.Shapes.Shape.Fill%2A>, <xref:System.Windows.Shapes.Shape.Stroke%2A>|  
|<xref:System.Windows.Controls.TextBlock>|<xref:System.Windows.Controls.TextBlock.Background%2A>|  
  
 En las secciones siguientes se describen <xref:System.Windows.Media.Brush> los distintos tipos y se proporciona un ejemplo de cada uno.  
  
<a name="paintwithsolidcolorbrush"></a>   
## <a name="paint-with-a-solid-color"></a>Pintar con un color sólido  
 Dibuja un área con un sólido <xref:System.Windows.Media.Color>. <xref:System.Windows.Media.SolidColorBrush> Hay varias maneras de especificar el <xref:System.Windows.Media.SolidColorBrush.Color%2A> de un <xref:System.Windows.Media.SolidColorBrush>: por ejemplo, puede especificar sus canales alfa, rojo, azul y verde o usar uno de los colores predefinidos proporcionados por la <xref:System.Windows.Media.Colors> clase.  
  
 <xref:System.Windows.Media.SolidColorBrush> En el ejemplo siguiente se utiliza para pintar <xref:System.Windows.Shapes.Shape.Fill%2A> el de <xref:System.Windows.Shapes.Rectangle>un. En la ilustración siguiente se muestra el rectángulo pintado.  
  
 ![Rectángulo pintado mediante SolidColorBrush](./media/graphicsmm-brush-ovw-solidcolorbrush.png "graphicsmm_brush_ovw_solidcolorbrush")  
Rectángulo pintado mediante SolidColorBrush  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmsolidcolorbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmsolidcolorbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmsolidcolorbrushexampleinline)]  
  
 Para obtener más información sobre <xref:System.Windows.Media.SolidColorBrush> la clase, consulte la [información general sobre el dibujo con colores sólidos y degradados](painting-with-solid-colors-and-gradients-overview.md).  
  
<a name="paintwithlineargradientbrush"></a>   
## <a name="paint-with-a-linear-gradient"></a>Pintar con un degradado lineal  
 <xref:System.Windows.Media.LinearGradientBrush> Dibuja un área con un degradado lineal. Un degradado lineal combina dos o más colores en una línea, el eje de degradado. Los objetos <xref:System.Windows.Media.GradientStop> se utilizan para especificar los colores del degradado y sus posiciones.  
  
 <xref:System.Windows.Media.LinearGradientBrush> En el ejemplo siguiente se utiliza para pintar <xref:System.Windows.Shapes.Shape.Fill%2A> el de <xref:System.Windows.Shapes.Rectangle>un. En la ilustración siguiente se muestra el rectángulo pintado.  
  
 ![Rectángulo pintado mediante LinearGradientBrush](./media/graphicsmm-brush-ovw-lineargradientbrush.jpg "graphicsmm_brush_ovw_lineargradientbrush")  
Rectángulo pintado mediante LinearGradientBrush  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmlineargradientbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmlineargradientbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmlineargradientbrushexampleinline)]  
  
 Para obtener más información sobre <xref:System.Windows.Media.LinearGradientBrush> la clase, consulte la [información general sobre el dibujo con colores sólidos y degradados](painting-with-solid-colors-and-gradients-overview.md).  
  
<a name="paintwithradialgradientbrush"></a>   
## <a name="paint-with-a-radial-gradient"></a>Pintar con un degradado radial  
 <xref:System.Windows.Media.RadialGradientBrush> Dibuja un área con un degradado radial. Un degradado radial combina dos o más colores en un círculo. Al igual que <xref:System.Windows.Media.LinearGradientBrush> con la clase, <xref:System.Windows.Media.GradientStop> los objetos se utilizan para especificar los colores del degradado y sus posiciones.  
  
 <xref:System.Windows.Media.RadialGradientBrush> En el ejemplo siguiente se utiliza para pintar <xref:System.Windows.Shapes.Shape.Fill%2A> el de <xref:System.Windows.Shapes.Rectangle>un. En la ilustración siguiente se muestra el rectángulo pintado.  
  
 ![Rectángulo pintado mediante RadialGradientBrush](./media/graphicsmm-brush-ovw-radialgradientbrush.jpg "graphicsmm_brush_ovw_radialgradientbrush")  
Rectángulo pintado mediante RadialGradientBrush  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmradialgradientbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmradialgradientbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmradialgradientbrushexampleinline)]  
  
 Para obtener más información sobre <xref:System.Windows.Media.RadialGradientBrush> la clase, consulte la [información general sobre el dibujo con colores sólidos y degradados](painting-with-solid-colors-and-gradients-overview.md).  
  
<a name="paintwithimage"></a>   
## <a name="paint-with-an-image"></a>Pintar con una imagen  
 Dibuja un área con un <xref:System.Windows.Media.ImageSource>. <xref:System.Windows.Media.ImageBrush>  
  
 <xref:System.Windows.Media.ImageBrush> En el ejemplo siguiente se utiliza para pintar <xref:System.Windows.Shapes.Shape.Fill%2A> el de <xref:System.Windows.Shapes.Rectangle>un. En la ilustración siguiente se muestra el rectángulo pintado.  
  
 ![Rectángulo pintado por un ImageBrush](./media/graphicsmm-brush-ovw-imagebrush.jpg "graphicsmm_brush_ovw_imagebrush")  
Rectángulo pintado mediante una imagen  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmimagebrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmimagebrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmimagebrushexampleinline)]  
  
 Para obtener más información sobre <xref:System.Windows.Media.ImageBrush> la clase, vea [pintar con imágenes, dibujos y objetos visuales](painting-with-images-drawings-and-visuals.md).  
  
<a name="paintwithdrawing"></a>   
## <a name="paint-with-a-drawing"></a>Pintar con un dibujo  
 Dibuja un área con un <xref:System.Windows.Media.Drawing>. <xref:System.Windows.Media.DrawingBrush> Un <xref:System.Windows.Media.Drawing> puede contener formas, imágenes, texto y elementos multimedia.  
  
 <xref:System.Windows.Media.DrawingBrush> En el ejemplo siguiente se utiliza para pintar <xref:System.Windows.Shapes.Shape.Fill%2A> el de <xref:System.Windows.Shapes.Rectangle>un. En la ilustración siguiente se muestra el rectángulo pintado.  
  
 ![Rectángulo pintado mediante DrawingBrush](./media/graphicsmm-brush-ovw-drawingbrush.jpg "graphicsmm_brush_ovw_drawingbrush")  
Rectángulo pintado mediante DrawingBrush  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmdrawingbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmdrawingbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmdrawingbrushexampleinline)]  
  
 Para obtener más información sobre <xref:System.Windows.Media.DrawingBrush> la clase, vea [pintar con imágenes, dibujos y objetos visuales](painting-with-images-drawings-and-visuals.md).  
  
<a name="paintwithvisual"></a>   
## <a name="paint-with-a-visual"></a>Pintar con un visual  
 Dibuja un área con un <xref:System.Windows.Media.Visual> objeto. <xref:System.Windows.Media.VisualBrush> Entre los ejemplos de objetos <xref:System.Windows.Controls.Button>visuales <xref:System.Windows.Controls.Page>se incluyen <xref:System.Windows.Controls.MediaElement>, y. <xref:System.Windows.Media.VisualBrush> También permite proyectar el contenido de una parte de la aplicación en otra área; resulta muy útil para crear efectos de reflexión y ampliar partes de la pantalla.  
  
 <xref:System.Windows.Media.VisualBrush> En el ejemplo siguiente se utiliza para pintar <xref:System.Windows.Shapes.Shape.Fill%2A> el de <xref:System.Windows.Shapes.Rectangle>un. En la ilustración siguiente se muestra el rectángulo pintado.  
  
 ![Rectángulo pintado mediante VisualBrush](./media/graphicsmm-brush-ovw-visualbrush.jpg "graphicsmm_brush_ovw_visualbrush")  
Rectángulo pintado mediante VisualBrush  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmvisualbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmvisualbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmvisualbrushexampleinline)]  
  
 Para obtener más información sobre <xref:System.Windows.Media.VisualBrush> la clase, vea [pintar con imágenes, dibujos y objetos visuales](painting-with-images-drawings-and-visuals.md).  
  
<a name="paintwithpredefinedbrushesandsystemcolors"></a>   
## <a name="paint-using-predefined-and-system-brushes"></a>Pintar usando predefinidos y pinceles del sistema  
 Para mayor comodidad, Windows Presentation Foundation (WPF) proporciona un conjunto de pinceles de sistema y predefinidos que puede usar para pintar objetos.  
  
- Para obtener una lista de los pinceles predefinidos <xref:System.Windows.Media.Brushes> disponibles, vea la clase. Para ver un ejemplo en el que se muestra cómo usar un pincel predefinido, vea [pintar un área con un color sólido](how-to-paint-an-area-with-a-solid-color.md).  
  
- Para obtener una lista de los pinceles del sistema <xref:System.Windows.SystemColors> disponibles, vea la clase. Para obtener un ejemplo, vea [pintar un área con un pincel del sistema](how-to-paint-an-area-with-a-system-brush.md).  
  
<a name="commonbrushfeatures"></a>   
## <a name="common-brush-features"></a>Características comunes de los pinceles  
 <xref:System.Windows.Media.Brush>los objetos proporcionan <xref:System.Windows.Media.Brush.Opacity%2A> una propiedad que se puede utilizar para hacer que un pincel sea transparente o parcialmente transparente. Un <xref:System.Windows.Media.Brush.Opacity%2A> valor de 0 hace que un pincel sea completamente transparente, <xref:System.Windows.Media.Brush.Opacity%2A> mientras que un valor de 1 hace que un pincel sea completamente opaco. En el ejemplo siguiente se <xref:System.Windows.Media.Brush.Opacity%2A> usa la propiedad para <xref:System.Windows.Media.SolidColorBrush> crear un 25 por ciento opaco.  
  
 [!code-xaml[BrushOverviewExamples_snip#OpacityExample1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/OpacityExample.xaml#opacityexample1xaml)]  
  
 [!code-csharp[BrushOverviewExamples_snip#OpacityExample1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/OpacityExample.cs#opacityexample1csharp)]  
  
 Si el pincel contiene colores que son parcialmente transparentes, el valor de opacidad del color se combina a través de la multiplicación con el valor de opacidad del pincel. Por ejemplo, si un pincel tiene un valor de opacidad de 0,5 y un color usado en el pincel también tiene un valor de opacidad de 0,5, el color de salida tiene un valor de opacidad de 0,25.  
  
> [!NOTE]
> Es más eficaz cambiar el valor de opacidad de un pincel que cambiar la opacidad de un elemento completo mediante su <xref:System.Windows.UIElement.Opacity%2A?displayProperty=nameWithType> propiedad.  
  
 Puede girar, escalar, sesgar y trasladar el contenido de un pincel mediante <xref:System.Windows.Media.Brush.Transform%2A> sus <xref:System.Windows.Media.Brush.RelativeTransform%2A> propiedades o. Para obtener más información, vea [información general sobre la transformación Brush](brush-transformation-overview.md).  
  
 Dado que son <xref:System.Windows.Media.Animation.Animatable> objetos, <xref:System.Windows.Media.Brush> los objetos se pueden animar. Para obtener más información, consulte [Información general sobre animaciones](animation-overview.md).  
  
<a name="freezable_features"></a>   
### <a name="freezable-features"></a>Características de los objetos Freezable  
 Dado que hereda de la <xref:System.Windows.Freezable> clase, la clase proporciona varias características especiales: <xref:System.Windows.Media.Brush> los <xref:System.Windows.Media.Brush> objetos se pueden declarar como [recursos](../advanced/xaml-resources.md), compartirse entre varios objetos y clonados. Además, todos los <xref:System.Windows.Media.Brush> tipos excepto <xref:System.Windows.Media.VisualBrush> se pueden convertir en de solo lectura para mejorar el rendimiento y hacerlos seguros para subprocesos.  
  
 Para obtener más información sobre las diferentes características proporcionadas por <xref:System.Windows.Freezable> los objetos, vea [información general sobre objetos Freezable](../advanced/freezable-objects-overview.md).  
  
 Para obtener más información sobre <xref:System.Windows.Media.VisualBrush> por qué no se pueden inmovilizar los objetos, vea la <xref:System.Windows.Media.VisualBrush> página tipo.  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Media.Brush>
- <xref:System.Windows.Media.Brushes>
- [Información general sobre el dibujo con colores sólidos y degradados](painting-with-solid-colors-and-gradients-overview.md)
- [Pintar con imágenes, dibujos y elementos visuales](painting-with-images-drawings-and-visuals.md)
- [Información general sobre objetos Freezable](../advanced/freezable-objects-overview.md)
- [Ejemplo de pinceles](https://go.microsoft.com/fwlink/?LinkID=159973)
- [Ejemplo de ImageBrush](https://go.microsoft.com/fwlink/?LinkID=160005)
- [Ejemplo de VisualBrush](https://go.microsoft.com/fwlink/?LinkID=160049)
- [Temas "Cómo..."](brushes-how-to-topics.md)
- [Otras recomendaciones de rendimiento](../advanced/optimizing-performance-other-recommendations.md)
