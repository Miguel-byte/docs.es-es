---
title: 'Tutorial: Serializar colecciones de tipos estándar con DesignerSerializationVisibilityAttribute'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- serialization [Windows Forms], collections
- standard types [Windows Forms], collections
- collections [Windows Forms], serializing
- collections [Windows Forms], standard types
ms.assetid: 020c9df4-fdc5-4dae-815a-963ecae5668c
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: f051d7a51a5f4ff8debf40fafbb8acfd8f7098f5
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/23/2019
ms.locfileid: "71182628"
---
# <a name="walkthrough-serialize-collections-of-standard-types"></a>Tutorial: Serializar colecciones de tipos estándar

A veces, los controles personalizados exponen una colección como una propiedad. En este tutorial se muestra cómo utilizar <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute> la clase para controlar cómo se serializa una colección en tiempo de diseño. Aplicar el <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute.Content> valor a la propiedad de colección garantiza que se serializará la propiedad.

Para copiar el código de este tema como una sola lista, vea [Cómo: Serializar colecciones de tipos estándar con DesignerSerializationVisibilityAttribute](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/ms171833(v=vs.120)).

## <a name="prerequisites"></a>Requisitos previos

Necesita Visual Studio para completar este tutorial.

## <a name="create-a-control-with-a-serializable-collection"></a>Crear un control con una colección serializable

El primer paso es crear un control que tenga una colección serializable como una propiedad. Puede editar el contenido de esta colección mediante el editor de la **colección**, al que puede tener acceso desde la ventana **propiedades** .

1. En Visual Studio, cree un proyecto de biblioteca de controles de Windows y asígnele el nombre **SerializationDemoControlLib**.

2. Cambie el `UserControl1` nombre `SerializationDemoControl`a. Para obtener más información, vea [cambiar el nombre de una refactorización de símbolo de código](/visualstudio/ide/reference/rename).

3. En la ventana **propiedades** , establezca el valor de la <xref:System.Windows.Forms.Padding.All%2A?displayProperty=nameWithType> propiedad en **10**.

4. Coloque un <xref:System.Windows.Forms.TextBox> control `SerializationDemoControl`en.

5. Seleccione el control <xref:System.Windows.Forms.TextBox>. En la ventana **propiedades** , establezca las siguientes propiedades.

    |Propiedad.|Cambiar a|
    |--------------|---------------|
    |**Multiline**|`true`|
    |**Anclaje**|<xref:System.Windows.Forms.DockStyle.Fill>|
    |**ScrollBars**|<xref:System.Windows.Forms.ScrollBars.Vertical>|
    |**ReadOnly**|`true`|

