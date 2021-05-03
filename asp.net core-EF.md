---
Titulo: "Apuntes Asp.Net Core Entity Frameworkd(Recipes)"
---

# Apuntes Asp.Net Core Entity Frameworkd(Recipes)

Command line for .Net core<br><br>
<code>
dotnet new web -o mywebapp<br>
dotnet new --help<br>
dotnet run<br>
dotnet build<br>

</code>
Tenemos ejemplos mas concretos. <br>
En este ejemplo creatmos un proyecto de tipo webapi:<br>
<code>
dotnet new webapi -n AspNetCoreWebApi
</code>

Para crear un proyecto de consola :<br>

<code>
dotnet new console -o console01
</code>

Para crear un proyecto MVC:<br>

<code>dotnet new mvc -o proyectmvc01</code>

Para crear un  proyecto de  solucion:

<code>dotnet new sln -o nuevasolucion</code>


<code>dotnet sln todo.sln add todo-app/todo-app.csproj</code>

Agregue varios proyectos de C# a una solución:

<code>dotnet sln todo.sln add todo-app/todo-app.csproj back-end/back-end.csproj</code>

Quite un proyecto de C# de una solución:<br>
<code>dotnet sln todo.sln remove todo-app/todo-app.csproj</code>

Tambien tenemos msbuild para la  creacion  y compilacion de todas sus dependencias:

<code>dotnet msbuild</code>

Tambien tenemos comandos de referencia de proyecto:<br>

<code>dotnet add reference</code><br>
<code>dotnet list reference</code><br>
<code>dotnet remove reference</code><br>

Tambien tenemos comandos de paquete de proyecto:

<code>dotnet add package</code><br>
<code>dotnet list package</code><br>
<code>dotnet  remove package</code><br>

Con la version 3.0 de net tenemos:

<pre>
dotnet new wpf
dotnet new winforms
</pre>



Tenemos en la pagina de microsoft explicando todos los comandos:<br>

### [dotnet new](https://docs.microsoft.com/es-es/dotnet/core/tools/dotnet-new?tabs=netcore22)




### [Tutorial EF de todas las versiones](https://www.entityframeworktutorial.net/) muy bueno.

A webApp program scaffolding example in .Net Core 2.0:
<pre>
public class Program
{
    BuildWebHost(args).Run();
}
public static IWebHost BuildWebHost(string[] args) => 
    WebHost.CreateDefaultBuilder(args).
    UserStartUp<StartUp>().
    Build(); 
</pre>

Esta es la nueva manera de ejecutar una app autocontenida en la version .Net core 2.0
<pre>
 public Startup(IHostingEnvironment env)
{
    var builder = new ConfigurationBuilder()
        .SetBasePath(env.ContentRootPath)
        .AddJsonFile("appsettings.json", optional: false, reloadOnChange: true)
        .AddJsonFile($"appsettings.{env.EnvironmentName}.json", optional: true);

    if (env.IsDevelopment())
    {
        builder.AddUserSecrets<Startup>();
    }

    builder.AddEnvironmentVariables();
    Configuration = builder.Build();
}

public IConfigurationRoot Configuration { get; }
</pre>


En la version de .Net Core 1.x el patro de creacion de una aplicacion web app era diferente.

Para usar micrations tenemos que añadir esto:

Microsoft.EntityFrameworkCore.Tools y tenemos que añadirlo utilizando nuget

Luego en la line a de comando podemos utilizar code first con migraciones:

<pre>
dotnet ef migrations add MyMigration [options]
dotnet ef database update [options]
dotnet ef migrations remove [options]
dotnet ef migrations script [From] [To] [options]
</pre>

Tambien podemos hacer reverse ingeniering con la siguiente linea de comando
<pre>
dotnet ef dbcontext scaffold [Connection] [Provider] [options]
</pre>

Esto nos generara un dbcontext de entity framework desde una base de datos con esta linea de comandos y sus parametros apropiados.

Para añadir paquetes nuget desde la linea de comandos
<pre>
dotnet add package Newtonsoft.Json

dotnet add package Microsoft.AspNetCore.StaticFiles

</pre>

Para trabajar con Entity Framework tenemos que añadir los siguientes packetes:
<pre>

