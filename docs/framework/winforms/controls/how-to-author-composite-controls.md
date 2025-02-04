---
title: Procedimiento para crear controles compuestos
ms.date: 03/30/2017
helpviewer_keywords:
- UserControl class [Windows Forms], creating composite controls
- user controls [Windows Forms], creating
- user controls [Windows Forms], inheriting from
- composite controls [Windows Forms], creating
ms.assetid: 79c9cf05-5ab6-4a18-886d-88a64748b098
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 08cb07ceebf08b3096415f9b7370e2d955152cb6
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015932"
---
# <a name="how-to-author-composite-controls"></a>Procedimiento Crear controles compuestos

Los controles compuestos pueden emplearse de muchas formas. Puede crearlos como parte de un proyecto de aplicación de escritorio de Windows y utilizarlos solo en formularios del proyecto. También podría crearlos en un proyecto de Biblioteca de controles de Windows, compilar el proyecto en un ensamblado y utilizar los controles en otros proyectos. Incluso puede heredar de ellos y utilizar la herencia visual para personalizarlos rápidamente para fines especiales.

## <a name="to-author-a-composite-control"></a>Para crear un control compuesto

1. En Visual Studio, cree un nuevo proyecto de **aplicación para Windows** y asígnele el nombre **DemoControlHost**.

2. En el menú **Proyecto** , haga clic en **Agregar control de usuario**.

3. En el cuadro de diálogo **Agregar nuevo elemento**, dé al archivo de clase (archivo .vb o .cs) el nombre que desea para el control compuesto.

4. Seleccione el botón **Agregar** para crear el archivo de clase para el control compuesto.

5. Agregue controles del **Cuadro de herramientas** a la superficie del control compuesto.

6. Escriba código en los procedimientos de evento para controlar los eventos que produzca el control compuesto o sus controles constituyentes.

7. Cierre el diseñador para el control compuesto y guarde el archivo cuando se le indique.

8. En el menú **Compilar** , haga clic en **Compilar solución**.

     Para que los controles personalizados aparezcan en el **Cuadro de herramientas**, deberá compilar el proyecto.

9. Use la pestaña **DemoControlHost** del **Cuadro de herramientas** para agregar instancias del control a `Form1`.

## <a name="to-author-a-control-class-library"></a>Para crear una biblioteca de clases de controles

1. Abra un nuevo proyecto de tipo **Biblioteca de controles de Windows**.

     De forma predeterminada, el proyecto contiene un control compuesto.

2. Agregue controles y código como se describió en el procedimiento anterior.

3. Elija un control cuyas clases de herencia no desee que cambien y establezca la propiedad **Modifiers** de este control en **Private**.

4. Compile el archivo DLL.

## <a name="to-inherit-from-a-composite-control-in-a-control-class-library"></a>Para heredar de un control compuesto de una biblioteca de clases de controles

1. En el menú **Archivo**, seleccione **Agregar** y **Nuevo proyecto** para agregar un nuevo proyecto **Aplicación Windows** a la solución.

2. En el **Explorador de soluciones**, haga clic con el botón derecho en la carpeta **Referencias** del nuevo proyecto y elija **Agregar referencia** para abrir el cuadro de diálogo **Agregar referencia**.

3. Seleccione la pestaña **Proyectos** y haga doble clic en el proyecto de Biblioteca de controles.

4. En el menú **Compilar** , haga clic en **Compilar solución**.

5. En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto de Biblioteca de controles y elija **Agregar nuevo elemento** en el menú contextual.

6. Seleccione la plantilla **Control de usuario heredado** en el cuadro de diálogo **Agregar nuevo elemento**.

7. En el cuadro de diálogo **Selector de herencia**, haga doble clic en el control del que desea heredar.

     Se agrega un nuevo control al proyecto.

8. Abra el diseñador visual para el nuevo control y agregue controles constituyentes adicionales.

     Puede ver los controles constituyentes heredados del control de usuario en la DLL, así como alterar las propiedades de aquellos controles cuya propiedad **Modifiers** sea **Public**. En cambio, no puede cambiar las propiedades del control cuya propiedad **Modifiers** sea **Private**.

## <a name="see-also"></a>Vea también

- [Tutorial: Crear un control compuesto](walkthrough-authoring-a-composite-control-with-visual-csharp.md)
- [Tutorial: Heredar de un control Windows Forms](walkthrough-inheriting-from-a-windows-forms-control-with-visual-csharp.md)
- [Recomendaciones sobre tipos de controles](control-type-recommendations.md)
- [Cómo: Controles de autor para Windows Forms](how-to-author-controls-for-windows-forms.md)
- [Variedades de controles personalizados](varieties-of-custom-controls.md)
