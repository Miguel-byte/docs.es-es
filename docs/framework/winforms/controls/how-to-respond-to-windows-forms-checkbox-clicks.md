---
title: Procedimiento para responder a clics en casillas de formularios Windows Forms
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Click event [Windows Forms], CheckBox control
- CheckBox control [Windows Forms], Click events
- events [Windows Forms], Click events
- double-clicks
- check boxes [Windows Forms], responding to events
ms.assetid: c39f901e-8899-43b6-aa31-939cbf7089fb
ms.openlocfilehash: 7ff6b2aad9ef0775547af57f11af28839e69637c
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69914982"
---
# <a name="how-to-respond-to-windows-forms-checkbox-clicks"></a>Procedimiento para responder a clics en casillas de formularios Windows Forms
Cada vez que un usuario hace clic <xref:System.Windows.Forms.CheckBox> en un control <xref:System.Windows.Forms.Control.Click> de Windows Forms, se produce el evento. Puede programar la aplicación para realizar alguna acción en función del estado de la casilla.  
  
### <a name="to-respond-to-checkbox-clicks"></a>Para responder a clics en casillas  
  
1. En el <xref:System.Windows.Forms.Control.Click> controlador de eventos, use <xref:System.Windows.Forms.CheckBox.Checked%2A> la propiedad para determinar el estado del control y realice las acciones necesarias.  
  
    ```vb  
    Private Sub CheckBox1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles CheckBox1.Click  
       ' The CheckBox control's Text property is changed each time the   
       ' control is clicked, indicating a checked or unchecked state.  
       If CheckBox1.Checked = True Then  
          CheckBox1.Text = "Checked"  
       Else  
          CheckBox1.Text = "Unchecked"  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    private void checkBox1_Click(object sender, System.EventArgs e)  
    {  
       // The CheckBox control's Text property is changed each time the   
       // control is clicked, indicating a checked or unchecked state.  
       if (checkBox1.Checked)  
       {  
          checkBox1.Text = "Checked";  
       }  
       else  
       {  
          checkBox1.Text = "Unchecked";  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       void checkBox1_CheckedChanged(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          if (checkBox1->Checked)  
          {  
             checkBox1->Text = "Checked";  
          }  
          else  
          {  
             checkBox1->Text = "Unchecked";  
          }  
       }  
    ```  
  
    > [!NOTE]
    > Si el usuario intenta hacer doble clic en el <xref:System.Windows.Forms.CheckBox> control, cada clic se procesará por separado; es decir, el <xref:System.Windows.Forms.CheckBox> control no admite el evento de doble clic.  
  
    > [!NOTE]
    > Cuando la <xref:System.Windows.Forms.CheckBox.AutoCheck%2A> propiedad es `true` (valor predeterminado), <xref:System.Windows.Forms.CheckBox> se selecciona o borra automáticamente al hacer clic en él. De lo contrario, debe establecer manualmente <xref:System.Windows.Forms.CheckBox.Checked%2A> la propiedad cuando <xref:System.Windows.Forms.Control.Click> se produce el evento.  
  
     También puede usar el <xref:System.Windows.Forms.CheckBox> control para determinar un curso de acción.  
  
### <a name="to-determine-a-course-of-action-when-a-check-box-is-clicked"></a>Para determinar una línea de acción al hacer clic en una casilla  
  
1. Use una instrucción Case para consultar el valor de la <xref:System.Windows.Forms.CheckBox.CheckState%2A> propiedad a fin de determinar un curso de acción. Cuando la <xref:System.Windows.Forms.CheckBox.ThreeState%2A> propiedad está establecida en `true`, la <xref:System.Windows.Forms.CheckBox.CheckState%2A> propiedad puede devolver tres valores posibles, que representan el cuadro que se está comprobando, el cuadro desactivado o un tercer estado indeterminado en el que se muestra el cuadro con un atenuado apariencia para indicar que la opción no está disponible.  
  
    ```vb  
    Private Sub CheckBox1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles CheckBox1.Click  
       Select Case CheckBox1.CheckState  
          Case CheckState.Checked  
             ' Code for checked state.  
          Case CheckState.Unchecked  
             ' Code for unchecked state.  
          Case CheckState.Indeterminate  
             ' Code for indeterminate state.  
       End Select   
    End Sub  
    ```  
  
    ```csharp  
    private void checkBox1_Click(object sender, System.EventArgs e)  
    {  
       switch(checkBox1.CheckState)  
       {  
          case CheckState.Checked:  
             // Code for checked state.  
             break;  
          case CheckState.Unchecked:  
             // Code for unchecked state.  
             break;  
          case CheckState.Indeterminate:  
             // Code for indeterminate state.  
             break;  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       void checkBox1_CheckedChanged(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          switch(checkBox1->CheckState) {  
             case CheckState::Checked:  
                // Code for checked state.  
                break;  
             case CheckState::Unchecked:  
                // Code for unchecked state.  
                break;  
             case CheckState::Indeterminate:  
                // Code for indeterminate state.  
                break;  
          }  
       }  
    ```  
  
    > [!NOTE]
    > Cuando la <xref:System.Windows.Forms.CheckBox.ThreeState%2A> propiedad se establece en `true`, <xref:System.Windows.Forms.CheckBox.Checked%2A> `true` lapropiedad<xref:System.Windows.Forms.CheckState.Indeterminate>devuelve para y.<xref:System.Windows.Forms.CheckState.Checked>  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Forms.CheckBox>
- [Información general sobre el control CheckBox](checkbox-control-overview-windows-forms.md)
- [Cómo: Establecer opciones con Windows Forms controles CheckBox](how-to-set-options-with-windows-forms-checkbox-controls.md)
- [CheckBox (control)](checkbox-control-windows-forms.md)