dotnet add package Microsoft.EntityFrameworkCore.SqlServer

dotnet add package --version 2.0.3

dotnet add package Microsoft.EntityFrameworkCore.Design

</pre>

El paquete <code>Microsoft.EntityFrameworkCore.Tools </code> es para lo siguiente:

Enables these commonly used commands:<br>
Add-Migration<br>
Drop-Database<br>
Get-DbContext<br>
Scaffold-DbContext<br>
Script-Migrations<br>
Update-Database<br>

Estos comando mencionados anteriormente se utilizarian en visual studio 2017/2019.<br>

Cuales son las diferencias entre estos dos paquetes:

<code>Microsoft.EntityFrameworkCore.Tools</code> are tools for use with the Package Manager Console (PMC) inside Visual Studio 2017/2019. Includes Scaffold-DbContext, Add-Migration, and Update-Database.

<code>Microsoft.EntityFrameworkCore.Tools.DotNet</code> are for use with .NET Core, specifically the dotnet.exe command line tool.



El paquete <code>microsoft.entityframeworkcore.design</code> es utilizado tambien para ef migrations y para reverse ingeniering pero para CLI dentro del sdk de net core y sobre todo en visual studio code.

Para la version .Net core 3.0 para instalar las herramientas ef de EntityFramework:<br>
Tambien esto se llama .Net core command lines interfaces (CLI) tools.
<pre>
dotnet tool install --global dotnet-ef --version 3.0.0-*
</pre>

Por ejemplo para utilizar entity framework con sql lite:

<pre>
dotnet add package Microsoft.EntityFrameworkCore.Sqlite
dotnet add package Microsoft.EntityFrameworkCore.Design
</pre>

Luego podemos hacer <code> dotnet restore </code> para que se baje los paquetes al proyecto.

Aqui tenemos ejemplo de codigo de un contexto EF, definido por convencion:<br>
(tambien podemos hacerlo por configuracion)

<pre>
using Microsoft.EntityFrameworkCore;
using System.Collections.Generic;

namespace ConsoleApp.SQLite
{
    public class BloggingContext : DbContext
    {
        public DbSet<Blog> Blogs { get; set; }
        public DbSet<Post> Posts { get; set; }

        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        {
            optionsBuilder.UseSqlite("Data Source=blogging.db");
        }
    }

    public class Blog
    {
        public int BlogId { get; set; }
        public string Url { get; set; }

        public ICollection<Post> Posts { get; set; }
    }

    public class Post
    {
        public int PostId { get; set; }
        public string Title { get; set; }
        public string Content { get; set; }

        public int BlogId { get; set; }
        public Blog Blog { get; set; }
    }
}
</pre>

En el optionBuilder tambien podemos tener:
<pre>
optionsBuilder
    .UseSqlServer(connectionString, providerOptions=>providerOptions.CommandTimeout(60))
    .UseQueryTrackingBehavior(QueryTrackingBehavior.NoTracking);
</pre>
Tambien puede ser:
<pre>
protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
{
    if (!optionsBuilder.IsConfigured)
    {
        optionsBuilder.UseSqlServer(@"Server=(localdb)\mssqllocaldb;Database=EFProviders.InMemory;Trusted_Connection=True;ConnectRetryCount=0");
    }
}
</pre>

Luego podemos correr el siguiente comando para aplicar code first, o sea crear una base de datos a partir de nuestro modelo definido:
<pre>
dotnet ef migrations add InitialCreate

dotnet ef database update
</pre>

El comando <code>dotnet ef database update</code> es para aplicar los cambios del modelo a la base de datos.

<pre>
using System;

namespace ConsoleApp.SQLite
{
    public class Program
    {
        public static void Main()
        {
            using (var db = new BloggingContext())
            {
                db.Blogs.Add(new Blog { Url = "http://blogs.msdn.com/adonet" });
                var count = db.SaveChanges();
                Console.WriteLine("{0} records saved to database", count);

                Console.WriteLine();
                Console.WriteLine("All blogs in database:");
                foreach (var blog in db.Blogs)
                {
                    Console.WriteLine(" - {0}", blog.Url);
                }
            }
        }
    }
}
</pre>

