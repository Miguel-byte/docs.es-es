---
title: Usar acciones para implementar el comportamiento del servidor
ms.date: 03/30/2017
ms.assetid: 11a372db-7168-498b-80d2-9419ff557ba5
ms.openlocfilehash: 5c71cfe8965cf8edbe07ff7ae4c6be95b437bf80
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70894256"
---
# <a name="using-actions-to-implement-server-side-behavior"></a>Usar acciones para implementar el comportamiento del servidor

Las acciones OData proporcionan una manera de implementar un comportamiento que actúa sobre un recurso obtenido de un servicio OData. Por ejemplo, considere una película digital como un recurso; se pueden hacer muchas cosas con ella: desproteger, valorar/comentar o insertar en el repositorio. Todos estos son ejemplos de acciones que se pueden implementar mediante un Servicio de datos de WCF que administre películas digitales. Las acciones se describen en una respuesta OData que contiene un recurso en el que se puede invocar la acción. Cuando un usuario solicita un recurso que representa una película digital, la respuesta devuelta por el Servicio de datos de WCF contiene información sobre las acciones disponibles para dicho recurso. La disponibilidad de una acción puede depender del estado del servicio de datos o del recurso. Por ejemplo, una vez desprotegida una película digital otro usuario no la puede desproteger. Los clientes pueden invocar una acción con solo especificar una dirección URL. Por ejemplo, `http://MyServer/MovieService.svc/Movies(6)` identificaría una película digital específica y `http://MyServer/MovieService.svc/Movies(6)/Checkout` invocaría la acción en la película específica. Las acciones le permiten exponer su modelo de servicio sin exponer el modelo de datos. Continuando con el ejemplo de servicio de películas, quizás desee permitir que un usuario valore una película pero no desee exponer directamente los datos de valoración como un recurso. Podría implementar una acción de valoración que permitiera al usuario valorar una película pero no tener acceso directamente a los datos de valoración como un recurso.
  
## <a name="implementing-an-action"></a>Implementar una acción  
 Para implementar una acción de servicio, debe implementar <xref:System.IServiceProvider>las interfaces, [llamará](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/hh859915(v=vs.103))y [IDataServiceInvokable](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/hh859893(v=vs.103)) . <xref:System.IServiceProvider>permite a WCF Data Services obtener la implementación de [llamará](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/hh859915(v=vs.103)). [Llamará](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/hh859915(v=vs.103)) permite a WCF Data Services crear, buscar, describir e invocar acciones de servicio. [IDataServiceInvokable](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/hh859893(v=vs.103)) le permite invocar el código que implementa el comportamiento de las acciones de servicio y obtener los resultados, si los hay. Tenga en cuenta que WCF Data Services son Servicios de WCF por llamada; se creará una nueva instancia del servicio cada vez que se llame al servicio.  Asegúrese de que no se realiza trabajo innecesario cuando se crea el servicio.  
  
### <a name="iserviceprovider"></a>IServiceProvider  
 <xref:System.IServiceProvider> contiene un método denominado <xref:System.IServiceProvider.GetService%2A>. WCF Data Services llama a este método para recuperar una serie de proveedores de servicios, incluidos proveedores de servicios de metadatos y proveedores de acciones de servicios de datos. Cuando se le pida un proveedor de acciones de servicio de datos, devuelva la implementación de [llamará](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/hh859915(v=vs.103)) .  
  
### <a name="idataserviceactionprovider"></a>IDataServiceActionProvider  
 [Llamará](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/hh859915(v=vs.103)) contiene métodos que permiten recuperar información sobre las acciones disponibles. Al implementar [llamará](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/hh859915(v=vs.103)) , se aumentan los metadatos para el servicio que se define en la implementación del servicio de [llamará](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/hh859915(v=vs.103)) con acciones y el control de envío a esas acciones como responda.  
  
#### <a name="advertiseserviceaction"></a>AdvertiseServiceAction  
 Se llama al [método AdvertiseServiceAction](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/hh859971(v=vs.103)) para determinar qué acciones están disponibles para el recurso especificado. Solo se llama a este método para las acciones que no están siempre disponibles. Se emplea para comprobar si la acción se debe incluir en la respuesta OData según el estado del recurso que se solicita o el estado del servicio. Usted decide cómo se realiza esta comprobación. Si resulta costoso calcular la disponibilidad y el recurso actual está en una fuente, es aceptable omitir la comprobación y anunciar la acción. El parámetro `inFeed` se establece en `true` si el recurso actual que se devuelve forma parte de una fuente.  
  
#### <a name="createinvokable"></a>CreateInvokable  
 Se llama a [CreateInvokable](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/hh859940(v=vs.103)) para crear un [IDataServiceInvokable](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/hh859893(v=vs.103)) que contiene un delegado que encapsula el código que implementa el comportamiento de la acción. Esto crea la instancia de [IDataServiceInvokable](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/hh859893(v=vs.103)) , pero no invoca la acción. Las acciones de un Servicio de datos de WCF tienen efectos secundarios y deben usarse junto con el proveedor de actualizaciones para guardar estos cambios en disco. Se llama al método [IDataServiceInvokable. Invoke](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/hh859924(v=vs.103)) desde el método SaveChanges () del proveedor de actualización.  
  
