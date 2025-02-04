---
title: Utilizar el almacenamiento en caché en la UI Automation
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- caching, UI Automation
- UI Automation, caching
ms.assetid: ec722dff-6009-4279-b86a-e18d3fa94ebf
ms.openlocfilehash: dd7506d388ba215f671ee3c7c4bae09baf4cc2b3
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71040305"
---
# <a name="use-caching-in-ui-automation"></a>Utilizar el almacenamiento en caché en la UI Automation
> [!NOTE]
> Esta documentación está dirigida a los desarrolladores de .NET Framework que quieran usar las clases [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] administradas definidas en el espacio de nombres <xref:System.Windows.Automation>. Para obtener la información más [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]reciente acerca [de, consulte API de automatización de Windows: Automatización](https://go.microsoft.com/fwlink/?LinkID=156746)de la interfaz de usuario.  
  
 En esta sección se muestra cómo implementar el almacenamiento en caché de patrones de control y propiedades de <xref:System.Windows.Automation.AutomationElement> .  
  
### <a name="activate-a-cache-request"></a>Activar una solicitud de almacenamiento en caché  
  
1. Creará un control <xref:System.Windows.Automation.CacheRequest>.  
  
2. Especifique las propiedades y los patrones que se almacenarán en caché mediante el uso de <xref:System.Windows.Automation.CacheRequest.Add%2A>.  
  
3. Especifique el ámbito del almacenamiento en caché estableciendo la propiedad <xref:System.Windows.Automation.CacheRequest.TreeScope%2A> .  
  
4. Especifique la vista del subárbol estableciendo la propiedad <xref:System.Windows.Automation.CacheRequest.TreeFilter%2A> .  
  
5. Establezca la propiedad <xref:System.Windows.Automation.CacheRequest.AutomationElementMode%2A> en <xref:System.Windows.Automation.AutomationElementMode.None> si quiere aumentar la eficacia sin recuperar una referencia completa a objetos. (Esto hará que no sea posible recuperar los valores actuales de esos objetos).  
  
6. Active la solicitud mediante el <xref:System.Windows.Automation.CacheRequest.Activate%2A> uso de `using` dentro de`Using` un bloque (en Microsoft Visual Basic .net).  
  
 Después de obtener objetos <xref:System.Windows.Automation.AutomationElement> o de suscribirse a eventos, desactive la solicitud mediante <xref:System.Windows.Automation.CacheRequest.Pop%2A> (si se usó <xref:System.Windows.Automation.CacheRequest.Push%2A> ) o eliminando el objeto creado por <xref:System.Windows.Automation.CacheRequest.Activate%2A>. (Utilice <xref:System.Windows.Automation.CacheRequest.Activate%2A> en un `using` bloque (`Using` en Microsoft Visual Basic .net).  
  
### <a name="cache-automationelement-properties"></a>Propiedades de AutomationElement de almacenamiento en caché  
  
1. Mientras un elemento <xref:System.Windows.Automation.CacheRequest> está activo, obtenga objetos <xref:System.Windows.Automation.AutomationElement> mediante <xref:System.Windows.Automation.AutomationElement.FindFirst%2A> o <xref:System.Windows.Automation.AutomationElement.FindAll%2A>; u obtenga un elemento <xref:System.Windows.Automation.AutomationElement> como el origen de un evento para el que se registró para cuando el elemento <xref:System.Windows.Automation.CacheRequest> estaba activo. (También puede crear una caché pasando un elemento <xref:System.Windows.Automation.CacheRequest> a GetUpdatedCache o uno de los métodos <xref:System.Windows.Automation.TreeWalker> ).  
  
2. Use <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A> o recupere una propiedad desde la propiedad <xref:System.Windows.Automation.AutomationElement.Cached%2A> del elemento <xref:System.Windows.Automation.AutomationElement>.  
  
### <a name="obtain-cached-patterns-and-their-properties"></a>Obtener patrones almacenados en caché y sus propiedades  
  
1. Mientras un elemento <xref:System.Windows.Automation.CacheRequest> está activo, obtenga objetos <xref:System.Windows.Automation.AutomationElement> mediante <xref:System.Windows.Automation.AutomationElement.FindFirst%2A> o <xref:System.Windows.Automation.AutomationElement.FindAll%2A>; u obtenga un elemento <xref:System.Windows.Automation.AutomationElement> como el origen de un evento para el que se registró para cuando el elemento <xref:System.Windows.Automation.CacheRequest> estaba activo. (También puede crear una caché pasando un elemento <xref:System.Windows.Automation.CacheRequest> a GetUpdatedCache o uno de los métodos <xref:System.Windows.Automation.TreeWalker> ).  
  
2. Use <xref:System.Windows.Automation.AutomationElement.GetCachedPattern%2A> o <xref:System.Windows.Automation.AutomationElement.TryGetCachedPattern%2A> para recuperar un patrón almacenado en caché.  
  
3. Recupere valores de propiedad de la propiedad `Cached` del patrón de control.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo de código siguiente se muestran varios aspectos del almacenamiento en caché en los que se usa <xref:System.Windows.Automation.CacheRequest.Activate%2A> para activar el elemento <xref:System.Windows.Automation.CacheRequest>.  
  
 [!code-csharp[UIAClient_snip#107](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#107)]
 [!code-vb[UIAClient_snip#107](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#107)]  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo de código siguiente se muestran varios aspectos del almacenamiento en caché en los que se usa <xref:System.Windows.Automation.CacheRequest.Push%2A> para activar el elemento <xref:System.Windows.Automation.CacheRequest>. Excepto cuando quiera anidar solicitudes de almacenamiento en caché, es preferible utilizar <xref:System.Windows.Automation.CacheRequest.Activate%2A>.  
  
 [!code-csharp[UIAClient_snip#108](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#108)]
 [!code-vb[UIAClient_snip#108](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#108)]  
  
## <a name="see-also"></a>Vea también

- [Almacenamiento en caché en los clientes de Automatización de la interfaz de usuario](caching-in-ui-automation-clients.md)
