---
title: Hay un acceso de propiedad Default ambiguo entre los miembros <defaultpropertyname> heredados de la interfaz <interfacename1> y <defaultpropertyname> de la interfaz <interfacename2>
ms.date: 07/20/2015
f1_keywords:
- vbc30686
- bc30686
helpviewer_keywords:
- BC30686
ms.assetid: 784fefec-ef57-48cf-b960-957df419b439
ms.openlocfilehash: a36cfe8e5496bbfd1941afa8a46086491ae96a2a
ms.sourcegitcommit: 463f3f050cecc0b6403e67f19a61f870fb8e7b7d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2019
ms.locfileid: "68512752"
---
# <a name="default-property-access-is-ambiguous-between-the-inherited-interface-members-defaultpropertyname-of-interface-interfacename1-and-defaultpropertyname-of-interface-interfacename2"></a>El acceso a la propiedad predeterminada es ambiguo entre los miembros\<de interfaz heredados ' defaultpropertyname\<> ' de la interfaz\<' interfacename1 > ' y '\< defaultpropertyname > ' de la interfaz ' interfacename2 > '

Una interfaz hereda de dos interfaces, cada una de las cuales declara una propiedad predeterminada con el mismo nombre. El compilador no puede resolver un acceso a esta propiedad predeterminada sin calificación. Esto se ilustra en el siguiente ejemplo:

```vb
Public Interface Iface1
    Default Property prop(ByVal arg As Integer) As Integer
End Interface
Public Interface Iface2
    Default Property prop(ByVal arg As Integer) As Integer
End Interface
Public Interface Iface3
    Inherits Iface1, Iface2
End Interface
Public Class testClass
    Public Sub accessDefaultProperty()
        Dim testObj As Iface3
        Dim testInt As Integer = testObj(1)
    End Sub
End Class
```

Cuando se especifica `testObj(1)`, el compilador intenta resolverlo en la propiedad predeterminada. Sin embargo, hay dos propiedades predeterminadas posibles debido a las interfaces heredadas, por lo que el compilador señala este error.

**IDENTIFICADOR de error:** BC30686

## <a name="to-correct-this-error"></a>Para corregir este error

- Evite la herencia de miembros con el mismo nombre. En el ejemplo anterior, si `testObj` no necesita ninguno de los miembros de, `Iface2`por ejemplo,, declárelo como se indica a continuación:

  ```vb
  Dim testObj As Iface1
  ```

  O bien

- Implemente la interfaz heredada en una clase. A continuación, puede implementar cada una de las propiedades heredadas con nombres diferentes. Sin embargo, solo uno de ellos puede ser la propiedad predeterminada de la clase de implementación. Esto se ilustra en el siguiente ejemplo:

  ```vb
  Public Class useIface3
      Implements Iface3
      Default Public Property prop1(ByVal arg As Integer) As Integer Implements Iface1.prop
          ' Insert code to define Get and Set procedures for prop1.
      End Property
      Public Property prop2(ByVal arg As Integer) As Integer Implements Iface2.prop
          ' Insert code to define Get and Set procedures for prop2.
      End Property
  End Class
  ```

## <a name="see-also"></a>Vea también

- [Interfaces](../../../visual-basic/programming-guide/language-features/interfaces/index.md)