### Proveedor de base de datos InMemory para EF Core

<pre>
   Install-Package Microsoft.EntityFrameworkCore.InMemory
</pre>

<pre>
dotnet add package Microsoft.EntityFrameworkCore.InMemory --version 2.2.6 (Ojo para la version 2.x, existe ya la version core 3.0)
</pre>

InMemory no es una base de datos relacional.


<pre>
public class BloggingContext : DbContext
{
    public BloggingContext()
    { }

    public BloggingContext(DbContextOptions<BloggingContext> options)
        : base(options)
    { }
</pre>


<pre>
using BusinessLogic;
using Microsoft.EntityFrameworkCore;
using Microsoft.VisualStudio.TestTools.UnitTesting;
using System.Linq;

namespace TestProject.InMemory
{
    [TestClass]
    public class BlogServiceTests
    {
        [TestMethod]
        public void Add_writes_to_database()
        {
            var options = new DbContextOptionsBuilder<BloggingContext>()
                .UseInMemoryDatabase(databaseName: "Add_writes_to_database")
                .Options;

            // Run the test against one instance of the context
            using (var context = new BloggingContext(options))
            {
                var service = new BlogService(context);
                service.Add("http://sample.com");
            }

            // Use a separate instance of the context to verify correct data was saved to database
            using (var context = new BloggingContext(options))
            {
                Assert.AreEqual(1, context.Blogs.Count());
                Assert.AreEqual("http://sample.com", context.Blogs.Single().Url);
            }
        }

        [TestMethod]
        public void Find_searches_url()
        {
            var options = new DbContextOptionsBuilder<BloggingContext>()
                .UseInMemoryDatabase(databaseName: "Find_searches_url")
                .Options;

            // Insert seed data into the database using one instance of the context
            using (var context = new BloggingContext(options))
            {
                context.Blogs.Add(new Blog { Url = "http://sample.com/cats" });
                context.Blogs.Add(new Blog { Url = "http://sample.com/catfish" });
                context.Blogs.Add(new Blog { Url = "http://sample.com/dogs" });
                context.SaveChanges();
            }

            // Use a clean instance of the context to run the test
            using (var context = new BloggingContext(options))
            {
                var service = new BlogService(context);
                var result = service.Find("cat");
                Assert.AreEqual(2, result.Count());
            }
        }
    }
}
</pre>

### Ejemplo con Sql server(Code-first) 

Aqui tenemos los paquetes a introducir en el proyecto:
<pre>

dotnet add package Microsoft.EntityFramecore.SqlServer

dotnet add package Microsoft.EntityFrameworkcore.SqlServer.Design

Microsoft.EntityFrameworkcore.Tools(este paquete seria mas para visual studio 2017/2019)
</pre>

Aqui tenemos el modelo
<pre>
namespace EFCore.models
{
    public class Product
    {
        public int Id { get; set; }
        public string Name { get; set; }
    }
}
</pre>

Y aqui tenemos el contexto de la base de datos

<pre>
using Microsoft.EntityFrameworkCore;
 
namespace EFCore.models
{
    public class EFContext : DbContext
    {
 
        private const string connectionString = "Server=(localdb)\\mssqllocaldb;Database=EFCore;Trusted_Connection=True;";
 
        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        {
            optionsBuilder.UseSqlServer(connectionString);
        }
 
        public DbSet<Product> Products { get; set; }
 
    }
}
</pre>


Para crear la base de datos desde el modelo y en visual studio 2017/2019
<pre>
Add-Migration “NewDatabase”

update-database
</pre>

Y luego le añadimos algunos datos, una vez creada la base de datos:
<pre>
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Hello World!");
        insertProduct();
 
        Console.WriteLine("Press any key to continue");
        Console.ReadKey();
    }
 
    static void insertProduct()
    {
        using (var db = new EFContext())
        { 
            Product product = new Product();
            product.Name = "Pen Drive";
            db.Add(product);
 
            product = new Product();
            product.Name = "Memory Card";
            db.Add(product);
 
            db.SaveChanges();
        }
        return;
   }
}
</pre>

<pre>
using System.Linq;
 
