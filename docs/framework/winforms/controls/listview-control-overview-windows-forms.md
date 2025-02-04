---
title: Información general del control ListView (Formularios Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- ListView
helpviewer_keywords:
- lists
- ListView control [Windows Forms], about ListView control
- list views
ms.assetid: c9ef56c1-3bb1-4101-9f4e-e95e720f2756
ms.openlocfilehash: 7b7eac942a7e857ad731c0f77389e84aee287c08
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69952165"
---
# <a name="listview-control-overview-windows-forms"></a>Información general del control ListView (Formularios Windows Forms)
El control <xref:System.Windows.Forms.ListView> de Windows Forms muestra una lista de elementos con iconos. Puede usar una vista de lista para crear una interfaz de usuario similar al panel derecho del Explorador de Windows. El control tiene cuatro modos de vista: LargeIcon, SmallIcon, List y details.  
  
## <a name="what-you-can-do-with-the-listview-control"></a>Qué puede hacer con el control ListView  
  
> [!NOTE]
> Un modo de vista adicional, mosaico, solo está disponible en Windows XP y en el sistema operativo Windows Server 2003. Para obtener más información, vea [Cómo: Habilitar la vista en mosaico en un control](how-to-enable-tile-view-in-a-windows-forms-listview-control.md)ListView Windows Forms.  
  
 El modo LargeIcon muestra iconos grandes junto al texto del elemento; los elementos aparecen en varias columnas si el control es suficientemente grande. El modo SmallIcon es el mismo, salvo que muestra iconos pequeños. El modo de lista muestra iconos pequeños, pero siempre está en una sola columna. El modo de detalles muestra los elementos en varias columnas. Para obtener más detalles, vea [Cómo: Agregue columnas al control](how-to-add-columns-to-the-windows-forms-listview-control.md)ListView de Windows Forms. La <xref:System.Windows.Forms.ListView.View%2A> propiedad determina el modo de vista. Todos los modos de vista pueden mostrar imágenes de las listas de imágenes. Para obtener más detalles, vea [Cómo: Mostrar iconos del control](how-to-display-icons-for-the-windows-forms-listview-control.md)ListView de Windows Forms.  
  
 En la tabla siguiente se enumeran <xref:System.Windows.Forms.ListView> algunos de los miembros y las vistas en las que son válidos.  
  
|Miembro de ListView|Ver|  
|---------------------|----------|  
|Propiedad<xref:System.Windows.Forms.ListView.Alignment%2A>|<xref:System.Windows.Forms.View.SmallIcon> o <xref:System.Windows.Forms.View.LargeIcon>|  
|Propiedad<xref:System.Windows.Forms.ListView.AutoArrange%2A>|<xref:System.Windows.Forms.View.SmallIcon> o <xref:System.Windows.Forms.View.LargeIcon>|  
|Método <xref:System.Windows.Forms.ListView.AutoResizeColumn%2A>|<xref:System.Windows.Forms.View.Details>|  
|Propiedad<xref:System.Windows.Forms.ListView.Columns%2A>|<xref:System.Windows.Forms.View.Details> o <xref:System.Windows.Forms.View.Tile>|  
|Evento<xref:System.Windows.Forms.ListView.DrawSubItem>|<xref:System.Windows.Forms.View.Details>|  
|Método <xref:System.Windows.Forms.ListView.FindItemWithText%2A>|<xref:System.Windows.Forms.View.Details>, <xref:System.Windows.Forms.View.List>o <xref:System.Windows.Forms.View.Tile>|  
|Método <xref:System.Windows.Forms.ListView.FindNearestItem%2A>|<xref:System.Windows.Forms.View.SmallIcon> o <xref:System.Windows.Forms.View.LargeIcon>|  
|Método <xref:System.Windows.Forms.ListView.GetItemAt%2A>|<xref:System.Windows.Forms.View.Details> o <xref:System.Windows.Forms.View.Tile>|  
|Propiedad<xref:System.Windows.Forms.ListView.Groups%2A>|Todas las vistas excepto<xref:System.Windows.Forms.View.List>|  
|Propiedad<xref:System.Windows.Forms.ListView.HeaderStyle%2A>|<xref:System.Windows.Forms.View.Details>|  
|Propiedad<xref:System.Windows.Forms.ListView.InsertionMark%2A>|<xref:System.Windows.Forms.View.LargeIcon>, <xref:System.Windows.Forms.View.SmallIcon>o <xref:System.Windows.Forms.View.Tile>|  
  
 La propiedad clave del <xref:System.Windows.Forms.ListView> control es <xref:System.Windows.Forms.ListView.Items%2A>, que contiene los elementos mostrados por el control. La <xref:System.Windows.Forms.ListView.SelectedItems%2A> propiedad contiene una colección de los elementos seleccionados actualmente en el control. El usuario puede seleccionar varios elementos, por ejemplo, para arrastrar y colocar varios elementos a la vez en otro control, si <xref:System.Windows.Forms.ListView.MultiSelect%2A> la propiedad está establecida `true`en. El <xref:System.Windows.Forms.ListView> control puede mostrar las casillas junto a los elementos si <xref:System.Windows.Forms.ListView.CheckBoxes%2A> la propiedad está establecida `true`en.  
  
 La <xref:System.Windows.Forms.ListView.Activation%2A> propiedad determina el tipo de acción que el usuario debe realizar para activar un elemento de la lista: las opciones <xref:System.Windows.Forms.ItemActivation.Standard>son <xref:System.Windows.Forms.ItemActivation.OneClick>, y <xref:System.Windows.Forms.ItemActivation.TwoClick>. <xref:System.Windows.Forms.ItemActivation.OneClick>la activación requiere un solo clic para activar el elemento. <xref:System.Windows.Forms.ItemActivation.TwoClick>la activación requiere que el usuario haga doble clic para activar el elemento; un solo clic cambia el color del texto del elemento. <xref:System.Windows.Forms.ItemActivation.Standard>la activación requiere que el usuario haga doble clic para activar un elemento, pero el elemento no cambia de apariencia.  
  
 El <xref:System.Windows.Forms.ListView> control también admite los estilos visuales y otras características disponibles en la plataforma Windows XP, incluida la agrupación, la vista de mosaico y las marcas de inserción.  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Forms.ListView>
- [ListView (Control)](listview-control-windows-forms.md)
- [Cómo: Agregar y quitar elementos con el control ListView de Windows Forms](how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)
- [Procedimientos: Agregar columnas al control Windows Forms ListView](how-to-add-columns-to-the-windows-forms-listview-control.md)
- [Cómo: Mostrar iconos del control ListView de Windows Forms](how-to-display-icons-for-the-windows-forms-listview-control.md)
- [Cómo: Mostrar subelementos en columnas con el control ListView Windows Forms](how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md)
- [Procedimientos: Seleccionar un elemento en el control Windows Forms ListView](how-to-select-an-item-in-the-windows-forms-listview-control.md)
- [Procedimientos: Agrupar elementos en un control Windows Forms ListView](how-to-group-items-in-a-windows-forms-listview-control.md)
- [Cómo: Mostrar una marca de inserción en un control ListView Windows Forms](how-to-display-an-insertion-mark-in-a-windows-forms-listview-control.md)
- [Cómo: Agregar capacidades de búsqueda a un control ListView](how-to-add-search-capabilities-to-a-listview-control.md)
- [Procedimientos: Agregar información personalizada a un control TreeView o ListView (Windows Forms)](add-custom-information-to-a-treeview-or-listview-control-wf.md)
- [Cómo: Cree una interfaz de usuario de MULTIPANEL con Windows Forms](how-to-create-a-multipane-user-interface-with-windows-forms.md)
