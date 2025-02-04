---
title: Procedimiento Filtrar los resultados de una consulta mediante LINQ (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- filtering [Visual Basic]
- filtering data [LINQ in Visual Basic]
- filtering [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], filtering results
- querying databases [LINQ]
- queries [LINQ in Visual Basic], how-to topics
- query samples [Visual Basic]
- filtering data [Visual Basic]
ms.assetid: ef103092-9bed-4134-97f4-2db696e83c12
ms.openlocfilehash: 1250f2fe0ccd7661b9bc1986000143ec4a15a9f0
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053290"
---
# <a name="how-to-filter-query-results-by-using-linq-visual-basic"></a>Procedimiento Filtrar los resultados de una consulta mediante LINQ (Visual Basic)

Language-Integrated Query (LINQ) facilita el acceso a la información de base de datos y la ejecución de consultas.

En el ejemplo siguiente se muestra cómo crear una nueva aplicación que realiza consultas en una base de datos de SQL Server y filtra los resultados por un valor `Where` determinado mediante la cláusula. Para obtener más información, vea [cláusula WHERE](../../../../visual-basic/language-reference/queries/where-clause.md).

En los ejemplos de este tema se utiliza la base de datos de ejemplo Northwind. Si no tiene esta base de datos en el equipo de desarrollo, puede descargarla desde el centro de descarga de Microsoft. Para obtener instrucciones, consulte [Descargar bases de datos de ejemplo](../../../../framework/data/adonet/sql/linq/downloading-sample-databases.md).

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

## <a name="to-create-a-connection-to-a-database"></a>Para crear una conexión a una base de datos

1. En Visual Studio, Abra **Explorador de servidores**/**Explorador de bases de datos** haciendo clic en **Explorador de servidores**/**Explorador de bases de datos** en el menú **Ver** .

2. Haga clic con el botón secundario en **conexiones de datos** en **Explorador de servidores**/**Explorador de bases de datos** y, a continuación, haga clic en **Agregar conexión**.

3. Especifique una conexión válida a la base de datos de ejemplo Northwind.

## <a name="to-add-a-project-that-contains-a-linq-to-sql-file"></a>Para agregar un proyecto que contiene un archivo LINQ to SQL

1. En el menú **Archivo** de Visual Studio, apunte a **Nuevo** y haga clic en **Proyecto**. Seleccione Visual Basic **aplicación de Windows Forms** como el tipo de proyecto.

2. En el menú **Proyecto** , haga clic en **Agregar nuevo elemento**. Seleccione la plantilla de elementos **LINQ to SQL clases** .

3. Asigne al archivo el nombre `northwind.dbml`. Haga clic en **Agregar**. Se abre el Object Relational Designer (Object Relational Designer) para el archivo Northwind. dbml.

## <a name="to-add-tables-to-query-to-the-or-designer"></a>Para agregar tablas que se van a consultar en Object Relational Designer

1. En **Explorador de servidores**/**Explorador de bases de datos**, expanda la conexión a la base de datos Northwind. Expanda la carpeta **tablas** .

     Si ha cerrado el Object Relational Designer, puede volver a abrirlo si hace doble clic en el archivo Northwind. dbml que agregó anteriormente.

2. Haga clic en la tabla Customers y arrástrela hasta el panel izquierdo del diseñador. Haga clic en la tabla Orders y arrástrela hasta el panel izquierdo del diseñador.

     El diseñador crea objetos `Customer` y `Order` nuevos para el proyecto. Observe que el diseñador detecta automáticamente las relaciones entre las tablas y crea las propiedades secundarias de los objetos relacionados. Por ejemplo, IntelliSense mostrará que el `Customer` objeto tiene una `Orders` propiedad para todos los pedidos relacionados con ese cliente.

3. Guarde los cambios y cierre el diseñador.

4. Guarde el proyecto.

## <a name="to-add-code-to-query-the-database-and-display-the-results"></a>Para agregar código para consultar la base de datos y mostrar los resultados

1. En el **cuadro de herramientas**, <xref:System.Windows.Forms.DataGridView> arrastre un control al formulario de Windows Forms predeterminado para el proyecto, Form1.

2. Haga doble clic en Form1 para agregar código al `Load` evento del formulario.

3. Al agregar tablas a Object Relational Designer, el diseñador agregó un <xref:System.Data.Linq.DataContext> objeto para el proyecto. Este objeto contiene el código que debe tener para obtener acceso a esas tablas, además de colecciones y objetos individuales para cada tabla. El <xref:System.Data.Linq.DataContext> nombre del objeto para el proyecto se basa en el nombre del archivo. dbml. Para este proyecto, el <xref:System.Data.Linq.DataContext> objeto se denomina `northwindDataContext`.

    Puede crear una instancia de <xref:System.Data.Linq.DataContext> en el código y consultar las tablas especificadas por Object Relational Designer.

    Agregue el código siguiente al `Load` evento para consultar las tablas que se exponen como propiedades de su contexto de datos. La consulta filtra los resultados y devuelve solo los clientes que se encuentran `London`en.

    [!code-vb[VbLINQToSQLHowTos#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQtoSQLHowTos/VB/Form5.vb#11)]

4. Presione F5 para ejecutar el proyecto y ver los resultados.

5. A continuación se muestran otros filtros que puede probar.

    [!code-vb[VbLINQToSQLHowTos#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQtoSQLHowTos/VB/Form5.vb#12)]

## <a name="see-also"></a>Vea también

- [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)
- [Consultas](../../../../visual-basic/language-reference/queries/index.md)
- [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)
- [Métodos DataContext (Object Relational Designer)](/visualstudio/data-tools/datacontext-methods-o-r-designer)