static void readProduct()
{
 
    using (var db = new EFContext())
    {
        List<Product> products = db.Products.ToList();
        foreach(Product p in products)
        {
            Console.WriteLine("{0} {1}",p.Id, p.Name);
        }
    }
    return;
}
</pre>



### Varios ConnectionString Ejemplos


<pre>
@"Server=(localdb)\mssqllocaldb;Database=EFProviders.InMemory;Trusted_Connection=True;ConnectRetryCount=0")
</pre>

Conectarse a una cuenta windows integrada en Sql Server:
<pre>
"Persist Security Info=False;Integrated Security=true;  
    Initial Catalog=AdventureWorks;Server=MSSQL1"  
"Persist Security Info=False;Integrated Security=SSPI;  
    database=AdventureWorks;server=(local)"  
"Persist Security Info=False;Trusted_Connection=True;  
    database=AdventureWorks;server=(local)" 
</pre>

Conectarse a una cuenta Sql Server:
<pre>
"Persist Security Info=False;User ID=*****;Password=*****;Initial Catalog=AdventureWorks;Server=MySqlServer"
</pre>

Conectarse a una instancia con nombre de SQL Server
<pre>
Data Source=MySqlServer\MSSQL1;"
</pre>

Standard Security
<pre>
Server=myServerAddress;Database=myDataBase;User Id=myUsername;
Password=myPassword;
</pre>

Connection to a SQL Server instance

<pre>
Server=myServerName\myInstanceName;Database=myDataBase;User Id=myUsername;
Password=myPassword;
</pre>

Connect via an IP address

<pre>
Data Source=190.190.200.100,1433;Network Library=DBMSSOCN;
Initial Catalog=myDataBase;User ID=myUsername;Password=myPassword;
</pre>

Enable MARS

<pre>
Server=myServerAddress;Database=myDataBase;Trusted_Connection=True;
MultipleActiveResultSets=true;
</pre>
Attach a database file on connect to a local SQL Server Express instance

<pre>
Server=.\SQLExpress;AttachDbFilename=C:\MyFolder\MyDataFile.mdf;Database=dbname;
Trusted_Connection=
</pre>

Todas estas cadenas de conexion las he sacado de la siguiente url:

https://www.connectionstrings.com/sql-server/



### Scaffold-DbContext Command

<pre>
dotnet ef dbcontext scaffold "Server=.\SQLEXPRESS;Database=SchoolDB;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer -o Models
</pre>

Estructura de la clase dbcontext en EF Core:

<pre>
public class SchoolContext : DbContext
{
    public SchoolContext()
    {
  
    }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
    }
    //entities
    public DbSet<Student> Students { get; set; }
    public DbSet<Course> Courses { get; set; }
} 
</pre>

<pre>
namespace EFCoreTutorials
{
    public class SchoolContext : DbContext
    {
        public DbSet<Student> Students { get; set; }
        public DbSet<Course> Courses { get; set; }

        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        { 
            optionsBuilder.UseSqlServer(@"Server=.\SQLEXPRESS;Database=SchoolDB;Trusted_Connection=True;");
        }
    }
}
</pre>

Para crear la base de datos:

<pre>
add-migration CreateSchoolDB
</pre>

<pre>
dotnet ef migrations add CreateSchoolDB
</pre>

Para materializar los cambios en la base de datos:

<pre>
 update-database –verbose
</pre>

<pre>
dotnet ef database update
</pre>

Luego agregar datos a dicha base de datos:

<pre>
namespace EFCoreTutorials
{
    class Program
    {
        static void Main(string[] args)
        {
            using (var context = new SchoolContext()) {

                var std = new Student()
                {
                     Name = "Bill"
                };

                context.Students.Add(std);
                context.SaveChanges();
            }
        }
    }
}
</pre>

### Procedimientos almacenados en Entity Framework


Una manera de añadir un procedimiento almacenado en code-first :<br>
Añadimos una migracion en blanco que nos generara un scaffolding

<pre>
Add-migration sp-GetStudents
</pre>

<pre>
public partial class spGetStudents : Migration
{
    protected override void Up(MigrationBuilder migrationBuilder)
    {
        var sp = @"CREATE PROCEDURE [dbo].[GetStudents]
                    @FirstName varchar(50)
                AS
                BEGIN
                    SET NOCOUNT ON;
                    select * from Students where FirstName like @FirstName +'%'
                END";

        migrationBuilder.Sql(sp);
    }

