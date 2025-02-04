---
title: -optioninfer
ms.date: 07/20/2015
f1_keywords:
- -optioninfer
helpviewer_keywords:
- -optioninfer compiler option [Visual Basic]
- /optioninfer compiler option [Visual Basic]
- optioninfer compiler option [Visual Basic]
ms.assetid: f6c09db1-0553-464a-abe3-d4510c61d6ed
ms.openlocfilehash: 4848dec148bc528e7a30940643e3364f1bb5f805
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69939197"
---
# <a name="-optioninfer"></a>-optioninfer
Permite el uso de la inferencia de tipo de variable local en declaraciones de variables.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-optioninfer[+ | -]  
```  
  
## <a name="arguments"></a>Argumentos  
  
|Término|Definición|  
|---|---|  
|`+` &#124; `-`|Opcional. Especifique `-optioninfer+` para habilitar la inferencia de tipo de variable local o `-optioninfer-` para bloquearla. La opción `-optioninfer`, sin ningún valor especificado, es igual a `-optioninfer+`. El valor predeterminado cuando el modificador `-optioninfer` no está presente también es `-optioninfer+`. El valor predeterminado se establece en el archivo de respuesta vbc.rsp.|  
  
> [!NOTE]
> Puede utilizar la opción `-noconfig` para conservar los valores predeterminados internos del compilador en lugar de los especificados en vbc.rsp. El valor predeterminado del compilador para esta opción es `-optioninfer-`.  
  
## <a name="remarks"></a>Comentarios  
 Si el archivo de código fuente contiene una [instrucción Option Infer](../../../visual-basic/language-reference/statements/option-infer-statement.md), la instrucción reemplaza la `-optioninfer` configuración del compilador de línea de comandos.  
  
### <a name="to-set--optioninfer-in-the-visual-studio-ide"></a>Para Set-optioninfer (en el IDE de Visual Studio  
  
1. Seleccione un proyecto en **Explorador de soluciones**. En el menú **Proyecto**, haga clic en **Propiedades**.  
  
2. En la pestaña compilar, modifique el valor del cuadro **Option Infer** .  
  
## <a name="example"></a>Ejemplo  
 El siguiente código compila `test.vb` con la inferencia de tipo de variable local habilitada.  
  
```console
vbc -optioninfer+ test.vb  
```  
  
## <a name="see-also"></a>Vea también

- [Compilador de línea de comandos de Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)
- [-optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)
- [-optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)
- [-optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)
- [Líneas de comandos de compilación de ejemplo](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [Option Infer (instrucción)](../../../visual-basic/language-reference/statements/option-infer-statement.md)
- [Inferencia de tipo de variable local](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
- [Valores predeterminados de Visual Basic, Proyectos, Opciones (Cuadro de diálogo)](/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
- [Página Compilación, Diseñador de proyectos (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)
- [/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)
- [Compilación desde la línea de comandos](../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md)
