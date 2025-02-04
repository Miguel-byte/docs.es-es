---
title: Procedimiento para implementar la validación con el control DataGrid
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGrid [WPF], validation
- validation [WPF], DataGrid
ms.assetid: ec6078a8-1e42-4648-b414-f4348e81bda1
ms.openlocfilehash: 8ae651b3085b39673a51cf8d5f65e9bfb9da87d7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962039"
---
# <a name="how-to-implement-validation-with-the-datagrid-control"></a>Procedimiento para implementar la validación con el control DataGrid
El <xref:System.Windows.Controls.DataGrid> control permite realizar la validación en el nivel de celda y de fila. Con la validación de nivel de celda, se validan las propiedades individuales de un objeto de datos enlazado cuando un usuario actualiza un valor. Con la validación de nivel de fila, se validan los objetos de datos completos cuando un usuario confirma los cambios en una fila. También puede proporcionar comentarios visuales personalizados para los errores de validación o usar los comentarios visuales predeterminados <xref:System.Windows.Controls.DataGrid> que proporciona el control.  
  
 Los procedimientos siguientes describen cómo aplicar reglas de validación a <xref:System.Windows.Controls.DataGrid> los enlaces y personalizar los comentarios visuales.  
  
### <a name="to-validate-individual-cell-values"></a>Para validar valores de celda individuales  
  