    protected override void Down(MigrationBuilder migrationBuilder)
    {

    }
}
</pre>

<pre>
Update-database
</pre>

De esta manera añadimos el procedimiento almacenado con el enfoque code-first a la base de datos.

Vamos a ver como se ejecuta el procedimiento sql con el metodo FromSql:

<pre>
var context = new SchoolContext(); 

var students = context.Students.FromSql("GetStudents 'Bill'").ToList()
</pre>

<pre>
var name = "Bill";

var context = new SchoolContext(); 
var students = context.Students
                      .FromSql($"GetStudents {name}")
                      .ToList();

//or
//var students = context.Students.FromSql($"exec GetStudents {name}").ToList();

</pre>

<pre>
var context = new SchoolContext(); 
var param = new SqlParameter("@FirstName", "Bill");
//or
/*var param = new SqlParameter() {
                    ParameterName = "@FirstName",
                    SqlDbType =  System.Data.SqlDbType.VarChar,
                    Direction = System.Data.ParameterDirection.Input,
                    Size = 50,
                    Value = "Bill"
};*/

var students = context.Students.FromSql("GetStudents @FirstName", param).ToList();
</pre>

Y con el metodo <code>ExecuteSqlCommand()</code> tendriamos lo siguiente:

<pre>
var context = new SchoolContext(); 

var rowsAffected = context.Database.ExecuteSqlCommand("Update Students set FirstName = 'Bill' where StudentId = 1;");
</pre>

<pre>
var context = new SchoolContext(); 

context.Database.ExecuteSqlCommand("CreateStudents @p0, @p1", parameters: new[] { "Bill", "Gates" });
</pre>

### Entity Framework Core Database-First

Tambien este enfoque es llamado desde EF core nuevas versiones "Ingeniería inversa".

Tenemos un articulo muy bueno explicando todo esto:

https://docs.microsoft.com/es-es/ef/core/managing-schemas/scaffolding.



Aqui tenemos algunos comandos de ejemplos de importar desde una base de datos el modelo relacional a un modelo de clases o de dominio:

<pre>
Scaffold-DbContext "host=server;database=test;user id=postgres;" Devart.Data.PostgreSql.Entity.EFCore
</pre>

<pre>
Scaffold-DbContext "host=server;database=test;user id=postgres;" Devart.Data.PostgreSql.Entity.EFCore -Tables dept,emp
</pre>

Aqui tenemos mas ejemplos:

<pre>
dotnet ef dbcontext scaffold "Data Source=(localdb)\MSSQLLocalDB;Initial Catalog=Chinook" Microsoft.EntityFrameworkCore.SqlServer
</pre>

Esto se utiliza con la herramienta secret manager:



<pre>
dotnet user-secrets set ConnectionStrings.Chinook "Data Source=(localdb)\MSSQLLocalDB;Initial Catalog=Chinook"
dotnet ef dbcontext scaffold Name=Chinook Microsoft.EntityFrameworkCore.SqlServer
</pre>

Especificacion de tablas:
El -Schemas parámetro en la PMC y --schema opción en la CLI puede utilizarse para incluir todas las tablas dentro de un esquema.

-Tables (PMC) y --table (CLI) puede usarse para incluir tablas específicas.

<pre>
Scaffold-DbContext ... -Tables Artist, Album
</pre>

<pre>
dotnet ef dbcontext scaffold ... --table Artist --table Album
</pre>

___

 .NET Core 3.1 Web API & Entity Framework Core Jumpstart

 https://www.youtube.com/watch?v=H4qg9HJX_SE

 
 
 
 
 
 
 
 ___

Entity Framework Core (CRUD Operation in .NET Core 3.0)

https://www.youtube.com/watch?v=VVWi9ZdAS9M


Hay que instalar Microsoft.EntityFrameworkCore y 
                 Microsoft.EntityFramework.SqlServer

                 




___

## Referencia de herramientas de Entity Framework Core: consola del administrador de paquetes en Visual Studio

https://docs.microsoft.com/es-es/ef/core/cli/powershell

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


___




