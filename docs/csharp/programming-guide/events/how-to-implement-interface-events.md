---
title: 'Procedimiento Implementar eventos de interfaz: Guía de programación de C#'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- interfaces [C#], event implementation in classes
- events [C#], in interfaces
ms.assetid: 63527447-9535-4880-8e95-35e2075827df
ms.openlocfilehash: 574ea9927a22c24c356d84652fd29692c519247b
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2019
ms.locfileid: "69590505"
---
# <a name="how-to-implement-interface-events-c-programming-guide"></a>Procedimiento Implementar eventos de interfaz (Guía de programación de C#)
Un [interfaz](../../language-reference/keywords/interface.md) puede declarar un [evento](../../language-reference/keywords/event.md). En el siguiente ejemplo, se muestra cómo implementar eventos de interfaz en una clase. Básicamente, las reglas son las mismas que para implementar cualquier propiedad o método de interfaz.  
  
## <a name="to-implement-interface-events-in-a-class"></a>Para implementar eventos de interfaz en una clase  
  
Declare el evento en la clase y, después, invóquelo en las áreas apropiadas.  
  
```csharp
namespace ImplementInterfaceEvents  
{  
    public interface IDrawingObject  
    {  
        event EventHandler ShapeChanged;  
    }  
    public class MyEventArgs : EventArgs   
    {  
        // class members  
    }  
    public class Shape : IDrawingObject  
    {  
        public event EventHandler ShapeChanged;  
        void ChangeShape()  
        {  
            // Do something here before the event…  

            OnShapeChanged(new MyEventArgs(/*arguments*/));  

            // or do something here after the event.   
        }  
        protected virtual void OnShapeChanged(MyEventArgs e)  
        {  
            ShapeChanged?.Invoke(this, e);  
        }  
    }  

}  
```  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se muestra cómo controlar la situación menos común en que la clase hereda de dos o más interfaces y cada interfaz tiene un evento con el mismo nombre. En esta situación, debe proporcionar una implementación de interfaz explícita para uno de los eventos como mínimo. Al escribir una implementación de interfaz explícita para un evento, también debe escribir los descriptores de acceso del evento `add` y `remove`. Normalmente, los proporciona el compilador, pero en este caso no es posible.  
  
Al proporcionar sus propios descriptores de acceso, puede especificar si los dos eventos se representan mediante el mismo evento en la clase o mediante eventos diferentes. Por ejemplo, si los eventos deben provocarse en momentos diferentes según las especificaciones de la interfaz, puede asociar cada evento a una implementación distinta en su clase. En el ejemplo siguiente, los suscriptores determinan qué evento `OnDraw` recibirán al convertir la referencia de forma en `IShape` o en `IDrawingObject`.  
  
 [!code-csharp[csProgGuideEvents#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideEvents/CS/Events.cs#10)]
  
## <a name="see-also"></a>Vea también

- [Guía de programación de C#](../index.md)
- [Eventos](./index.md)
- [Delegados](../delegates/index.md)
- [Implementación de interfaz explícita](../interfaces/explicit-interface-implementation.md)
- [Cómo: Producir eventos de una clase base en clases derivadas](./how-to-raise-base-class-events-in-derived-classes.md)
