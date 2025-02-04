---
title: Como esta llamada no es "awaited", la ejecución del método actual continuará antes de que se complete la llamada.
ms.date: 07/20/2015
f1_keywords:
- bc42358
- vbc42358
helpviewer_keywords:
- BC42358
ms.assetid: 43342515-c3c8-4155-9263-c302afabcbc2
ms.openlocfilehash: 6ceebc3af01c13474affa6e728c49d6d246eb331
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701200"
---
# <a name="because-this-call-is-not-awaited-the-current-method-continues-to-run-before-the-call-is-completed"></a>Como esta llamada no es "awaited", la ejecución del método actual continuará antes de que se complete la llamada.
Dado que no se esperaba esta llamada, la ejecución del método actual continuará antes de que se complete la llamada. Considere la posibilidad de aplicar el operador "Await" al resultado de la llamada.  
  
 El método actual llama a un método asincrónico que devuelve un valor <xref:System.Threading.Tasks.Task> o <xref:System.Threading.Tasks.Task%601> y no aplica el operador [Await](../../../visual-basic/language-reference/operators/await-operator.md) al resultado. La llamada al método asincrónico inicia una tarea asincrónica. Pero, dado que no se aplica un operador `Await` , el programa continúa sin esperar a que se complete la tarea. En la mayoría de los casos, no se espera ese comportamiento. Normalmente otros aspectos del método de llamada dependen de los resultados de la llamada o, como mínimo, se espera que el método llamado se complete antes de volver del método que contiene la llamada.  
  
 Otro problema igual de importante es lo que sucede con las excepciones que se producen en el método asincrónico llamado. Una excepción que aparece en un método que devuelve un valor <xref:System.Threading.Tasks.Task> o  <xref:System.Threading.Tasks.Task%601> se almacena en la tarea devuelta. Si no espera la tarea o comprueba explícitamente las excepciones, se perderá la excepción. Si espera la tarea, su excepción se volverá a producir.  
  
 El procedimiento recomendado es esperar siempre la llamada.  
  
 De forma predeterminada, este mensaje es una advertencia. Para más información sobre cómo ocultar las advertencias o cómo tratarlas como errores, vea [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **IDENTIFICADOR de error:** BC42358  
  
### <a name="to-address-this-warning"></a>Para resolver esta advertencia  
  
- Considere la posibilidad de suprimir la advertencia solamente si está seguro de que no quiere esperar a que se complete la llamada asincrónica y que el método llamado no producirá excepciones. En ese caso, puede suprimir la advertencia asignando el resultado de la tarea de la llamada a una variable.  
  
     En el ejemplo siguiente se muestra cómo provocar la advertencia, cómo suprimirla y cómo esperar la llamada.  
  
    ```vb  
    Async Function CallingMethodAsync() As Task  
  
        ResultsTextBox.Text &= vbCrLf & "  Entering calling method."  
  
        ' Variable delay is used to slow down the called method so that you  
        ' can distinguish between awaiting and not awaiting in the program's output.   
        ' You can adjust the value to produce the output that this topic shows   
        ' after the code.  
        Dim delay = 5000  
  
        ' Call #1.  
        ' Call an async method. Because you don't await it, its completion isn't   
        ' coordinated with the current method, CallingMethodAsync.  
        ' The following line causes the warning.  
        CalledMethodAsync(delay)  
  
        ' Call #2.  
        ' To suppress the warning without awaiting, you can assign the   
        ' returned task to a variable. The assignment doesn't change how  
        ' the program runs. However, the recommended practice is always to  
        ' await a call to an async method.  
        ' Replace Call #1 with the following line.  
        'Task delayTask = CalledMethodAsync(delay)  
  
        ' Call #3  
        ' To contrast with an awaited call, replace the unawaited call   
        ' (Call #1 or Call #2) with the following awaited call. The best   
        ' practice is to await the call.  
  
        'Await CalledMethodAsync(delay)  
  
        ' If the call to CalledMethodAsync isn't awaited, CallingMethodAsync  
        ' continues to run and, in this example, finishes its work and returns  
        ' to its caller.  
        ResultsTextBox.Text &= vbCrLf & "  Returning from calling method."  
    End Function  
  
    Async Function CalledMethodAsync(howLong As Integer) As Task  
  
        ResultsTextBox.Text &= vbCrLf & "    Entering called method, starting and awaiting Task.Delay."  
        ' Slow the process down a little so you can distinguish between awaiting  
        ' and not awaiting. Adjust the value for howLong if necessary.  
        Await Task.Delay(howLong)  
        ResultsTextBox.Text &= vbCrLf & "    Task.Delay is finished--returning from called method."  
    End Function  
    ```  
  
     En el ejemplo, si elige Call #1 o Call #2, el método asincrónico no esperado (`CalledMethodAsync`) termina después de que se completen su llamador (`CallingMethodAsync`) y el llamador del llamador (`StartButton_Click`). La última línea de la salida siguiente muestra cuándo finaliza el método llamado. La entrada y la salida del controlador de eventos que llama a `CallingMethodAsync` en el ejemplo completo se marcan en la salida.  
  
    ```console  
    Entering the Click event handler.  
      Entering calling method.  
        Entering called method, starting and awaiting Task.Delay.  
      Returning from calling method.  
    Exiting the Click event handler.  
        Task.Delay is finished--returning from called method.  
    ```  
  
## <a name="example"></a>Ejemplo  
 La siguiente aplicación de Windows Presentation Foundation (WPF) contiene los métodos del ejemplo anterior. Los siguientes pasos sirven para configurar la aplicación.  
  
1. Cree una aplicación WPF y asígnele el nombre `AsyncWarning`.  
  
2. En el Editor de código de Visual Studio, elija la pestaña **MainWindow.xaml** .  
  
     Si la pestaña no está visible, abra el menú contextual de MainWindow.xaml en el **Explorador de soluciones**y elija **Ver código**.  
  
3. Reemplace el código de la vista **XAML** de MainWindow.xaml por el código siguiente.  
  
    ```vb  
    <Window x:Class="MainWindow"  
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
            Title="MainWindow" Height="350" Width="525">  
        <Grid>  
            <Button x:Name="StartButton" Content="Start" HorizontalAlignment="Left" Margin="214,28,0,0" VerticalAlignment="Top" Width="75" HorizontalContentAlignment="Center" FontWeight="Bold" FontFamily="Aharoni" Click="StartButton_Click" />  
            <TextBox x:Name="ResultsTextBox" Margin="0,80,0,0" TextWrapping="Wrap" FontFamily="Lucida Console"/>  
        </Grid>  
    </Window>  
    ```  
  
     En la vista **Diseño** de MainWindow.xaml aparece una ventana simple que contiene un botón y un cuadro de texto.  
  
     Para obtener más información sobre el Diseñador XAML, vea [Tutorial: Crear una IU usando el Diseñador XAML](/visualstudio/designers/creating-a-ui-by-using-xaml-designer-in-visual-studio). Para obtener información sobre cómo crear una interfaz de usuario simple propia, vea las secciones "Para crear una aplicación para WPF" y "Para diseñar una ventana MainWindow simple de WPF" de [Tutorial: Acceso a web usando Async y Await](../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md).  
  
4. Reemplace el código en el archivo MainWindow.xaml.vb por el código siguiente.  
  
    ```vb  
    Class MainWindow   
  
        Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs)  
  
            ResultsTextBox.Text &= vbCrLf & "Entering the Click event handler."  
            Await CallingMethodAsync()  
            ResultsTextBox.Text &= vbCrLf & "Exiting the Click event handler."  
        End Sub  
  
        Async Function CallingMethodAsync() As Task  
  
            ResultsTextBox.Text &= vbCrLf & "  Entering calling method."  
  
            ' Variable delay is used to slow down the called method so that you  
            ' can distinguish between awaiting and not awaiting in the program's output.   
            ' You can adjust the value to produce the output that this topic shows   
            ' after the code.  
            Dim delay = 5000  
  
            ' Call #1.  
            ' Call an async method. Because you don't await it, its completion isn't   
            ' coordinated with the current method, CallingMethodAsync.  
            ' The following line causes the warning.  
            CalledMethodAsync(delay)  
  
            ' Call #2.  
            ' To suppress the warning without awaiting, you can assign the   
            ' returned task to a variable. The assignment doesn't change how  
            ' the program runs. However, the recommended practice is always to  
            ' await a call to an async method.  
  
            ' Replace Call #1 with the following line.  
            'Task delayTask = CalledMethodAsync(delay)  
  
            ' Call #3  
            ' To contrast with an awaited call, replace the unawaited call   
            ' (Call #1 or Call #2) with the following awaited call. The best   
            ' practice is to await the call.  
  
            'Await CalledMethodAsync(delay)  
  
            ' If the call to CalledMethodAsync isn't awaited, CallingMethodAsync  
            ' continues to run and, in this example, finishes its work and returns  
            ' to its caller.  
            ResultsTextBox.Text &= vbCrLf & "  Returning from calling method."  
        End Function  
  
        Async Function CalledMethodAsync(howLong As Integer) As Task  
  
            ResultsTextBox.Text &= vbCrLf & "    Entering called method, starting and awaiting Task.Delay."  
            ' Slow the process down a little so you can distinguish between awaiting  
            ' and not awaiting. Adjust the value for howLong if necessary.  
            Await Task.Delay(howLong)  
            ResultsTextBox.Text &= vbCrLf & "    Task.Delay is finished--returning from called method."  
        End Function  
  
    End Class  
  
    ' Output  
  
    ' Entering the Click event handler.  
    '   Entering calling method.  
    '     Entering called method, starting and awaiting Task.Delay.  
    '   Returning from calling method.  
    ' Exiting the Click event handler.  
    '     Task.Delay is finished--returning from called method.  
  
    ' Output  
  
    ' Entering the Click event handler.  
    '   Entering calling method.  
    '     Entering called method, starting and awaiting Task.Delay.  
    '     Task.Delay is finished--returning from called method.  
    '   Returning from calling method.  
    ' Exiting the Click event handler.  
    ```  
  
5. Presione la tecla F5 para ejecutar el programa y elija el botón **Inicio** .  
  
     La salida esperada aparece al final del código.  
  
## <a name="see-also"></a>Vea también

- [Await (operador)](../../../visual-basic/language-reference/operators/await-operator.md)
- [Programación asincrónica con Async y Await](../../../visual-basic/programming-guide/concepts/async/index.md)
