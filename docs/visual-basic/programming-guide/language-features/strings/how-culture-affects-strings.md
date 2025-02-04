---
title: Cómo afecta la referencia cultural a las cadenas en Visual Basic
ms.date: 07/20/2015
helpviewer_keywords:
- locale [Visual Basic], effect on strings
- strings [Visual Basic], locale dependence
ms.assetid: c4664444-ee0d-47bf-bef1-eaa3c54bdd7f
ms.openlocfilehash: d090a6e89a470958dd323c3f249ed0658dc1cefa
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69955103"
---
# <a name="how-culture-affects-strings-in-visual-basic"></a>Cómo afecta la referencia cultural a las cadenas en Visual Basic
En esta página de ayuda se describe cómo Visual Basic usa la información de referencia cultural para realizar conversiones de cadenas y comparaciones.  
  
## <a name="when-to-use-culture-specific-strings"></a>Cuándo usar cadenas específicas de la referencia cultural  
 Normalmente, debe usar cadenas específicas de la referencia cultural para todos los datos presentados y leídos de los usuarios, y usar cadenas de referencia cultural invariable para los datos internos de la aplicación.  
  
 Por ejemplo, si la aplicación pide a los usuarios que escriban una fecha como una cadena, debería esperar que los usuarios apliquen formato a las cadenas según su referencia cultural y la aplicación debe convertir la cadena de forma adecuada. Si la aplicación presenta esa fecha en su interfaz de usuario, debe presentarla en la referencia cultural del usuario.  
  
 Sin embargo, si la aplicación carga la fecha en un servidor central, debe dar formato a la cadena según una referencia cultural concreta, para evitar confusiones entre formatos de fecha potencialmente diferentes.  
  
## <a name="culture-sensitive-functions"></a>Funciones que tienen en cuenta la referencia cultural  
 Todas las funciones de conversión de cadenas de Visual Basic (excepto las `Str` funciones `Val` y) usan la información de referencia cultural de la aplicación para asegurarse de que las conversiones y comparaciones son adecuadas para la referencia cultural de la de la aplicación. usuario.  
  
 La clave para usar correctamente las funciones de conversión de cadenas en aplicaciones que se ejecutan en equipos con una configuración de referencia cultural diferente es entender qué funciones usan una configuración de referencia cultural específica y cuáles utilizan la configuración de referencia cultural actual. Tenga en cuenta que la configuración de la referencia cultural de la aplicación se hereda de forma predeterminada de la configuración de referencia cultural del sistema operativo. Para obtener más información, <xref:Microsoft.VisualBasic.Strings.Asc%2A>vea <xref:Microsoft.VisualBasic.Strings.AscW%2A> <xref:Microsoft.VisualBasic.Strings.Chr%2A> <xref:Microsoft.VisualBasic.Strings.ChrW%2A>,,, <xref:Microsoft.VisualBasic.Strings.Format%2A>, <xref:Microsoft.VisualBasic.Conversion.Hex%2A>,,y [funciones de conversión de tipos.](../../../../visual-basic/language-reference/functions/type-conversion-functions.md) <xref:Microsoft.VisualBasic.Conversion.Oct%2A>  
  
 (Convierte números en cadenas) y `Val` (convierte cadenas en números) las funciones no usan la información de referencia cultural de la aplicación al realizar la conversión entre cadenas y números. `Str` En su lugar, reconocen solo el punto (.) como separador decimal válido. Los análogos que tienen en cuenta la referencia cultural de estas funciones son:  
  
- **Conversiones que usan la referencia cultural actual.** Las `CStr` funciones `Format` y convierten un número en una cadena, y `CDbl` las `CInt` funciones y convierten una cadena en un número.  
  
- **Conversiones que usan una referencia cultural concreta.** Cada objeto Number tiene un `ToString(IFormatProvider)` método que convierte un número en una cadena y un `Parse(String, IFormatProvider)` método que convierte una cadena en un número. Por ejemplo, el `Double` tipo proporciona los <xref:System.Double.ToString%28System.IFormatProvider%29> métodos <xref:System.Double.Parse%28System.String%2CSystem.IFormatProvider%29> y.  
  
 Para obtener más información, vea <xref:Microsoft.VisualBasic.Conversion.Str%2A> y <xref:Microsoft.VisualBasic.Conversion.Val%2A>.  
  
