---
title: Procedimiento para serializar y deserializar datos JSON
ms.date: 03/25/2019
ms.assetid: 88abc1fb-8196-4ee3-a23b-c6934144d1dd
ms.openlocfilehash: 0bebdbb3d74d58db093c4ec1e0e88138c7080335
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69947897"
---
# <a name="how-to-serialize-and-deserialize-json-data"></a>Procedimiento Serialización y deserialización de datos JSON
JSON (notación de objetos JavaScript) es un formato de codificación de datos eficaz que permite intercambios rápidos de cantidades pequeñas de datos entre los exploradores de cliente y servicios web con AJAX (JavaScript asincrónico y XML) habilitado.  
  
 En este artículo se muestra cómo serializar objetos de tipo .NET en datos codificados con JSON y, a continuación, deserializar los datos en formato JSON en instancias de tipos .NET. En este ejemplo se usa un contrato de datos para mostrar la serialización y la deserialización `Person` de un tipo <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>definido por el usuario y se utiliza.  
  
 Normalmente, Windows Communication Foundation (WCF) administra automáticamente la serialización y deserialización de JSON cuando se usan tipos de contrato de datos en operaciones de servicio que se exponen a través de puntos de conexión habilitados para AJAX. Sin embargo, en algunos casos puede que necesite trabajar directamente con datos JSON.   
  
> [!NOTE]
> Si se produce un error durante la serialización de una respuesta saliente en el servidor o por algún otro motivo, puede que no se devuelva al cliente como un error.  
  
 Este artículo se basa en el ejemplo de serialización de [JSON](../samples/json-serialization.md) .  
  
## <a name="to-define-the-data-contract-for-a-person-type"></a>Para definir el contrato de datos para un tipo de persona 
  
1. Defina el contrato de datos para `Person` adjuntando <xref:System.Runtime.Serialization.DataContractAttribute> a la clase y el atributo <xref:System.Runtime.Serialization.DataMemberAttribute> a los miembros que desee serializar. Para obtener más información sobre los contratos de datos, consulte [diseño de contratos de servicio](../designing-service-contracts.md).  
  
    ```csharp  
    [DataContract]  
    internal class Person  
    {  
        [DataMember]  
        internal string name;  
  
        [DataMember]  
        internal int age;  
    }  
    ```  
  
## <a name="to-serialize-an-instance-of-type-person-to-json"></a>Para serializar una instancia de tipo Persona a JSON  
  
1. Cree una instancia del tipo `Person`.  
  
    ```csharp  
    var p = new Person();  
    p.name = "John";  
    p.age = 42;  
    ```  
  
2. Serialice el `Person` objeto en una secuencia <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>de memoria mediante.  
  
    ```csharp  
    var stream1 = new MemoryStream();  
    var ser = new DataContractJsonSerializer(typeof(Person));  
    ```  
  
3. Utilice el método <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.WriteObject%2A> para escribir datos JSON en la secuencia.  
  
    ```csharp  
    ser.WriteObject(stream1, p);  
    ```  
  
4. Muestre la salida JSON.  
  
    ```csharp  
    stream1.Position = 0;  
    var sr = new StreamReader(stream1);  
    Console.Write("JSON form of Person object: ");  
    Console.WriteLine(sr.ReadToEnd());  
    ```  
  
## <a name="to-deserialize-an-instance-of-type-person-from-json"></a>Deserialización de una instancia de tipo Persona a partir de JSON  
  
1. Deserialice los datos codificados con JSON en una nueva instancia de `Person` utilizando el método <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.ReadObject%2A> de <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>:  
  
    ```csharp  
    stream1.Position = 0;  
    var p2 = (Person)ser.ReadObject(stream1);  
    ```  
  
2. Muestre los resultados.  
  
    ```csharp  
    Console.WriteLine($"Deserialized back, got name={p2.name}, age={p2.age}");  
    ```  
  
## <a name="example"></a>Ejemplo  
  
```csharp  
// Create a User object and serialize it to a JSON stream.  
public static string WriteFromObject()  
{  
    // Create User object.  
    var user = new User("Bob", 42);  
  
    // Create a stream to serialize the object to.  
    var ms = new MemoryStream();  
  
    // Serializer the User object to the stream.  
    var ser = new DataContractJsonSerializer(typeof(User));  
    ser.WriteObject(ms, user);  
    byte[] json = ms.ToArray();  
    ms.Close();  
    return Encoding.UTF8.GetString(json, 0, json.Length);  
}  
  
// Deserialize a JSON stream to a User object.  
public static User ReadToObject(string json)  
{  
    var deserializedUser = new User();  
    var ms = new MemoryStream(Encoding.UTF8.GetBytes(json));  
    var ser = new DataContractJsonSerializer(deserializedUser.GetType());  
    deserializedUser = ser.ReadObject(ms) as User;  
    ms.Close();  
    return deserializedUser;  
}  
```  
  
> [!NOTE]
> El serializador de JSON inicia una excepción de serialización para los contratos de datos que tienen varios miembros con el mismo nombre, tal y como se muestra en el siguiente código de ejemplo.  
  
```csharp  
[DataContract]  
public class TestDuplicateDataBase  
{  
    [DataMember]  
    public int field1 = 123;  
}

[DataContract]  
public class TestDuplicateDataDerived : TestDuplicateDataBase  
{  
    [DataMember]  
    public new int field1 = 999;  
}  
```  
  
## <a name="see-also"></a>Vea también

- [Serialización de JSON independiente](stand-alone-json-serialization.md)
- [Compatibilidad con JSON y otros formatos de transferencia de datos](support-for-json-and-other-data-transfer-formats.md)
