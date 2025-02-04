---
title: Usar System.Transactions en ASP.NET
ms.date: 03/30/2017
ms.assetid: 1982c300-7ea6-4242-95ed-dc28ccfacac9
ms.openlocfilehash: bfc75661ea538ac52b244e38eb10e6ae37a8fd62
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/31/2019
ms.locfileid: "70205838"
---
# <a name="using-systemtransactions-in-aspnet"></a>Usar System.Transactions en ASP.NET
Este tema describe cómo se puede utilizar <xref:System.Transactions> correctamente dentro de una aplicación ASP.NET.  
  
## <a name="enable-distributedtransactionpermission-in-aspnet"></a>Habilitar DistributedTransactionPermission en ASP.NET  
 <xref:System.Transactions> admite los llamadores de confianza parcial y se marca con el atributo **AllowPartiallyTrustedCallers** (APTCA). Los niveles de confianza para <xref:System.Transactions> se definen dependiendo de los tipos de recursos, por ejemplo, la memoria del sistema, los recursos de todo el proceso compartido, los recursos para todo el sistema y otros recursos. <xref:System.Transactions> expone dichos tipos de recursos y el nivel de confianza que se debería exigir para tener acceso a ellos. En un entorno de confianza parcial, un ensamblado sin plena confianza puede usar solo las transacciones dentro del dominio de aplicación (en este caso, el único recurso que se protege es la memoria del sistema) a menos que se permita <xref:System.Transactions.DistributedTransactionPermission>.  
  
 Se exige<xref:System.Transactions.DistributedTransactionPermission> cuando la administración de la transacción se escala para que el Coordinador de transacciones distribuidas de Microsoft (MSDTC) la administre. Este tipo de escenario usa recursos de todo el proceso y particularmente un recurso global, que es el espacio reservado en el registro de MSDTC. Un ejemplo de este uso es un front-end web con una base de datos o una aplicación que usa una base de datos como parte de los servicios que proporciona.  
  
 ASP.NET tiene su propio conjunto de niveles de confianza y asocia un conjunto concreto de permisos con estos niveles de confianza a través de los archivos de directivas. Para obtener más información, consulte [niveles de confianza y archivos de directiva de ASP.net](https://docs.microsoft.com/previous-versions/aspnet/wyts434y(v=vs.100)). Al instalar inicialmente el Windows SDK, ninguno de los archivos de directiva de ASP.NET predeterminados está <xref:System.Transactions.DistributedTransactionPermission>asociado a. Como tal, cuando su transacción en una aplicación ASP.NET realiza una escalada para ser administrada por MSDTC, se produce un error en la subida con <xref:System.Security.SecurityException> al exigir <xref:System.Transactions.DistributedTransactionPermission>. Debería permitir <xref:System.Transactions.DistributedTransactionPermission> en los mismos niveles de confianza predeterminados como aquéllos de <xref:System.Data.SqlClient.SqlClientPermission>para habilitar la subida de la transacción en un entorno confiable parcial de ASP.NET. Puede configurar su propio nivel de confianza personalizado y archivo de directivas para admitirlo o bien modificar los archivos de directivas predeterminados, **Web_hightrust.config** y **Web_mediumtrust.config**.  
  
 Para modificar los archivos de directivas, agregue un elemento **SecurityClass** para **DistributedTransactionPermission** al elemento **SecurityClasses** en el elemento **PolicyLevel** y agregue un elemento **IPermission** correspondiente en el ASP.NET **NamedPermissionSet** para System. Transactions. Esto se muestra en el siguiente archivo de configuración.  
  
```xml  
<SecurityClasses>  
   <SecurityClass Name="DistributedTransactionPermission" Description="System.Transactions.DistributedTransactionPermission, System.Transactions, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"/>  
...  
</SecurityClasses>  
  
<PermissionSet  
  class="NamedPermissionSet"  
  version="1"  
  Name="ASP.Net">  
     <IPermission  
        class="System.Transactions.DistributedTransactionPermission, System.Transactions, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"  
        version="1"  
        Unrestricted="true"  
     />  
...  
</PermissionSet>  
```  
  
 Para obtener más información sobre la Directiva de seguridad ASP.NET, vea [elemento securityPolicy (esquema de configuración de ASP.net)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/zhs35b56(v=vs.100)).  
  
## <a name="dynamic-compilation"></a>Compilación dinámica  
 Si desea importar y utilizar <xref:System.Transactions> en una aplicación ASP.NET que está compilada dinámicamente en acceso, debería colocar una referencia al ensamblado <xref:System.Transactions> en el archivo de configuración. Específicamente, la referencia debe agregarse en la sección **compilation**/**assemblies** del archivo de configuración **Web.config** de la raíz predeterminada, o bien en un archivo de configuración de una aplicación web concreta. En el siguiente ejemplo se muestra cómo hacerlo.  
  
```xml  
<configuration>  
   <system.web>  
      <compilation>  
         <assemblies>  
      <add assembly="System.Transactions, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
         </assemblies>  
      </compilation>  
   </system.web>  
</configuration>  
```  
  
 Para obtener más información, vea [Add Element for assemblies for Compilation (ASP.NET Settings Schema)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/37e2zyhb(v=vs.100)).  
  
## <a name="see-also"></a>Vea también

- [Niveles de confianza y archivos de directiva de ASP.NET](https://docs.microsoft.com/previous-versions/aspnet/wyts434y(v=vs.100))
- [Elemento securityPolicy (esquema de configuración de ASP.NET)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/zhs35b56(v=vs.100))
- [Escalado de administración de transacciones](transaction-management-escalation.md)
