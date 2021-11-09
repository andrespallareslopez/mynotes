---
Titulo: "Apuntes Asp.Net Core"
---

# Apuntes Asp.Net Core
- [Apuntes Asp.Net Core](#apuntes-aspnet-core)
    - [NET CORE 3.1 Cookie Authentication](#net-core-31-cookie-authentication)
    - [ASP.NET Core 2.0 Cookie Authentication – Local logins](#aspnet-core-20-cookie-authentication--local-logins)
    - [Cookie authentication in ASP.NET Core 2 without ASP.NET Identity](#cookie-authentication-in-aspnet-core-2-without-aspnet-identity)
    - [Getting Started With Entity Framework Core - ASP.NET Core](#getting-started-with-entity-framework-core---aspnet-core)
    - [Creacion de una aplicacion ASP.NET core](#creacion-de-una-aplicacion-aspnet-core)
    - [Tutorial: Introducción a EF Core en una aplicación web de ASP.NET Core MVC](#tutorial-introducción-a-ef-core-en-una-aplicación-web-de-aspnet-core-mvc)
    - [Haciendo fácil el acceso a datos con Entity Framework Core (Parte 2)](#haciendo-fácil-el-acceso-a-datos-con-entity-framework-core-parte-2)
  - [Entity Framework Core «Code First» en Visual Studio](#entity-framework-core-code-first-en-visual-studio)
  - [Entity Framework Core «Code First» en DotNet CLI](#entity-framework-core-code-first-en-dotnet-cli)
  - [Logging in ASP.NET Core](#logging-in-aspnet-core)
  - [CRUD FullStack React JS, ASP.NET Core y SQL Server || Tutorial en Español || Parte 1](#crud-fullstack-react-js-aspnet-core-y-sql-server--tutorial-en-español--parte-1)

### NET CORE 3.1 Cookie Authentication

https://bjdejongblog.nl/net-core-3-1-cookie-authentication/

____

### ASP.NET Core 2.0 Cookie Authentication – Local logins

http://codereform.com/blog/post/asp-net-core-2-0-cookie-authentication-local-logins/

Como Extender Asp.net Identity y customizarlo

____

 
### Cookie authentication in ASP.NET Core 2 without ASP.NET Identity


https://www.meziantou.net/cookie-authentication-in-asp-net-core-2-without-asp-net-identity.htm

____
### Getting Started With Entity Framework Core - ASP.NET Core

https://www.learnentityframeworkcore.com/walkthroughs/aspnetcore-application

### Creacion de una aplicacion ASP.NET core

para crear una aplicacion ASP.NET core necesitamos desde la linea de comandos los siguiente:

~~~
     dotnet new mvc
     
     dotnet add package Microsoft.EntityFrameworkCore.SqlServer
     
     dotnet add package --version 1.1.0-msbuild3-final Microsoft.EntityFrameworkCore.Tools
     
     dotnet restore

     dotnet run
~~~

Si abrimos desde visual studio .csproj incluye la siguiente seccion:

~~~
    
   <ItemGroup>
    <DotNetCliToolReference
        Include="Microsoft.EntityFrameworkCore.Tools.DotNet"
        Version="1.0.0-msbuild3-final" />
   </ItemGroup>
    
~~~
    

Una vez que tenemos las herramientas de linea de comandos para entityframework podemos consultar lo siguiente:

<code>
    dotnet ef -h
</code>

Una vez que en el proyecto lo tenemos añadido, tenemos que crear un folder llamado Model y añadir lo siguiente:

- Las clases modelo
- La clase contexto de EF

Creamos el fichero EFCoreWebDemoContext.cs y tambien las clases modelos:

~~~
using Microsoft.EntityFrameworkCore;
namespace EFCoreWebDemo
{
    public class EFCoreWebDemoContext : DbContext
    {
        public DbSet<Book> Books { get; set; }
        public DbSet<Author> Authors { get; set; }
        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        {
            optionsBuilder.UseSqlServer(@"Server=.\;Database=EFCoreWebDemo;Trusted_Connection=True;MultipleActiveResultSets=true");
        }
    }
}
~~~

Añadiendo una migracion:
~~~
   dotnet ef migrations add CreateDatabase
~~~
Este comando añadira una carpeta migracions con unos archivos para llevar a cabo la migracion a la base de datos.

Despues para que se aplique la migracion a la base de datos, tenemos que lanzar el suguiente comando:

~~~
   dotnet ef database update
~~~

Podemos modicar la base de datos y hacer cambiar y aplicarlo a la base de datos con migraciones.

Por ejemplo añadimos lo siguiente a las clases correspondientes Author.cs y Book.cs

~~~
    using System.ComponentModel.DataAnnotations;
~~~

Luego tenemos las clases modelo mencionadas:


~~~
public class Book
{
    public int BookId { get; set; }
    [StringLength(255)]
    public string Title { get; set; }
    public int AuthorId { get; set; }
    public Author Author { get; set; }
}
~~~

~~~
public class Author
{
    public int AuthorId { get; set; }
    [StringLength(50)]
    public string FirstName { get; set; }
    [StringLength(75)]
    public string LastName { get; set; }
    public ICollection<Book> Books { get; set; } = new List<Book>();
}
~~~

Luego volvemos a lanzar los comandos de migraciones:

~~~
    dotnet ef migrations add LimitStrings
~~~

~~~
    dotnet ef database update
~~~

Luego en los controladores para trabajar con esos datos, podemos hacer lo siguiente:

~~~
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore;
namespace EFCoreWebDemo.Controllers
{
    public class AuthorController : Controller
    {
        public async Task<IActionResult> Index()
        {
            using (var context = new EFCoreWebDemoContext())
            {
                var model = await context.Authors.AsNoTracking().ToListAsync();
                return View(model);
            }
            
        }  
        [HttpGet]
        public IActionResult Create()
        {
            return View();
        }
        [HttpPost]
        public async Task<IActionResult> Create([Bind("FirstName, LastName")] Author author)
        {
            using (var context = new EFCoreWebDemoContext())
            {
                context.Add(author);
                await context.SaveChangesAsync();
                return RedirectToAction("Index");
            }
        }
    }
~~~

Luego tenemos el apartado de la vistas:
~~~
@model IEnumerable<Author>
@{
    ViewBag.Title = "Authors";
}
<h1>@ViewBag.Title</h1>
<ul>
@foreach (var author in Model)
{
    <li>@author.FirstName @author.LastName</li>
}
</ul>
<div>@Html.ActionLink("New", "create")

</pre>

<pre>
@model Author
@{
    ViewBag.Title = "New Author";
}
<h1>@ViewBag.Title</h1>
@using(Html.BeginForm()){
  <div class="form-group">
    @Html.LabelFor(model => model.FirstName)
    @Html.TextBoxFor(model => model.FirstName, new { @class="form-control"}) 
  </div>
  <div class="form-group">
    @Html.LabelFor(model => model.LastName)
    @Html.TextBoxFor(model => model.LastName, new { @class="form-control"}) 
  </div>
  <button type="submit" class="btn btn-default">Submit</button>
}
~~~

luego para ver que todo ha ido bien podemos hacer los siguiente:

~~~
    dotnet build
~~~

~~~
    dotnet run
~~~

Luego podemos añadir los formularios para ir añadiendo datos a la base de datos:

~~~
using System.Threading.Tasks;
using System.Linq;
using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore;
using Microsoft.AspNetCore.Mvc.Rendering;
namespace EFCoreWebDemo.Controllers
{
    public class BookController : Controller
    {
        public async Task<IActionResult> Index()
        {
            using (var context = new EFCoreWebDemoContext())
            {
                var model = await context.Authors.Include(a => a.Books).AsNoTracking().ToListAsync();
                return View(model);
            }
            
        }  
        [HttpGet]
        public async Task<IActionResult> Create()
        {
            using(var context = new EFCoreWebDemoContext())
            {
                var authors = await context.Authors.Select(a => new SelectListItem {
                    Value = a.AuthorId.ToString(), 
                    Text = $"{a.FirstName} {a.LastName}"
                }).ToListAsync();
                ViewBag.Authors = authors;
            }
            return View();
        }
        [HttpPost]
        public async Task<IActionResult> Create([Bind("Title, AuthorId")] Book book)
        {
            using (var context = new EFCoreWebDemoContext())
            {
                context.Books.Add(book);
                await context.SaveChangesAsync();
                return RedirectToAction("Index");
            }
        }
    }
}

~~~

Y luego tenemos las vistas asociadas:

~~~
@model IEnumerable<Author>
@{
    ViewBag.Title = "Authors and their books";
}
<h1>@ViewBag.Title</h1>
@if(Model.Any()){
    <ul>
    @foreach(var author in Model){
        <li>@author.FirstName @author.LastName
            <ul>
            @foreach(var book in author.Books){
                <li>@book.Title</li>
            }
            </ul>
        </li>
    }
    </ul>
}
<div>@Html.ActionLink("New", "create")
~~~


~~~
@model Book
@{
    ViewBag.Title = "New Book";
}
<h1>@ViewBag.Title</h1>
@using(Html.BeginForm()){
  <div class="form-group">
    @Html.LabelFor(model => model.AuthorId)
    @Html.DropDownListFor(model => model.AuthorId, (IEnumerable<SelectListItem>)ViewBag.Authors, string.Empty, new { @class="form-control"}) 
  </div>
  <div class="form-group">
    @Html.LabelFor(model => model.Title)
    @Html.TextBoxFor(model => model.Title, new { @class="form-control"}) 
  </div>
  <button type="submit" class="btn btn-default">Submit</button>
}
~~~



____

### Tutorial: Introducción a EF Core en una aplicación web de ASP.NET Core MVC

https://docs.microsoft.com/es-es/aspnet/core/data/ef-mvc/intro?view=aspnetcore-5.0


Esta para la version ASP.NET core 5.0, tal vez sera valido para ASP.NET 3.1

Tenemos la configuracion de la pagina maesta layout.cshtml en:

~~~
    Views/Shared/_Layout.cshtml
~~~

Paquetes Nuget de EF Core:

*Microsoft.EntityFrameworkCore.SqlServer*

Con Powershell podemos añadirlo de la siguiente manera:

~~~
Install-Package Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore
Install-Package Microsoft.EntityFrameworkCore.SqlServer

~~~

Aparte de crear los modelos y la base de datos tenemos que crear el contexto de EF:

~~~
using ContosoUniversity.Models;
using Microsoft.EntityFrameworkCore;

namespace ContosoUniversity.Data
{
    public class SchoolContext : DbContext
    {
        public SchoolContext(DbContextOptions<SchoolContext> options) : base(options)
        {
        }

        public DbSet<Course> Courses { get; set; }
        public DbSet<Enrollment> Enrollments { get; set; }
        public DbSet<Student> Students { get; set; }

         protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            modelBuilder.Entity<Course>().ToTable("Course");
            modelBuilder.Entity<Enrollment>().ToTable("Enrollment");
            modelBuilder.Entity<Student>().ToTable("Student");
        }


    }
}

~~~

Luego tenemos que registrar el Contexto de EF en el pipeline de ASP.NET core mediante inyeccion de dependencias:

~~~
using ContosoUniversity.Data;
using Microsoft.EntityFrameworkCore;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;

namespace ContosoUniversity
{
    public class Startup
    {
        public Startup(IConfiguration configuration)
        {
            Configuration = configuration;
        }

        public IConfiguration Configuration { get; }

        public void ConfigureServices(IServiceCollection services)
        {
            services.AddDbContext<SchoolContext>(options =>
                options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));

            services.AddControllersWithViews();
        }
~~~


y en el archivo appsettings.json añadimos lo siguiente:

~~~
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=ContosoUniversity1;Trusted_Connection=True;MultipleActiveResultSets=true"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  },
  "AllowedHosts": "*"
}
~~~

Añadimos unos filtros de excepcion de la base de datos llamado AddDatabaseDeveloperPageExceptionFilter proporciona informacion util en el entorno de desarrollo.

~~~
public void ConfigureServices(IServiceCollection services)
{
    services.AddDbContext<SchoolContext>(options =>
        options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));

    services.AddDatabaseDeveloperPageExceptionFilter();

    services.AddControllersWithViews();
}
~~~

Aparte de con migraciones podemos crear la base de datos imperativamente con EnsureCreated de la siguiente manera (context.Database.EnsureCreated())


Vamos a crear una carpeta Data y ahi vamos a crear archivo y clase llamada DbInitializer.cs con el codigo siguiente:
~~~
using ContosoUniversity.Models;
using System;
using System.Linq;

namespace ContosoUniversity.Data
{
    public static class DbInitializer
    {
        public static void Initialize(SchoolContext context)
        {
            context.Database.EnsureCreated();

            // Look for any students.
            if (context.Students.Any())
            {
                return;   // DB has been seeded
            }

            var students = new Student[]
            {
            new Student{FirstMidName="Carson",LastName="Alexander",EnrollmentDate=DateTime.Parse("2005-09-01")},
            new Student{FirstMidName="Meredith",LastName="Alonso",EnrollmentDate=DateTime.Parse("2002-09-01")},
            new Student{FirstMidName="Arturo",LastName="Anand",EnrollmentDate=DateTime.Parse("2003-09-01")},
            new Student{FirstMidName="Gytis",LastName="Barzdukas",EnrollmentDate=DateTime.Parse("2002-09-01")},
            new Student{FirstMidName="Yan",LastName="Li",EnrollmentDate=DateTime.Parse("2002-09-01")},
            new Student{FirstMidName="Peggy",LastName="Justice",EnrollmentDate=DateTime.Parse("2001-09-01")},
            new Student{FirstMidName="Laura",LastName="Norman",EnrollmentDate=DateTime.Parse("2003-09-01")},
            new Student{FirstMidName="Nino",LastName="Olivetto",EnrollmentDate=DateTime.Parse("2005-09-01")}
            };
            foreach (Student s in students)
            {
                context.Students.Add(s);
            }
            context.SaveChanges();

            var courses = new Course[]
            {
            new Course{CourseID=1050,Title="Chemistry",Credits=3},
            new Course{CourseID=4022,Title="Microeconomics",Credits=3},
            new Course{CourseID=4041,Title="Macroeconomics",Credits=3},
            new Course{CourseID=1045,Title="Calculus",Credits=4},
            new Course{CourseID=3141,Title="Trigonometry",Credits=4},
            new Course{CourseID=2021,Title="Composition",Credits=3},
            new Course{CourseID=2042,Title="Literature",Credits=4}
            };
            foreach (Course c in courses)
            {
                context.Courses.Add(c);
            }
            context.SaveChanges();

            var enrollments = new Enrollment[]
            {
            new Enrollment{StudentID=1,CourseID=1050,Grade=Grade.A},
            new Enrollment{StudentID=1,CourseID=4022,Grade=Grade.C},
            new Enrollment{StudentID=1,CourseID=4041,Grade=Grade.B},
            new Enrollment{StudentID=2,CourseID=1045,Grade=Grade.B},
            new Enrollment{StudentID=2,CourseID=3141,Grade=Grade.F},
            new Enrollment{StudentID=2,CourseID=2021,Grade=Grade.F},
            new Enrollment{StudentID=3,CourseID=1050},
            new Enrollment{StudentID=4,CourseID=1050},
            new Enrollment{StudentID=4,CourseID=4022,Grade=Grade.F},
            new Enrollment{StudentID=5,CourseID=4041,Grade=Grade.C},
            new Enrollment{StudentID=6,CourseID=1045},
            new Enrollment{StudentID=7,CourseID=3141,Grade=Grade.A},
            };
            foreach (Enrollment e in enrollments)
            {
                context.Enrollments.Add(e);
            }
            context.SaveChanges();
        }
    }
}
~~~

Y en el program.cs tenemos lo siguiente:

~~~
using ContosoUniversity.Data;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;
using System;

namespace ContosoUniversity
{
    public class Program
    {
        public static void Main(string[] args)
        {
            var host = CreateHostBuilder(args).Build();

            CreateDbIfNotExists(host);

            host.Run();
        }

        private static void CreateDbIfNotExists(IHost host)
        {
            using (var scope = host.Services.CreateScope())
            {
                var services = scope.ServiceProvider;
                try
                {
                    var context = services.GetRequiredService<SchoolContext>();
                    DbInitializer.Initialize(context);
                }
                catch (Exception ex)
                {
                    var logger = services.GetRequiredService<ILogger<Program>>();
                    logger.LogError(ex, "An error occurred creating the DB.");
                }
            }
        }

        public static IHostBuilder CreateHostBuilder(string[] args) =>
            Host.CreateDefaultBuilder(args)
                .ConfigureWebHostDefaults(webBuilder =>
                {
                    webBuilder.UseStartup<Startup>();
                });
    }
}
~~~

Tenemos disponible desde program con el 

- using ContosoUniversity.Data;
- using Microsoft.Extensions.DependencyInjection;

acceso al servicio de injeccion de dependencias y solicitar una instancia del contexto

Luego en los controladores podemos hacer lo siguiente:

~~~
   namespace ContosoUniversity.Controllers
{
    public class StudentsController : Controller
    {
        private readonly SchoolContext _context;

        public StudentsController(SchoolContext context)
        {
            _context = context;
        }


public async Task<IActionResult> Index()
{
    return View(await _context.Students.ToListAsync());
}
~~~
Luego creamos las vistas:

____

### Haciendo fácil el acceso a datos con Entity Framework Core (Parte 2)

https://www.fixedbuffer.com/entity-framework-core-2/

Aqui en este ejemplo utiliza mysql como servidor de base de datos.

Podemos verlo como creando la solucion desde Visual Studio con powershell, o creando la solucion desde Visual studio code y con DotNet Cli.

Instala dos paquetes:
 
Con powershell desde visual studio
~~~
Install-Package Microsoft.EntityFrameworkCore -Version 2.1.3

Install-Package Microsoft.EntityFrameworkCore.Tools -Version 2.1.3

Install-Package Pomelo.EntityFrameworkCore.MySql -Version 2.1.2

~~~


y con DotNet cli 

~~~
- dotnet new console
– dotnet add package Microsoft.EntityFrameworkCore -v 2.1.3
– dotnet add package Microsoft.EntityFrameworkCore.Tools -v 2.1.3
– dotnet add package Pomelo.EntityFrameworkCore.MySql -v 2.1.2
~~~

Luego tenemos que generar el contexto y los modelos y podemos verlo con las siguientes clases:

~~~
//Alumnos.cs
using System;
using System.ComponentModel.DataAnnotations;

namespace PostCore.Data
{
    public class Alumnos
    {
        [Key]
        public int IdAlumno { get; set; } //Clave primaria
        public string Nombre { get; set; } 
        public DateTime Nacimiento { get; set; }
        public int IdCurso { get; set; } //Campo clave foranea

        //Entity Framewrok Core
        public Cursos Curso { get; set; } //Objeto de navegación virtual EFC
    }
}

//Cursos.cs
using System.Collections.Generic;
using System.ComponentModel.DataAnnotations;

namespace PostCore.Data
{
    public class Cursos
    {
        //Inicializamos el objeto de navegacion virtual de Entity Framework Core
        public Cursos()
        {
            Alumnos = new HashSet<Alumnos>();
        }

        [Key]
        public int IdCurso { get; set; } //Clave primaria
        public string Nombre { get; set; }
        public string Ciudad { get; set; }
        public int IdProfesor { get; set; } //Campo clave foranea

        //Entity Framewrok Core
        public Profesores Profesor { get; set; } //Objeto de navegación virtual EFC
        public ICollection<Alumnos> Alumnos { get; set; } //Objeto de navegación virtual EFC
    }
}

//Profesores.cs
using System.Collections.Generic;
using System.ComponentModel.DataAnnotations;

namespace PostCore.Data
{
    public class Profesores
    {
        //Inicializamos el objeto de navegacion virtual de Entity Framework Core
        public Profesores()
        {
            Cursos = new HashSet<Cursos>();
        }
        [Key]
        public int IdProfesor { get; set; } //Clave primaria
        public string Nombre { get; set; }

        //Entity Framewrok Core
        public ICollection<Cursos> Cursos { get; set; } //Objeto de navegación virtual EFC
    }
}

//PostDbContext.cs
using Microsoft.EntityFrameworkCore;

namespace PostCore.Data
{
    //Heredamos de DbContext nuestro contexto
    class PostDbContext : DbContext
    {
        //Constructor sin parametros
        public PostDbContext()       
        {
        }

        //Constructor con parametros para la configuracion
        public PostDbContext(DbContextOptions options)
        : base(options)
        {
        }

        //Sobreescribimos el metodo OnConfiguring para hacer los ajustes que queramos en caso de
        //llamar al constructor sin parametros
        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        {
            //En caso de que el contexto no este configurado, lo configuramos mediante la cadena de conexion
            if (!optionsBuilder.IsConfigured) 
            {
                optionsBuilder.UseMySql("Server=localhost;Database=postefcore;Uid=root;Pwd=root;");
            }
        }

        //Tablas de datos
        public virtual DbSet<Alumnos> Alumnos { get; set; }
        public virtual DbSet<Cursos> Cursos { get; set; }
        public virtual DbSet<Profesores> Profesores { get; set; }
    }
}

~~~

## Entity Framework Core «Code First» en Visual Studio

Ahora vamos a ver Entity framework core Code First en visual studio con powershell, los comandos relacionados para hacer migraciones:

**add-migration**: Con este comando, generaremos la migración que lanzaremos a la base de datos. Este comando tiene 2 parámetros:

{nombre}: Con este parámetro indicaremos el nombre que queremos indicarle a la migración, ademas, es obligatorio.
-Context {contexto}: En caso de tener más de un contexto de datos en nuestro programa, indicaremos cual de los contextos es mediante este parámetro. Si solo tenemos un contexto de datos, no es obligatorio usarlo.
**remove-migration**: Con este comando, eliminaremos la ultima migración que hemos generado. Se puede utilizar varias veces consecutivamente para ir eliminando migraciones desde la última a la primera.

**update-database**: Con este comando, enviaremos a la base de datos los cambios de la migración, haciéndola efectiva:

{nombre}: Con este parámetro indicaremos el nombre de la migración que queremos aplicar.
-Context {contexto}: En caso de tener más de un contexto de datos en nuestro programa, indicaremos cual de los contextos es mediante este parámetro. Si solo tenemos un contexto de datos, no es obligatorio usarlo.
**drop-database**: Con este comando, eliminaremos la base de datos. Este comando tiene 1 parámetro:

-Context {contexto}: En caso de tener más de un contexto de datos en nuestro programa, indicaremos cual de los contextos es mediante este parámetro. Si solo tenemos un contexto de datos, no es obligatorio usarlo.


Y para empezar a utilizar las migraciones, lanzamos el siguiente comando:

~~~
add-migration init -Context PostDbContext
~~~

Esto genera una carpeta «Migrations» donde va a ir guardando cada una de las migraciones. Conviene no borrar el contenido, ya que almacena las «versiones» del contexto de datos, de modo que podemos revertir los cambios en la base de datos. Ademas, el hecho de almacenar estas migraciones, permite al sistema aplicar cambios de manera incremental en las próximas migraciones, y es requisito para poder aplicar cambios a la base de datos sin que se produzcan errores por tablas ya existentes.

Con eso, ejecutamos:

~~~
  update-database -Context PostDbContext
~~~

## Entity Framework Core «Code First» en DotNet CLI

____

## Logging in ASP.NET Core

https://www.tutorialsteacher.com/core/aspnet-core-logging


~~~
Microsoft.Extensions.Logging.Console
Microsoft.Extensions.Logging.Debug
Microsoft.Extensions.Logging.EventSource
Microsoft.Extensions.Logging.TraceSource
~~~

Tenemos en program el siguiente codigo:
~~~
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
               .UseStartup<Startup>();
}
~~~
Por defecto tenemos el siguiente codigo en el metodo WebHost.CreateDefaultBuilder() relacionado con tracear el codigo de la aplicacion, y esta porcion de codigo por defecto la podemos ver en github
~~~
.ConfigureLogging((hostingContext, logging) =>
    {
        logging.AddConfiguration(hostingContext.Configuration.GetSection("Logging"));
        logging.AddConsole();
        logging.AddDebug();
        logging.AddEventSourceLogger();
    }).
~~~




~~~

~~~

___

## CRUD FullStack React JS, ASP.NET Core y SQL Server || Tutorial en Español || Parte 1

https://www.youtube.com/watch?v=Usj0J4rUumI&list=PLqC1FgzJhTiw4HaSmkN8_mMgKlZayIQHe

Creamos un proyecto asp.net core Web api en visual studio


Agregamos el siguiente paquete nuget 
~~~
Install-Package Microsoft.EntityFrameworkCore.SqlServer -Version 3.1.7
~~~


- Generamos las clases POCO, con ciertos atributos
- Generamos el fichero AppDbContext
- Agregamos una cadena de conexion al fichero AppSettings.json


Cadena de conexion en AppSettings.json
~~~
   .
   .
   .
"ConnectionStrings": {
    "conexion" : "data source=(LocalDb)\\MSSQLLocalDB; initial catalog=prueba; user id=sa; password=Admin;MultipleActiveResulsets=true"
} 
   .
   .
   .
~~~



Archivo AppDbContext.cs
~~~
public class AppDbContext : DbContext
{
     public AppDbContext(DbContextOptions<AppContext> options)
     {

     }
     public DbSet<Gestores_Bd> gestores_bd {get;set;}
     
}


~~~
Luego en el fichero StartUp.cs tenemos que añadir en el metodo ConfigureServices lo siguiente:

Tenemos que habilitar CORS para que puedan hacer llamadas desde la parte frontal
~~~
public void ConfigureServices(IServiceCollection services)
{
    services.AddCors();
    services.AddControllers();
    
    services.AddBdContext<AppDbContext>(options => options.UseSqlServer(Configuration.GetConnectionString("Conexion")));
}

public void Configure(IApplicationBuilder app,IwebHostEnvironment env)
{
    app.UseCors(options => 
    {
        options.WithOrigins("http://localhost:3000");
        options.AllowAnyMethod();
        options.AllowAnyHeader();
    });
}

~~~
Clase controlador de API

~~~
    .
    .
    .
private readonly AppDbContext context;

//Constructor del controller
public GestoresController()
{
   this.context = context;  
}
   .
   .
   .
~~~
En  un action de tipo get escribimos los siguiente:
~~~

[HttpGet]
public ActionResult Get()
{
    try
    {
        return Ok(context.gestores_bd.ToList());
    }catch(Exception ex)
    {
        return BadRequest(ex.Message);
    }
}

[HttpGet("{id}",Name="GetGestor")]
public ActionResult Get(int id)
{
    try
    {
    var gestor = context.gestores_bd.FirstOrDefault(g =>g.id == id);
    return Ok(gestor);
    }catch(Exception ex)
    {
        return BadRequest(ex.Message);
    }
}

~~~
Creamos otro actions  para peticiones tipo POST hacemos lo siguiente;
~~~
[HttpPost]
public ActionResult Post([FromBody]Gestores_Bd gestor)
{
    try
    {
       context.gestores_bd.Add(gestor);
       context.SaveChanges();
       return CreateAtRoute("GetGestor", new { id = gestor.id}, gestor); 
    }catch(Exception ex)
    {
        return BadRequest(ex.Message);
    }
}

~~~
Create otro Action para peticiones PUT de actualizacion:

~~~
[HttpPut("{id}")]
public ActionResult Put(int id, [FromBody]Gestores_Bd gestor)
{
    try
    {
       if (gestor.id == id)
       {
           context.Entry(gestor).State = EntityState.Modified;
           context.SaveChanges();ç
           return CreatedAtRoute("GetGestor", new {id = gestor.id}, gestor);
       }
       else
       {
           return BadRequest();
       }
    }catch (Exception ex)
    {
        return BadRequest();
    }
}
~~~
Crear otra action para borrar un registro
~~~
[HttpDelete("{id}")]
public ActionResult Delete(int id)
{
    try
    {
        var gestor = context.gestores_bd.FirstOrDefault(g => g.id == id); 
        if (gestor != null)
        {
            context.gestores_bd.Remove(gestor);
            context.SaveChanges();
            return Ok(id);
        }
    }catch(Exception ex)
    {
        return BadRequest(ex.Message);
    }
}

~~~
Luego vamos a utilizar react en la parte frontal con visual studio code.

Instalamos las siguientes librerias
~~~
npm i bootstrap reactstrap axios
~~~


Y creamos el App.js
~~~
import React,{useState,useEffect} from 'react';
import './App.css'
import 'bootstrap/dist/css/bootstrap.min.css';
import axios from 'axios';
import {Modal,ModalBody,ModalFooter,ModalHeader} from 'reactstrap';

function App() {
    const baseUrl = "https://-...."
    const [data,setData] = useState([]);
    
    const peticionGet = async() => {
         await axios.get(baseUrl).then(response => {
             setData(response.data);

         }).catch(error => {
             console.log(error)
         })
    }
    
    useEffect(()=>{
        peticionGet();
    },[])
    
     
    return (
        <div className="App" >
           <table className="table table-bordered" >
               <thead>
                  <tr>
                     <th>ID</th>
                     <th>Nombre</th>
                     <th>Lanzamiento</th>
                     <th>Desarrollador</th>
                     <th>Acciones</th>
                  </tr>
               <thead>
               <tbody>
                {data.map(gestor =>(
                 <tr key={gestor.id} >
                    <td>{gestor.id}</td>
                    <td>{gestor.nombre}</td>
                    <td>{gestor.lanzamiento}</td>
                    <td>{gestor.desarrollador}</td>
                    <td>
                        <button className="btn btn-primary">Editar</button> {"  "}
                        <button className="btn btn-danger">Eliminar</button>
                    </td>
                 </tr>
                ))}    
               </tbody>     
           </table>  
        </div>
    )
}

export default App;
~~~



~~~

~~~

___

Mini Profiler for ASP.ET Core Projects

https://www.youtube.com/watch?v=7ThPz-9XM54

___

Using .NET Memory Profiler to investigate memory issues

https://www.youtube.com/watch?v=b0tiHyeotRU

___

Using Visual Studio Diagnostic tools to investigate memory issues

https://www.youtube.com/watch?v=TK1HfJ9pn7g

___

Performance Profiling | .NET Object Allocation Tracking Tool

https://www.youtube.com/watch?v=60euKwSqT-U

___

Performance Profiling | CPU Usage Tool

https://www.youtube.com/watch?v=X1-uHpEqNGM

___