- Especifique una o varias reglas de validación en el enlace utilizado con una columna. Esto es similar a la validación de datos en controles simples, como se describe en [información general sobre el enlace de datos](../data/data-binding-overview.md).  
  
     En el ejemplo siguiente se <xref:System.Windows.Controls.DataGrid> muestra un control con cuatro columnas enlazadas a diferentes propiedades de un objeto comercial. Tres de las columnas especifican <xref:System.Windows.Controls.ExceptionValidationRule> estableciendo la <xref:System.Windows.Data.Binding.ValidatesOnExceptions%2A> propiedad en `true`.  
  
     [!code-xaml[DataGrid_Validation#BasicXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/window1.xaml#basicxaml)]  
  
     Cuando un usuario escribe un valor no válido (como un entero en la columna ID. de curso), aparece un borde rojo alrededor de la celda. Puede cambiar estos comentarios de validación predeterminados tal y como se describe en el procedimiento siguiente.  
  
### <a name="to-customize-cell-validation-feedback"></a>Para personalizar los comentarios de validación de celda  
  
- Establezca la propiedad de <xref:System.Windows.Controls.DataGridBoundColumn.EditingElementStyle%2A> la columna en un estilo apropiado para el control de edición de la columna. Dado que los controles de edición se crean en tiempo de ejecución, no <xref:System.Windows.Controls.Validation.ErrorTemplate%2A?displayProperty=nameWithType> puede usar la propiedad adjunta como lo haría con los controles simples.  
  
     En el ejemplo siguiente se actualiza el ejemplo anterior agregando un estilo de error compartido por las tres columnas con reglas de validación. Cuando un usuario escribe un valor no válido, el estilo cambia el color de fondo de la celda y agrega una información sobre herramientas. Tenga en cuenta el uso de un desencadenador para determinar si hay un error de validación. Esto es necesario porque actualmente no hay ninguna plantilla de error dedicada para las celdas.  
  
     [!code-xaml[DataGrid_Validation#CellValidationXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#cellvalidationxaml)]  
  
     Puede implementar una personalización más amplia reemplazando la <xref:System.Windows.Controls.DataGridColumn.CellStyle%2A> utilizada por la columna.  
  
### <a name="to-validate-multiple-values-in-a-single-row"></a>Para validar varios valores en una sola fila  
  
1. Implemente <xref:System.Windows.Controls.ValidationRule> una subclase que compruebe varias propiedades del objeto de datos enlazado. En la <xref:System.Windows.Controls.ValidationRule.Validate%2A> implementación del método, convierta el valor del <xref:System.Windows.Data.BindingGroup> `value` parámetro en una instancia de. A continuación, puede tener acceso al objeto de <xref:System.Windows.Data.BindingGroup.Items%2A> datos a través de la propiedad.  
  
     En el ejemplo siguiente se muestra este proceso para validar `StartDate` si el valor de `Course` propiedad de un objeto es `EndDate` anterior al valor de su propiedad.  
  
     [!code-csharp[DataGrid_Validation#CourseValidationRule](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml.cs#coursevalidationrule)]
     [!code-vb[DataGrid_Validation#CourseValidationRule](~/samples/snippets/visualbasic/VS_Snippets_Wpf/datagrid_validation/vb/mainwindow.xaml.vb#coursevalidationrule)]  
  
2. Agregue la regla de validación a <xref:System.Windows.Controls.DataGrid.RowValidationRules%2A?displayProperty=nameWithType> la colección. La <xref:System.Windows.Controls.DataGrid.RowValidationRules%2A> propiedad proporciona acceso directo a la <xref:System.Windows.Data.BindingGroup.ValidationRules%2A> propiedad de una <xref:System.Windows.Data.BindingGroup> instancia de que agrupa todos los enlaces utilizados por el control.  
  
     En el ejemplo siguiente se <xref:System.Windows.Controls.DataGrid.RowValidationRules%2A> establece la propiedad en XAML. La <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> propiedad se establece en <xref:System.Windows.Controls.ValidationStep.UpdatedValue> para que la validación se produzca solo después de que se actualice el objeto de datos enlazado.  
  
     [!code-xaml[DataGrid_Validation#RowValidationRulesXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#rowvalidationrulesxaml)]  
  
     Cuando un usuario especifica una fecha de finalización anterior a la fecha de inicio, aparece un signo de exclamación rojo (!) en el encabezado de fila. Puede cambiar estos comentarios de validación predeterminados tal y como se describe en el procedimiento siguiente.  
  
### <a name="to-customize-row-validation-feedback"></a>Para personalizar los comentarios de validación de filas  
  
- Establecer la propiedad <xref:System.Windows.Controls.DataGrid.RowValidationErrorTemplate%2A?displayProperty=nameWithType>. Esta propiedad le permite personalizar los comentarios de la validación de <xref:System.Windows.Controls.DataGrid> filas para los controles individuales. También puede afectar a varios controles mediante el uso de un estilo de fila implícito <xref:System.Windows.Controls.DataGridRow.ValidationErrorTemplate%2A?displayProperty=nameWithType> para establecer la propiedad.  
  
     En el ejemplo siguiente se reemplazan los comentarios de validación de filas predeterminados por un indicador más visible. Cuando un usuario escribe un valor no válido, aparece un círculo rojo con un signo de exclamación blanco en el encabezado de fila. Esto sucede en los errores de validación de filas y celdas. El mensaje de error asociado se muestra en una información sobre herramientas.  
  
     [!code-xaml[DataGrid_Validation#RowValidationFeedbackXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#rowvalidationfeedbackxaml)]  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se proporciona una demostración completa de la validación de celdas y filas. La `Course` clase proporciona un objeto de datos de ejemplo que <xref:System.ComponentModel.IEditableObject> implementa para admitir transacciones. El <xref:System.Windows.Controls.DataGrid> control interactúa con <xref:System.ComponentModel.IEditableObject> para permitir que los usuarios reviertan los cambios presionando la tecla ESC.  
  
> [!NOTE]
> Si está utilizando Visual Basic, en la primera línea de MainWindow. XAML, reemplace `x:Class="DataGridValidation.MainWindow"` por. `x:Class="MainWindow"`  
  
 Para probar la validación, intente lo siguiente:  
  
- En la columna ID. de curso, escriba un valor que no sea entero.  
  
- En la columna fecha de finalización, escriba una fecha anterior a la fecha de inicio.  
  
- Elimine el valor de ID. de curso, fecha de inicio o fecha de finalización.  
  
- Para deshacer un valor de celda no válido, vuelva a colocar el cursor en la celda y presione la tecla ESC.  
  
- Para deshacer los cambios de una fila completa cuando la celda actual está en modo de edición, presione la tecla ESC dos veces.  
  
- Cuando se produzca un error de validación, mueva el puntero del mouse sobre el indicador del encabezado de fila para ver el mensaje de error asociado.  
  
 [!code-csharp[DataGrid_Validation#FullCode](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml.cs#fullcode)]
 [!code-vb[DataGrid_Validation#FullCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/datagrid_validation/vb/mainwindow.xaml.vb#fullcode)]  
  
 [!code-xaml[DataGrid_Validation#FullXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#fullxaml)]  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Controls.DataGrid>
- [DataGrid](datagrid.md)
- [Enlace de datos](../data/data-binding-wpf.md)
- [Implementar la validación de enlaces](../data/how-to-implement-binding-validation.md)
- [Implementar lógica de validación en objetos personalizados](../data/how-to-implement-validation-logic-on-custom-objects.md)
