---
title: Patrones de control compatibles en un proveedor de UI Automation
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- control patterns, supporting in UI Automation provider
- UI Automation, supporting control patterns in provider
ms.assetid: 0d635c35-ffa8-4dc8-bbc9-12fcd5445776
ms.openlocfilehash: 67f37dfe1fe63f2130646cb227fec855ccc7bf75
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71042601"
---
# <a name="support-control-patterns-in-a-ui-automation-provider"></a>Patrones de control compatibles en un proveedor de UI Automation

> [!NOTE]
> Esta documentación está dirigida a los desarrolladores de .NET Framework que quieran usar las clases [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] administradas definidas en el espacio de nombres <xref:System.Windows.Automation>. Para obtener la información más [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]reciente acerca [de, consulte API de automatización de Windows: Automatización](https://go.microsoft.com/fwlink/?LinkID=156746)de la interfaz de usuario.

En este tema se muestra cómo implementar uno o varios patrones de control en un proveedor de Automatización de la interfaz de usuario para que las aplicaciones cliente puedan manipular controles y obtener datos de ellos.

## <a name="support-control-patterns"></a>Admitir patrones de control

1. Implemente las interfaces adecuadas para los patrones de control que el elemento debe admitir, como <xref:System.Windows.Automation.Provider.IInvokeProvider> para <xref:System.Windows.Automation.InvokePattern>.

2. Devuelva el objeto que contiene la implementación de cada interfaz de control de la implementación de <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.GetPatternProvider%2A?displayProperty=nameWithType>

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se muestra una implementación de <xref:System.Windows.Automation.Provider.ISelectionProvider> para un cuadro de lista personalizada de selección única. Devuelve tres propiedades y obtiene el elemento actualmente seleccionado.

[!code-csharp[UIAFragmentProvider_snip#119](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAFragmentProvider_snip/CSharp/ListPattern.cs#119)]
[!code-vb[UIAFragmentProvider_snip#119](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAFragmentProvider_snip/VisualBasic/ListPattern.vb#119)]

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se muestra una implementación de <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.GetPatternProvider%2A> que devuelve la clase que implementa <xref:System.Windows.Automation.Provider.ISelectionProvider>. La mayoría de los controles de cuadro de lista también admitirían otros patrones, pero en este ejemplo`Nothing` se devuelve una referencia nula (en Microsoft Visual Basic .net) para los demás identificadores de patrón.

[!code-csharp[UIAFragmentProvider_snip#120](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAFragmentProvider_snip/CSharp/ListFragment.cs#120)]
[!code-vb[UIAFragmentProvider_snip#120](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAFragmentProvider_snip/VisualBasic/ListFragment.vb#120)]

## <a name="see-also"></a>Vea también

- [Información general sobre proveedores de la Automatización de la interfaz de usuario](ui-automation-providers-overview.md)
- [Implementación del proveedor de automatización de la interfaz de usuario en el servidor](server-side-ui-automation-provider-implementation.md)
