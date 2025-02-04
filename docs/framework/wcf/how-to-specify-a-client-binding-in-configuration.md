---
title: Procedimiento para especificar un enlace de cliente en la configuración
ms.date: 03/30/2017
ms.assetid: 4a7c79aa-50ee-4991-891e-adc0599323a7
ms.openlocfilehash: 0757dac4cdcffc7c3550432a71fe45b587327660
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/14/2019
ms.locfileid: "70990215"
---
# <a name="how-to-specify-a-client-binding-in-configuration"></a>Procedimiento para especificar un enlace de cliente en la configuración
En este ejemplo, se crea una aplicación de consola de cliente para utilizar un servicio de calculadora y el enlace para ese cliente se especifica de manera declarativa en la configuración. El cliente obtiene acceso al `CalculatorService`, que implementa la interfaz `ICalculator`, y el servicio y el cliente utilizan la clase <xref:System.ServiceModel.BasicHttpBinding>.  
  
 El procedimiento descrito asume que el servicio de calculadora se está ejecutando. Para obtener información acerca de cómo crear el servicio, [consulte Cómo: Especifique un enlace de servicio en](../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md)la configuración. También usa la [herramienta de utilidad de metadatos de ServiceModel (SvcUtil. exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) que Windows Communication Foundation (WCF) proporciona para generar automáticamente los componentes de cliente. La herramienta genera el código de cliente y la configuración para obtener acceso al servicio.  
  
 El cliente se crea en dos partes. Svcutil.exe genera la `ClientCalculator` que implementa la interfaz `ICalculator`. Esta aplicación de cliente se construye a continuación mediante la creación de una instancia de `ClientCalculator`.  
  
 Normalmente es el mejor procedimiento para especificar el enlace y la información de dirección de forma declarativa en configuración en lugar de hacerlo de forma imperativa en código. Normalmente, no resulta muy práctico definir los puntos de conexión en el código ya que los enlaces y las direcciones de un servicio implementado son, por lo general, diferentes de los utilizados durante el desarrollo del servicio. Más generalmente, manteniendo el enlace y la información de dirección fuera del código permite cambiarlos sin tener que recompilar o implementar la aplicación.  
  
 Puede realizar todos los pasos de configuración siguientes mediante la [herramienta editor de configuración (SvcConfigEditor. exe)](../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md).  
  
 Para la copia de origen de este ejemplo, consulte el ejemplo [BasicBinding](../../../docs/framework/wcf/samples/basicbinding.md) .  
  
### <a name="specifying-a-client-binding-in-configuration"></a>Especificación de un enlace de cliente mediante configuración  
  
1. Utilice Svcutil.exe desde la línea de comandos para generar el código a partir de los metadatos del servicio.  
  
    ```console  
    Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>   
    ```  
  
2. El cliente que se genera contiene la interfaz `ICalculator` que define el contrato de servicios que la implementación del cliente debe cumplir.  
  
     [!code-csharp[C_HowTo_ConfigureClientBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/generatedclient.cs#1)]
     [!code-csharp[C_HowTo_ConfigureClientBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/source.cs#1)]  
  
3. El cliente generado también contiene la implementación de `ClientCalculator`.  
  
     [!code-csharp[C_HowTo_ConfigureClientBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/generatedclient.cs#2)]
     [!code-csharp[C_HowTo_ConfigureClientBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/source.cs#2)]  
  
4. Svcutil.exe también genera la configuración para el cliente que utiliza la clase <xref:System.ServiceModel.BasicHttpBinding>. Al usar Visual Studio, asigne al archivo el nombre app. config. Observe que la información de enlace y dirección no se especifican en ninguna parte de la implementación del servicio. Además, el código tiene que escribirse para recuperar esa información del archivo de configuración.  
  
     [!code-xml[C_HowTo_ConfigureClientBinding#100](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/common/client.exe.config#100)]   
            
5. Cree una instancia de `ClientCalculator` en una aplicación y, a continuación, llame a las operaciones del servicio.  
  
     [!code-csharp[C_HowTo_ConfigureClientBinding#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/client.cs#3)]  
  
6. Compile y ejecute el cliente.  
  
## <a name="see-also"></a>Vea también

- [Utilización de enlaces para configurar servicios y clientes](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)
