---
Titulo: "Apuntes Asp.Net Identity"
---


____
## ASP NET Core Identity tutorial from scratch

https://www.youtube.com/watch?v=egITMrwMOPU


~~~

~~~
____
## ASP.NET Core 3 - Authentication - Ep.1 Basics (Claims/ClaimsIdentity/ClaimsPrincipal/Authorization)

https://www.youtube.com/watch?v=Fhfvbl_KbWo&list=PLOeFnOV9YBa7dnrjpOG6lMpcyd7Wn7E8V


~~~

~~~
____

## ASP.NET Core 3 - Authentication - Ep.2 Identity Authentication

https://www.youtube.com/watch?v=IjbtWPXVJGw&list=PLOeFnOV9YBa7dnrjpOG6lMpcyd7Wn7E8V&index=2



~~~

~~~
____
## ASP.NET Core 3 - Identity - Ep.2.1 Email Verification

https://www.youtube.com/watch?v=Vj7iCb7wDs0&list=PLOeFnOV9YBa7dnrjpOG6lMpcyd7Wn7E8V&index=3



~~~

~~~
____
## ASP.NET Core 3 - Authentication - Ep.3 Authorization (All about Policies and Claims)

https://www.youtube.com/watch?v=RBMO_hruKaI&list=PLOeFnOV9YBa7dnrjpOG6lMpcyd7Wn7E8V&index=4




~~~

~~~

____

## ASP.NET Core 3 - Authorization - Ep.4 Extras (IAuthorizationService & much more...)

https://www.youtube.com/watch?v=n-g9O0dOV9A&list=PLOeFnOV9YBa7dnrjpOG6lMpcyd7Wn7E8V&index=5




~~~

~~~

____
## ASP.NET Core 5.0 - Authentication/Authorization - .Net Engineering Forum 2021-01-26

https://www.youtube.com/watch?v=BWa7Mu-oMHk


~~~

~~~

____
## 01 - Customizing ASP.NET Authentication with Identity - Overview of Identity

https://www.youtube.com/watch?v=2SIYclIN2jI&list=PL38oYrcNWuOPs29ltEJGuzMKaYEMKBp6-




~~~

~~~

____
## 02 - Customizing ASP.NET Authentication with Identity - Locally Authenticated Users

https://www.youtube.com/watch?v=J5izES2OQ2k&list=PL38oYrcNWuOPs29ltEJGuzMKaYEMKBp6-&index=2



Abrimos Package manager console:
~~~
install-package jQuery




~~~

Activamos las migraciones
~~~
enable-migrations
~~~


Generame un script sql para actualizar la base de datos
~~~
Update-Database -Script -SourceMigration: $InitialDatabase
~~~

ahora tenemos las herramientas de entity framework core desde la consola de administracion de paquetes, para utilizarlo desde visual studio

Sacado del siguiente articulo:

Referencia de herramientas de Entity Framework Core: consola del administrador de paquetes en Visual Studio

https://docs.microsoft.com/es-es/ef/core/cli/powershell

~~~
Install-Package Microsoft.EntityFrameworkCore.Tools

Update-Package Microsoft.EntityFrameworkCore.Tools


~~~


Y desde powershell podemos ver las herramientas instaladas


~~~
Get-Help about_EntityFrameworkCore
~~~

Lista de comandos

Añadir una migracion
~~~
Add-Migration -Name "nombremigracion"
~~~


~~~
Drop-Database
~~~


~~~
Get-DbContext
~~~

Esta es nueva en EF Core 5.0
~~~
Get-Migration
~~~


~~~
Remove-Migration -Force
~~~

~~~
Scaffold-DbContext "Server=(localdb)\mssqllocaldb;Database=Blogging;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models
~~~

Ejemplo que scaffolding solo selecciona tablas y crea el contexto en una carpeta independiente con un nombre y un espacio de nombres especificados:

~~~
Scaffold-DbContext "Server=(localdb)\mssqllocaldb;Database=Blogging;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models -Tables "Blog","Post" -ContextDir Context -Context BlogContext -ContextNamespace New.Namespace
~~~
Genera un script SQL desde DbContext.Agregado en EF Core 3,0.
~~~
Script-DbContext
~~~

Genera un script SQL que aplica todos los cambios de una migración seleccionada a otra migración seleccionada.

~~~
Script-Migration 0 InitialCreate
~~~

En el ejemplo siguiente se crea un script para todas las migraciones después de la migración de InitialCreate con el identificador de migración.


~~~
Script-Migration 20180904195021_InitialCreate
~~~
Actualiza la base de datos a la última migración o a una migración especificada.



~~~
Update-Database
~~~
En el ejemplo siguiente se revierten todas las migraciones.

~~~
Update-Database 0
~~~
En los siguientes ejemplos se actualiza la base de datos a una migración especificada. El primero usa el nombre de la migración y el segundo usa el identificador de migración y una conexión especificada:


~~~
Update-Database InitialCreate
Update-Database 20180904195021_InitialCreate -Connection your_connection_string
~~~


____

## 26- Configurando Identity (passwords, usuarios, logins) | Programando en ASP.NET Core 2

https://www.youtube.com/watch?v=FN-JGlCrCcQ



~~~

~~~

____

## 27- UserManager y RoleManager | Programando en ASP.NET Core 2

https://www.youtube.com/watch?v=i8ftra-_8IM




~~~

~~~

____

## 28- Entendiendo Claims y Policies | Programando en ASP.NET Core 2.0

https://www.youtube.com/watch?v=fwyDqi3uQZ0



~~~

~~~

____