6. En el **Editor de código**, declare un campo de `stringsValue` matriz `SerializationDemoControl`de cadenas denominado en.

     [!code-cpp[System.ComponentModel.DesignerSerializationVisibilityAttribute#4](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/cpp/form1.cpp#4)]
     [!code-csharp[System.ComponentModel.DesignerSerializationVisibilityAttribute#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/CS/form1.cs#4)]
     [!code-vb[System.ComponentModel.DesignerSerializationVisibilityAttribute#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/VB/form1.vb#4)]

7. Defina la `Strings` propiedad `SerializationDemoControl`en.

   > [!NOTE]
   > El <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute.Content> valor se utiliza para habilitar la serialización de la colección.

   [!code-cpp[System.ComponentModel.DesignerSerializationVisibilityAttribute#5](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/cpp/form1.cpp#5)]
   [!code-csharp[System.ComponentModel.DesignerSerializationVisibilityAttribute#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/CS/form1.cs#5)]
   [!code-vb[System.ComponentModel.DesignerSerializationVisibilityAttribute#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/VB/form1.vb#5)]

8. Presione **F5** para compilar el proyecto y ejecutar el control en **UserControl Test Container**.

9. Busque la propiedad **Strings** en el <xref:System.Windows.Forms.PropertyGrid> de **UserControl Test Container**. Seleccione la **propiedad cadenas** y, a continuación, seleccione![los puntos suspensivos (el botón de puntos suspensivos (...)](./media/visual-studio-ellipsis-button.png)en el botón ventana Propiedades de Visual Studio) para abrir el editor de la **colección de cadenas**.

10. Escriba varias cadenas en el **Editor de colección de cadenas**. Sepárelos presionando la tecla **entrar** al final de cada cadena. Haga clic en **Aceptar** cuando haya terminado de escribir las cadenas.

   > [!NOTE]
   > Las cadenas que escribió aparecen en el <xref:System.Windows.Forms.TextBox> `SerializationDemoControl`del.

## <a name="serialize-a-collection-property"></a>Serializar una propiedad de colección

Para probar el comportamiento de la serialización del control, lo colocará en un formulario y cambiará el contenido de la colección con el editor de la **colección**. Puede ver el estado de la colección serializada examinando un archivo de diseñador especial en el que el **Diseñador de Windows Forms** emite el código.

1. Agregue un proyecto de aplicación para Windows a la solución. Dé un nombre al proyecto `SerializationDemoControlTest`.

2. En el **cuadro de herramientas**, busque la pestaña denominada **SerializationDemoControlLib Components**. En esta pestaña encontrará el `SerializationDemoControl`. Para obtener más información, vea [Tutorial: Rellenar automáticamente el cuadro de](walkthrough-automatically-populating-the-toolbox-with-custom-components.md)herramientas con componentes personalizados.

3. Coloque un `SerializationDemoControl` en el formulario.

4. Busque la `Strings` propiedad en la ventana **propiedades** . Haga clic `Strings` en la propiedad y, después,![haga clic en los puntos suspensivos (el botón de puntos suspensivos (..](./media/visual-studio-ellipsis-button.png).) en el botón ventana Propiedades de Visual Studio) para abrir el editor de la **colección de cadenas**.

5. Escriba varias cadenas en el **Editor**de la colección de cadenas. Sepárelos presionando **entrar** al final de cada cadena. Haga clic en **Aceptar** cuando haya terminado de escribir las cadenas.

    > [!NOTE]
    > Las cadenas que escribió aparecen en el <xref:System.Windows.Forms.TextBox> `SerializationDemoControl`del.

6. En el **Explorador de soluciones**, haga clic en el botón **Mostrar todos los archivos**.

7. Abra el nodo **Form1** . Debajo, se trata de un archivo denominado **Form1.Designer.CS** o **Form1. Designer. VB**. Este es el archivo en el que el **Diseñador de Windows Forms** emite código que representa el estado de tiempo de diseño del formulario y sus controles secundarios. Abra este archivo en el **Editor de código**.

8. Abra la región denominada **código generado por el diseñador de Windows Forms** y busque la sección con la etiqueta **serializationDemoControl1**. Debajo de esta etiqueta se encuentra el código que representa el estado serializado del control. Las cadenas que escribió en el paso 5 aparecen en una asignación a la `Strings` propiedad. En los siguientes ejemplos de C# código de y Visual Basic, se muestra código similar al que se verá si se escriben las cadenas "red", "naranja" y "amarillo".

    ```csharp
    this.serializationDemoControl1.Strings = new string[] {
            "red",
            "orange",
            "yellow"};
    ```

    ```vb
    Me.serializationDemoControl1.Strings = New String() {"red", "orange", "yellow"}
    ```

9. En el **Editor de código**, cambie el valor de <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute> en la `Strings` propiedad a <xref:System.ComponentModel.DesignerSerializationVisibility.Hidden>.

    ```csharp
    [DesignerSerializationVisibility(DesignerSerializationVisibility.Hidden)]
    ```

    ```vb
    <DesignerSerializationVisibility(DesignerSerializationVisibility.Hidden)> _
    ```

10. Recompile la solución y repita los pasos 3 y 4.

> [!NOTE]
> En este caso, el **Diseñador de Windows Forms** no emite ninguna asignación a la `Strings` propiedad.

## <a name="next-steps"></a>Pasos siguientes

Una vez que sepa cómo serializar una colección de tipos estándar, considere la posibilidad de integrar los controles personalizados más profundamente en el entorno en tiempo de diseño. En los temas siguientes se describe cómo mejorar la integración en tiempo de diseño de los controles personalizados:

- [Arquitectura en tiempo de diseño](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/c5z9s1h4(v=vs.120))

- [Atributos en controles de Windows Forms](attributes-in-windows-forms-controls.md)

- [Información general sobre la serialización del diseñador](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/ms171834(v=vs.120))

- [Tutorial: Crear un control de Windows Forms que aprovecha las características en tiempo de diseño de Visual Studio](creating-a-wf-control-design-time-features.md)

## <a name="see-also"></a>Vea también

- <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute>
- [Tutorial: Rellenar automáticamente el cuadro de herramientas con componentes personalizados](walkthrough-automatically-populating-the-toolbox-with-custom-components.md)
