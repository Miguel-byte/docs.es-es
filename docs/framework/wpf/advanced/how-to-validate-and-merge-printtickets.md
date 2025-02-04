---
title: Procedimiento Validar y combinar elementos PrintTicket
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- merging PrintTickets [WPF]
- PrintTicket [WPF], merging
- validation of PrintTickets [WPF]
- PrintTicket [WPF], validation
ms.assetid: 4fe2d501-d0b0-4fef-86af-6ffe6c162532
ms.openlocfilehash: 9e5242c07179501e6b39840a36f8dd6364d65b84
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69918347"
---
# <a name="how-to-validate-and-merge-printtickets"></a>Procedimiento Validar y combinar elementos PrintTicket
El [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] [esquema de impresión](https://go.microsoft.com/fwlink/?LinkId=186397) incluye los <xref:System.Printing.PrintCapabilities> <xref:System.Printing.PrintTicket> elementos flexible y extensible. En el primero se detallan las capacidades de un dispositivo de impresión y en el último se especifica cómo el dispositivo debe usar esas capacidades con respecto a una secuencia determinada de documentos, documento individual o página individual.  
  
 Una secuencia típica de tareas para una aplicación que admite la impresión sería la siguiente.  
  
1. Determinar las capacidades de una impresora.  
  
2. Configure <xref:System.Printing.PrintTicket> un para que use esas capacidades.  
  
3. Valide el <xref:System.Printing.PrintTicket>.  
  
 En este artículo se muestra cómo hacerlo.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo simple siguiente, solo le interesará si una impresora admite la impresión a dos caras. Los pasos principales son los siguientes.  
  
1. Obtiene un <xref:System.Printing.PrintCapabilities> objeto con el <xref:System.Printing.PrintQueue.GetPrintCapabilities%2A> método.  
  
2. Compruebe la presencia de la funcionalidad que desee. En el ejemplo siguiente, se prueba la <xref:System.Printing.PrintCapabilities.DuplexingCapability%2A> propiedad <xref:System.Printing.PrintCapabilities> del objeto para la presencia de la capacidad de impresión en ambos lados de una hoja de papel con el "torneado de páginas" a lo largo del lado de la hoja. Como <xref:System.Printing.PrintCapabilities.DuplexingCapability%2A> es una colección, usamos el `Contains` método de <xref:System.Collections.ObjectModel.ReadOnlyCollection%601>.  
  
    > [!NOTE]
    > Este paso no es estrictamente necesario. El <xref:System.Printing.PrintQueue.MergeAndValidatePrintTicket%2A> método que se usa a continuación comprobará cada <xref:System.Printing.PrintTicket> solicitud de con respecto a las capacidades de la impresora. Si la funcionalidad solicitada no es compatible con la impresora, el controlador de impresora sustituirá una solicitud <xref:System.Printing.PrintTicket> alternativa en la devuelta por el método.  
  
3. Si la impresora admite el dúplex, el código de ejemplo crea <xref:System.Printing.PrintTicket> un que solicita el dúplex. Pero la aplicación no especifica todos los valores posibles de la impresora disponibles <xref:System.Printing.PrintTicket> en el elemento. Esto sería una pérdida de tiempo del programa y del programador. En su lugar, el código establece solo la solicitud de dúplex y, a continuación <xref:System.Printing.PrintTicket> , la combina con una existente, completamente configurada y validada, <xref:System.Printing.PrintTicket>en este caso, <xref:System.Printing.PrintTicket>el valor predeterminado del usuario.  
  
4. En consecuencia, el ejemplo llama <xref:System.Printing.PrintQueue.MergeAndValidatePrintTicket%2A> al método para combinar el nuevo, el <xref:System.Printing.PrintTicket> mínimo y el valor predeterminado <xref:System.Printing.PrintTicket>del usuario. Esto devuelve un <xref:System.Printing.ValidationResult> que incluye el nuevo <xref:System.Printing.PrintTicket> como una de sus propiedades.  
  
5. A continuación, el ejemplo comprueba que <xref:System.Printing.PrintTicket> el nuevo solicita dúplex. Si lo hace, el ejemplo lo convierte en el nuevo vale de impresión predeterminado para el usuario. Si se ha omitido el paso 2 anterior y la impresora no admitía el dúplex en `false`el lado largo, la prueba habría resultado. (Vea la nota anterior).  
  
6. El último paso significativo es confirmar el cambio en la <xref:System.Printing.PrintQueue.UserPrintTicket%2A> propiedad <xref:System.Printing.PrintQueue> de con el <xref:System.Printing.PrintQueue.Commit%2A> método.  
  
 [!code-csharp[PrintTicketManagment#UsingMergeAndValidate](~/samples/snippets/csharp/VS_Snippets_Wpf/PrintTicketManagment/CSharp/printticket.cs#usingmergeandvalidate)]
 [!code-vb[PrintTicketManagment#UsingMergeAndValidate](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PrintTicketManagment/visualbasic/printticket.vb#usingmergeandvalidate)]  
  
 Para que pueda probar rápidamente este ejemplo, el resto de ellos se muestra a continuación. Cree un proyecto y un espacio de nombres y, a continuación, pegue los fragmentos de código de este artículo en el bloque de espacio de nombres.  
  
 [!code-csharp[PrintTicketManagment#UIForMergeAndValidatePTUtility](~/samples/snippets/csharp/VS_Snippets_Wpf/PrintTicketManagment/CSharp/printticket.cs#uiformergeandvalidateptutility)]
 [!code-vb[PrintTicketManagment#UIForMergeAndValidatePTUtility](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PrintTicketManagment/visualbasic/printticket.vb#uiformergeandvalidateptutility)]  
  
## <a name="see-also"></a>Vea también

- <xref:System.Printing.PrintCapabilities>
- <xref:System.Printing.PrintTicket>
- <xref:System.Printing.PrintServer.GetPrintQueues%2A>
- <xref:System.Printing.PrintServer>
- <xref:System.Printing.EnumeratedPrintQueueTypes>
- <xref:System.Printing.PrintQueue>
- <xref:System.Printing.PrintQueue.GetPrintCapabilities%2A>
- [Documentos en WPF](documents-in-wpf.md)
- [Información general sobre impresión](printing-overview.md)
- [Imprimir esquema](https://go.microsoft.com/fwlink/?LinkId=186397)