## <a name="using-a-specific-culture"></a>Usar una referencia cultural específica  
 Imagine que está desarrollando una aplicación que envía una fecha (con formato de cadena) a un servicio Web. En este caso, la aplicación debe usar una referencia cultural específica para la conversión de cadenas. Para ilustrar por qué, tenga en cuenta el resultado de <xref:System.DateTime.ToString> utilizar el método de la fecha: Si la aplicación usa ese método para dar formato a la fecha 4 de julio de 2005, devuelve "7/4/2005 12:00:00 AM" cuando se ejecuta con la referencia cultural de Estados Unidos inglés (en-US), pero devuelve "04.07.2005 00:00:00" cuando se ejecuta con la referencia cultural de alemán (de-DE).  
  
 Cuando necesite realizar una conversión de cadena en un formato de referencia cultural concreto, debe utilizar la `CultureInfo` clase que está integrada en el .NET Framework. Puede crear un nuevo `CultureInfo` objeto para una referencia cultural concreta pasando el nombre de la referencia cultural <xref:System.Globalization.CultureInfo.%23ctor%2A> al constructor. Los nombres de referencia cultural admitidos se <xref:System.Globalization.CultureInfo> muestran en la página de ayuda de la clase.  
  
 Como alternativa, puede obtener una instancia de la *referencia cultural de todos* los idiomas <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> de la propiedad. La referencia cultural de todos los idiomas se basa en la referencia cultural en inglés, pero hay algunas diferencias. Por ejemplo, la referencia cultural de todos los idiomas especifica un reloj de 24 horas en lugar de un reloj de 12 horas.  
  
 Para convertir una fecha en la cadena de la referencia cultural, <xref:System.Globalization.CultureInfo> pase el objeto al método del <xref:System.DateTime.ToString%28System.IFormatProvider%29> objeto Date. Por ejemplo, el código siguiente muestra "07/04/2005 00:00:00", independientemente de la configuración de la referencia cultural de la aplicación.  
  
 [!code-vb[VbVbalrConcepts#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConcepts/VB/Class1.vb#1)]  
  
> [!NOTE]
> Los literales de fecha siempre se interpretan según la referencia cultural en inglés.  
  
## <a name="comparing-strings"></a>Comparar cadenas  
 Hay dos situaciones importantes en las que se necesitan comparaciones de cadenas:  
  
- **Ordenación de los datos que se van a mostrar al usuario.** Utilice operaciones basadas en la referencia cultural actual para que las cadenas se ordenen correctamente.  
  
- **Determinar si dos cadenas internas de aplicación coinciden exactamente (normalmente por motivos de seguridad).** Usar operaciones que omitan la referencia cultural actual.  
  
 Puede realizar ambos tipos de comparaciones con la función <xref:Microsoft.VisualBasic.Strings.StrComp%2A> Visual Basic. Especifique el argumento `Compare` opcional para controlar el tipo de comparación: `Text` para la mayoría de la `Binary` entrada y la salida para determinar las coincidencias exactas.  
  
 La `StrComp` función devuelve un entero que indica la relación entre las dos cadenas comparadas en función del criterio de ordenación. Un valor positivo para el resultado indica que la primera cadena es mayor que la segunda cadena. Un resultado negativo indica que la primera cadena es más pequeña y cero indica la igualdad entre las cadenas.  
  
 [!code-vb[VbVbalrStrings#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class1.vb#22)]  
  
 También puede usar el .NET Framework asociado de la `StrComp` función, el <xref:System.String.Compare%2A?displayProperty=nameWithType> método. Este es un método estático y sobrecargado de la clase de cadena base. En el ejemplo siguiente se muestra cómo se utiliza este método:  
  
 [!code-vb[VbVbalrStrings#48](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#48)]  
  
 Para tener un mayor control sobre cómo se realizan las comparaciones, puede usar sobrecargas adicionales <xref:System.String.Compare%2A> del método. Con el <xref:System.String.Compare%2A?displayProperty=nameWithType> método, puede utilizar el argumento `comparisonType` para especificar el tipo de comparación que se va a usar.  
  
|Valor del `comparisonType` argumento|Tipo de comparación|Cuándo utilizarlo|  
|---|---|---|  
|`Ordinal`|Comparación basada en bytes de componentes de cadenas.|Use este valor al comparar: identificadores que distinguen mayúsculas de minúsculas, configuraciones relacionadas con la seguridad u otros identificadores no lingüísticos donde los bytes deben coincidir exactamente.|  
|`OrdinalIgnoreCase`|Comparación basada en bytes de componentes de cadenas.<br /><br /> `OrdinalIgnoreCase`usa la información de la referencia cultural de todos los idiomas para determinar si dos caracteres solo difieren en mayúsculas.|Use este valor al comparar: identificadores que no distinguen mayúsculas de minúsculas, configuraciones relacionadas con la seguridad y datos almacenados en Windows.|  
|`CurrentCulture` o `CurrentCultureIgnoreCase`|Comparación basada en la interpretación de las cadenas en la referencia cultural actual.|Use estos valores al comparar: datos que se muestran al usuario, la mayoría de los datos proporcionados por el usuario y otros datos que requieren interpretación lingüística.|  
|`InvariantCulture` o `InvariantCultureIgnoreCase`|Comparación basada en la interpretación de las cadenas en la referencia cultural de todos los idiomas.<br /><br /> Es diferente de y `Ordinal` `OrdinalIgnoreCase`, porque la referencia cultural de todos los idiomas trata los caracteres que están fuera del intervalo aceptado como caracteres invariables equivalentes.|Utilice estos valores solo al comparar datos persistentes o Mostrar datos pertinentes lingüísticamente que requieran un criterio de ordenación fijo.|  
  
### <a name="security-considerations"></a>Consideraciones de seguridad  
 Si la aplicación toma decisiones de seguridad basadas en el resultado de una comparación o de una operación de cambio de mayúsculas y minúsculas, la operación `Ordinal` debe `OrdinalIgnoreCase` utilizar el `comparisonType` <xref:System.String.Compare%2A?displayProperty=nameWithType> método y pasar o para el argumento.  
  
## <a name="see-also"></a>Vea también

- <xref:System.Globalization.CultureInfo>
- [Introducción a las cadenas en Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)
- [Funciones de conversión de tipos](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)