#### <a name="getserviceactions"></a>GetServiceActions  
 Este método devuelve una colección de instancias de [ServiceAction](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/hh544089(v=vs.103)) que representan todas las acciones que expone un servicio de datos de WCF. [ServiceAction](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/hh544089(v=vs.103)) es la representación de metadatos de una acción, que incluye información como el nombre de la acción, sus parámetros y su tipo de valor devuelto.  
  
#### <a name="getserviceactionsbybindingparametertype"></a>GetServiceActionsByBindingParameterType  
 Este método devuelve una colección de todas las instancias de [ServiceAction](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/hh544089(v=vs.103)) que se pueden enlazar al tipo de parámetro de enlace especificado. En otras palabras, todos los [ServiceAction](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/hh544089(v=vs.103))que pueden actuar en el tipo de recurso especificado (también denominado tipo de parámetro de enlace). Se utiliza cuando el servicio devuelve un recurso para incluir información acerca de las acciones que se pueden invocar en ese recurso. Este método solo debe devolver acciones que se pueden enlazar al tipo de parámetro de enlace exacto (no a tipos derivados). Se llama a este método una vez por solicitud por tipo encontrado y WCF Data Services almacena en memoria caché el resultado.  
  
#### <a name="tryresolveserviceaction"></a>TryResolveServiceAction  
 Este método busca un [ServiceAction](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/hh544089(v=vs.103)) especificado y devuelve `true` si se encuentra [ServiceAction](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/hh544089(v=vs.103)) . Si se encuentra, se devuelve [ServiceAction](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/hh544089(v=vs.103)) en el `serviceAction` `out` parámetro.  
  
### <a name="idataserviceinvokable"></a>IDataServiceInvokable  
 Esta interfaz proporciona una forma de ejecutar una acción de un Servicio de datos de WCF. A la hora de implementar IDataServiceInvokable, es responsable de 3 cosas:  
  
1. Capturar y posiblemente calcular las referencias de los parámetros  
  
2. Enviar los parámetros al código que implementa realmente la acción cuando se llama a Invoke()  
  
3. Almacenar los resultados de Invoke() para que se puedan recuperar mediante GetResult()  
  
 Los parámetros se pueden pasar como tokens. Esto se debe a que es posible escribir un proveedor de servicios de datos que funcione con tokens que representan recursos; en este caso, quizás necesite convertir (serializar) estos tokens en recursos reales antes de enviarlos a la acción real. Una vez calculadas las referencias del parámetro, debe estar en un estado editable para que cualquier cambio en el recurso que se produzca cuando se invoque la acción se guarde y se escriba en el disco.  
  
 Esta interfaz requiere dos métodos: Invocar y GetResult. Invoke invoca el delegado que implementa el comportamiento de la acción y GetResult devuelve el resultado de la acción.  
  
## <a name="invoking-a-wcf-data-service-action"></a>Invocar una acción de un Servicio de datos de WCF  
 Las acciones se invocan mediante una solicitud POST HTTP. La dirección URL especifica el recurso seguido del nombre de la acción. Los parámetros se pasan en el cuerpo de la solicitud. Por ejemplo, suponga que hay un servicio denominado MovieService que expone una acción denominada Rate. Puede usar la dirección URL siguiente para invocar la acción Rate en una película concreta:  
  
 `http://MovieServer/MovieService.svc/Movies(1)/Rate`
  
 Movies(1) especifica la película que desea valorar y Rate especifica la acción Rate. El valor real de la valoración estará en el cuerpo de la solicitud HTTP como se muestra en el ejemplo siguiente:  
  
```http
POST http://MovieServer/MoviesService.svc/Movies(1)/Rate HTTP/1.1   
Content-Type: application/json   
Content-Length: 20   
Host: localhost:15238  
{   
   "rating": 4   
}  
```  
  
> [!WARNING]
> El código muestra anterior solo funcionará con WCF Data Services 5.2 y versiones posteriores que admitan JSON ligero. Si emplea una versión anterior de WCF Data Services, debe especificar el content-type detallado de json de la manera siguiente: `application/json;odata=verbose`.  
  
 O bien, puede invocar una acción mediante el Cliente de WCF Data Services como se muestra en el fragmento de código siguiente.  
  
```csharp
MoviesModel context = new MoviesModel (new Uri("http://MyServer/MoviesService.svc/"));  
//...  
context.Execute(new Uri("http://MyServer/MoviesService.svc/Movies(1)/Rate"), "POST", new BodyOperationParameter("rating",4) );
```
  
 En el fragmento de código anterior, la clase `MoviesModel` se generaba usando Visual Studio para Agregar referencia de servicio a un Servicio de datos de WCF.  
  
## <a name="see-also"></a>Vea también

- [Servicios de datos de WCF 4.5](index.md)
- [Definir Servicios de datos de WCF](defining-wcf-data-services.md)
- [Desarrollo e implementación de WCF Data Services](developing-and-deploying-wcf-data-services.md)
- [Proveedores de servicios de datos personalizados](custom-data-service-providers-wcf-data-services.md)
